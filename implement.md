# Implementation Checklist: Power Leave (Two-Stage Approval)

## Phase 1: SharePoint Setup
- [ ] **Create List**
  - [ ] Name: `LeaveRequests`
- [ ] **Add Columns**
  - [ ] `RequesterEmail` (Text)
  - [ ] `SupervisorEmail` (Text)
  - [ ] `StartDate` (Date)
  - [ ] `EndDate` (Date)
  - [ ] `ReasonDetails` (Multiline Text, Plain)
  - [ ] `OverallStatus` (Choice: Awaiting Support, Awaiting Principal, Approved, Rejected, Not Supported)
  - [ ] *Ref:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Power App Development
- [ ] **Connectors**
  - [ ] Connect `SharePoint` & `Office 365 Users`.
- [ ] **Form Construction**
  - [ ] User Header: `varCurrentUser.displayName`.
  - [ ] Supervisor Picker: `Office365Users.SearchUser`.
  - [ ] Reason Input: Multi-line text.
- [ ] **Submit Logic**
  - [ ] Implement `Patch` with `OverallStatus` set to "Awaiting Support".
  - [ ] *Ref:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)

## Phase 3: Workflow Logic
- [ ] **Trigger**
  - [ ] SharePoint: `When an item is created`.
- [ ] **Conditional Branching**
  - [ ] IF `SupervisorEmail` == `bezuidenhouth@hsgrabouw.co.za` -> Skip to Principal Approval.
- [ ] **Supervisor Stage**
  - [ ] Action: Approval (Support/Not-Support).
  - [ ] Update Status based on outcome.
- [ ] **Principal Stage**
  - [ ] Action: Approval (Approve/Reject) assigned to `bezuidenhouth@hsgrabouw.co.za`.
  - [ ] *Ref:* [LeaveRequestApprovalFlow.json](./PowerAutomate/LeaveRequestApprovalFlow.json)

## Phase 4: Deployment
- [ ] **Permissions**
  - [ ] Grant staff "Contribute" access to SharePoint.
- [ ] **Publish**
  - [ ] Save and Publish App v1.0.
