# Implementation Checklist: Power Leave (Two-Stage Approval)

## Phase 1: SharePoint Setup
- [ ] **Create List**
  - [ ] Name: `LeaveRequests`
- [ ] **Configure Columns**
  - [ ] `LeaveReason` (Renamed Title)
  - [ ] `RequesterEmail` (Single line text)
  - [ ] `SupervisorEmail` (Single line text)
  - [ ] `StartDate` (Date)
  - [ ] `EndDate` (Date)
  - [ ] `ReasonDetails` (Multiline text, Plain)
  - [ ] `OverallStatus` (Choice: Awaiting Support, Awaiting Principal, Approved, Rejected, Not Supported)
  - [ ] *Ref:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Power App Development
- [ ] **Data Connectors**
  - [ ] Connect `SharePoint` & `Office 365 Users`.
- [ ] **App Logic**
  - [ ] `App.OnStart`: `Set(varCurrentUser, Office365Users.MyProfileV2())`.
- [ ] **Build UI**
  - [ ] Supervisor Combo Box: `Office365Users.SearchUser({searchTerm: Self.SearchText})`.
  - [ ] Date Pickers for Start/End.
  - [ ] Text Input for ReasonDetails.
- [ ] **Submit Logic**
  - [ ] Patch code setting `OverallStatus` to "Awaiting Support".
  - [ ] *Ref:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)

## Phase 3: Workflow Automation
- [ ] **Shortcut Check**
  - [ ] Condition: If `SupervisorEmail` == `bezuidenhouth@hsgrabouw.co.za`.
- [ ] **Supervisor Stage**
  - [ ] Action: Approval with custom responses "Support" / "Not-Support".
  - [ ] Update status to "Awaiting Principal" on Support.
- [ ] **Principal Stage**
  - [ ] Action: Approve/Reject assigned to `bezuidenhouth@hsgrabouw.co.za`.
  - [ ] Update final status based on result.
  - [ ] *Ref:* [LeaveRequestApprovalFlow.json](./PowerAutomate/LeaveRequestApprovalFlow.json)

## Phase 4: Finalization
- [ ] **Permissions**
  - [ ] Grant "Contribute" access to staff for SharePoint List.
- [ ] **Launch**
  - [ ] Publish App v1.0.
