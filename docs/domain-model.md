# Domain Model

## User
Represents authentication credentials.

### Attributes
- id
- username
- password
- status
- createdAt
- updatedAt

### Responsibilities
- Authenticate into the system.
- Control system access.

### Relationships
```text
User
├── 1 Customer OR
└── 1 Employee
```

---

## Customer
Represents a banking customer.

### Attributes

- id
- firstName
- lastName
- email
- birthDate
- phoneNumber
- address
- status
- createdAt

### Responsibilities
- Manage owned accounts.
- Manage beneficiaries.
- Make transfers.
- View transfer history.
- Receive notifications.
 
### Relationships
```text
Customer
├── 1 User
├── N Accounts
├── N Beneficiaries
├── N Transfers
└── N Notifications
```

---

## Employee
Represents a bank employee.

### Attributes
- id
- employeeCode
- firstName
- lastName
- email
- role
- status
- createdAt

### Responsibilities
- Review bank operations.
- Approve or reject transfers.
- Access audit information.

### Relationships
```text
Employee
├── 1 User
├── N Approvals
└── N Audit Queries
```

---

## EmployeeRole
Represents employee permissions.

### Values
- SUPERVISOR
- ADMIN
 
### Responsibilities
- Define employee system permissions.

---

## Account
Represents a bank account.

### Attributes
- id
- accountNumber
- accountType
- balance
- status
- createdAt

### Responsibilities
- Store customer funds.
- Act as source or destination for transfers.

### Relationships
```text
Account
├── 1 Customer
├── 1 AccountType
├── N Outgoing Transfers
└── N Incoming Transfers
```

---

## AccountType
Represents the type of bank account.

### Values
- SAVINGS
- CHECKING
- INVESTMENT

### Responsibilities
- Define account behavior and business rules.

---
## AccountStatus
Represents the status of the account

### Values
- ACTIVE
- BLOCKED
- CLOSED

### Responsibilities
- Define account behavior and business rules.

---

## Beneficiary
Represents a transfer recipient.

### Attributes
- id
- alias
- ownerName
- destinationAccountNumber
- destinationBank
- status
- createdAt

### Responsibilities
- Allow clients to save recipients for future transfers.

### Relationships
```text
Beneficiary
├── 1 Customer (Owner)
└── N Transfers
```

---

## Transfer
Represents a money transfer.

### Attributes
- id
- amount
- description
- status
- referenceNumber
- transferType
- createdAt
- processedAt

### Responsibilities
- Transfer funds between accounts.
- Trigger approval workflow when required.

### Relationships
```text
Transfer
├── 1 Source Account
├── 1 Destination Account
├── 1 Customer
├── 0..1 Approval
├── N AuditLogs
└── 1 TransferReceipt
```

---

## TransferType
Represents the type of transfer.

### Values
- INTERNAL
- EXTERNAL

### Responsibilities
- Define transfer processing behavior.

---

## TransferStatus
Represents the current transfer status.

### Values
- PENDING
- APPROVED
- REJECTED
- EXECUTED
- FAILED

----

## Approval
Represents a transfer approval process.

### Attributes
- id
- decision
- comments
- approvedBy
- approvedAt

### Responsibilities
- Approve or reject high value transfers.

### Relationships
```text
Approval
├── 1 Transfer
└── 1 Employee
```

---

## AuditLog
Represents a system audit record.

### Attributes
- id
- userId
- action
- entityType
- entityId
- details
- timestamp

### Responsibilities
- Maintain operation traceability.

### Relationships
```text
AuditLog
├── 1 Employee
└── 1 Related Entity
```

---

## Notification
Represents a system notification.

### Attributes
- id
- title
- message
- status
- createdAt

### Responsibilities
- Notify users about important events.

## Relationships
```text
Notification
└── 1 Customer
```

## Business Constraints
### BC-001
A user must be at least 18 years old to create a bank account.
### BC-002
A transfer cannot be made if the source account balance is insufficient.
### BC-003
A transfer cannot be made between the same source and destination account.
### BC-004
Transfers above $15,000 require supervisor approval.
### BC-005
Only ACTIVE accounts can send or receive transfers.
### BC-006
Only employees with role SUPERVISOR can approve transfers.
### BC-007
A supervisor cannot approve a transfer that was created by the same user.
### BC-008
All transfer operations must generate an audit record.
### BC-009
A blocked customer cannot perform transfers.
### BC-010
A beneficiary must have at least one active account.
### BC-011
Only ACTIVE users can authenticate into the system.
