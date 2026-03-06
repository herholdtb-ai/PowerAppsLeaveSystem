# Implementation Checklist: Power Leave (Two-Stage Approval)

## Phase 1: SharePoint Data Layer
- [ ] **Create List**
  - [ ] Name: `LeaveRequests`
- [ ] **Configure Columns**
  - [ ] [ ] `LeaveReason` (Default Title field renamed)
  - [ ] [ ] `RequesterEmail` (Single line text)
  - [ ] [ ] `SupervisorEmail` (Single line text)
  - [ ] [ ] `StartDate` (Date only)
  - [ ] [ ] `EndDate` (Date only)
  - [ ] [ ] `ReasonDetails` (Multiline text, Plain text)
  - [ ] [ ] `OverallStatus` (Choice: Awaiting Support, Awaiting Principal, Approved, Rejected, Not Supported)
  - [ ] *Ref:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Power App Development
- [ ] **Connectors**
  - [ ] Add `SharePoint` (LeaveRequests list).
  - [ ] Add `Office 365 Users`.
- [ ] **Initial Setup**
  - [ ] Set `App.OnStart`: `Set(varCurrentUser, Office365Users.MyProfileV2())`.
- [ ] **Build UI Controls**
  - [ ] [ ] Header Label: `"User: " & varCurrentUser.displayName`.
  - [ ] [ ] Supervisor Combo Box: `Office365Users.SearchUser({searchTerm: Self.SearchText})`.
  - [ ] [ ] Text Input (Multi-line): `txtReason`.
- [ ] **Submission Formula**
  - [ ] Button `OnSelect`: Paste `Patch` function setting `OverallStatus` to "Awaiting Support".
  - [ ] *Ref:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)

## Phase 3: Automated Workflow Logic
- [ ] **Trigger**
  - [ ] SharePoint: `When an item is created`.
- [ ] **Branching Logic**
  - [ ] Condition: `SupervisorEmail` equals `bezuidenhouth@hsgrabouw.co.za`.
- [ ] **Stage 1 (Supervisor)**
  - [ ] Start Approval: Response options "Support" / "Not-Support".
  - [ ] Update SharePoint Status to "Awaiting Principal" if supported.
- [ ] **Stage 2 (Principal)**
  - [ ] Start Approval: "Approve" / "Reject" assigned to `bezuidenhouth@hsgrabouw.co.za`.
  - [ ] Update final Status based on response.
  - [ ] *Ref:* [LeaveRequestApprovalFlow.json](./PowerAutomate/LeaveRequestApprovalFlow.json)

## Phase 4: Finalization
- [ ] **Permissions**
  - [ ] Ensure all staff have "Contribute" access to the SharePoint list.
- [ ] **Publication**
  - [ ] Save and Publish App v1.0.
