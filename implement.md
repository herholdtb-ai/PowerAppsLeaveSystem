# Implementation Checklist: Power Leave (Integrated)

## Phase 1: SharePoint Setup
- [ ] **Create List**
  - [ ] Name: `LeaveRequests`
- [ ] **Add Columns**
  - [ ] `RequesterEmail` (Single line text)
  - [ ] `SupervisorEmail` (Single line text)
  - [ ] `StartDate` (Date)
  - [ ] `EndDate` (Date)
  - [ ] `Reason` (Multiple lines of text, Plain text)
  - [ ] `Status` (Choice: Pending, Approved, Denied)
  - [ ] *Ref:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Power App Development
- [ ] **Connectors**
  - [ ] Connect `SharePoint` (LeaveRequests list).
  - [ ] Connect `Office 365 Users`.
- [ ] **Global Logic**
  - [ ] Set `App.OnStart`: `Set(varCurrentUser, Office365Users.MyProfileV2())`.
- [ ] **UI Components**
  - [ ] Display `varCurrentUser.displayName` in a Label.
  - [ ] Create Supervisor Combo Box: `Office365Users.SearchUser({searchTerm: Self.SearchText})`.
  - [ ] Create Multi-line Text Input for `Reason`.
- [ ] **Submit Button**
  - [ ] Implement `Patch` function to write to SharePoint.
  - [ ] *Ref:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)

## Phase 3: Approval Workflow
- [ ] **Trigger**
  - [ ] SharePoint: `When an item is created`.
- [ ] **Approval Action**
  - [ ] Action: `Start and wait for an approval`.
  - [ ] Assigned to: `SupervisorEmail` dynamic value.
- [ ] **Outcome Update**
  - [ ] Update SharePoint item `Status` based on response.
  - [ ] *Ref:* [ApprovalNotificationFlow.json](./PowerAutomate/ApprovalNotificationFlow.json)

## Phase 4: Launch
- [ ] **Permissions**
  - [ ] Grant staff "Contribute" access to SharePoint List.
- [ ] **Publishing**
  - [ ] Save and Publish the App version 1.0.
