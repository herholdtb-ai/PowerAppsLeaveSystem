# Implementation Checklist: Power Leave (O365 Integrated)

## Phase 1: Data Backend
- [ ] **SharePoint List Creation**
  - [ ] Create list `LeaveRequests`.
  - [ ] Add columns: `RequesterEmail` (Text), `Department` (Text), `SupervisorEmail` (Text), `LeaveType` (Choice), `StartDate` (Date), `EndDate` (Date), `Status` (Choice).
  - [ ] *Ref:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Power Apps Development
- [ ] **Data Integration**
  - [ ] Connect `SharePoint` list.
  - [ ] Connect `Office 365 Users`.
- [ ] **User Context**
  - [ ] Set `OnStart`: `Set(varCurrentUser, Office365Users.MyProfileV2())`.
- [ ] **Form Construction**
  - [ ] Create Combo Box for Supervisor: `Office365Users.SearchUser({searchTerm: Self.SearchText})`.
  - [ ] Bind Leave Inputs to SharePoint fields.
  - [ ] *Ref:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)

## Phase 3: Workflow Automation
- [ ] **Approval Flow**
  - [ ] Trigger: New SharePoint Item.
  - [ ] Action: Start Approval assigned to `SupervisorEmail`.
  - [ ] Action: Update Item Status based on outcome.
  - [ ] *Ref:* [ApprovalNotificationFlow.json](./PowerAutomate/ApprovalNotificationFlow.json)

## Phase 4: Deployment
- [ ] **Permissioning**
  - [ ] Grant "Contribute" access to the SharePoint list for all @hsgrabouw.co.za users.
- [ ] **App Launch**
  - [ ] Save and Publish version 1.0.
