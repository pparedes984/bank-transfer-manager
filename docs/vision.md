# Bank Transfer Manager

## Project Overview
Bank Transfer Manager is a banking platform designed to manage bank accounts, money transfers, approvals, notifications, and audit records.
The system enables clients to perform secure transfers while allowing supervisors and administrators to control, review, and audit financial operations.

## Problem Statement
Financial institutions require controls for bank transfers, high-value amount approvals, transaction auditing, 
and secure user management.

## Objectives
1. Manage users.
2. Manage bank accounts.
3. Make transfers.
4. Approve high-value transfers.
5. Audit all transactions.

## Actors
CLIENT  
Can: 
- Log in 
- Log out
- View accounts
- Transfer money 
- Manage beneficiaries 
- View transaction history 
- Download transaction receipts
- Create inversion accounts


SUPERVISOR  
Can: 
- Approve transfers 
- Reject Transfers
- Review pending transfers
- Review aproval history
- view audit history

ADMIN  
Can: 
- Manage users 
- Manage transaction limits
- Block users
- Unblock users
- Assign roles
- View audit logs

## Functional Requirements
### FR-001 User Authentication
The system shall allow users to authenticate using username and password.
### FR-002 Account Management
The system shall allow clients to view their bank accounts.
### FR-003 Beneficiary Management
The system shall allow clients to create, update and delete beneficiaries.
### FR-004 Transfer Creation
The system shall allow clients to create money transfers.
### FR-005 Transfer Approval
The system shall allow supervisors to approve or reject transfers requiring authorization.
### FR-006 Transaction History
The system shall allow clients to review historical transactions.
### FR-007 Audit Logging
The system shall record all user actions for auditing purposes.
### FR-008 Notification Management
The system shall notify users about transfer status changes.
### FR-009 User Management
The system shall allow administrators to manage users and roles.

## High-Level Transfer Flow
1. Client logs into the system.
2. Client selects a source account.
3. Client selects or creates a beneficiary.
4. Client enters the transfer amount.
5. System validates balance and account status.
6. System evaluates transfer approval rules.
7. If approval is not required, the transfer is executed.
8. If approval is required, the transfer is sent for review.
9. Supervisor approves or rejects the transfer.
10. System executes the transfer if approved.
11. System generates the transaction receipt.
12. System logs the operation in the audit trail.
13. System sends a notification to the client.

## Business Rules
### BR-001
Transfers up to $5,000 are processed automatically.
### BR-002
Transfers above $5,000 require supervisor approval.
### BR-003
The source account must have sufficient balance.
### BR-004
The destination account must exist and be active.
### BR-005
All operations must be audited.
### BR-006
Clients can save beneficiaries for future transfers.
### BR-007
A client can own multiple bank accounts.
### BR-008
The initial account is created by the bank.
### BR-009
Clients can create new investment accounts.
