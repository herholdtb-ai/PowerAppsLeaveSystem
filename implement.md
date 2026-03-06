# Implementation Checklist: Power Apps Leave Management System

## Phase 1: Data Backend (SharePoint)
- [ ] **Create SharePoint List**
    - [ ] Navigate to your SharePoint site.
    - [ ] Create a list named `LeaveRequests`.
- [ ] **Define Schema**
    - [ ] [ ] Add `Title` (Text, Required)
    - [ ] [ ] Add `CreatedBy` (Person, Required)
    - [ ] [ ] Add `CreatedDate` (Date/Time, Required)
    - [ ] [ ] Add `DueDate` (Date/Time, Optional)
    - [ ] [ ] Add `Status` (Choice: Open, In Progress, Closed)
    - [ ] *Reference:* [SharePointListSchema.json](./SharePoint/SharePointListSchema.json)

## Phase 2: Logic and Workflow (Power Automate)
- [ ] **Approval Workflow**
    - [ ] Create Business Process: `Leave Request Approval Flow`.
    - [ ] Configure steps: Request -> Manager Review -> HR Finalization.
    - [ ] *Reference:* [LeaveRequestApprovalFlow.json](./PowerAutomate/LeaveRequestApprovalFlow.json)
- [ ] **Balance Verification**
    - [ ] Create Manual Flow: `Leave Balance Check`.
    - [ ] Define input: `userId`.
    - [ ] *Reference:* [LeaveBalanceCheckFlow.json](./PowerAutomate/LeaveBalanceCheckFlow.json)
- [ ] **Notification System**
    - [ ] Create Automated Flow: `Approval Notification Workflow`.
    - [ ] Configure `SendApproval` to Manager and `Notify` to Requester.
    - [ ] *Reference:* [ApprovalNotificationFlow.json](./PowerAutomate/ApprovalNotificationFlow.json)

## Phase 3: Applications (Power Apps)
- [ ] **Employee Registration App**
    - [ ] Build form for First/Last Name, Email, and Department.
    - [ ] *Reference:* [EmployeeRegistrationApp.powerapps](./PowerApps/EmployeeRegistrationApp.powerapps)
- [ ] **Leave Request App**
    - [ ] Build submission form for Leave Type, Dates, and Reason.
    - [ ] Implement `submitLeaveRequest` function.
    - [ ] *Reference:* [LeaveRequestApp.powerapps](./PowerApps/LeaveRequestApp.powerapps)
- [ ] **Manager Dashboard**
    - [ ] Build dashboard with Performance Charts and Approve buttons.
    - [ ] *Reference:* [ManagerDashboardApp.powerapps](./PowerApps/ManagerDashboardApp.powerapps)
- [ ] **History Tracker**
    - [ ] Build log viewer for hiring/promotion history.
    - [ ] *Reference:* [EmployeeHistoryApp.powerapps](./PowerApps/EmployeeHistoryApp.powerapps)

## Phase 4: Integration
- [ ] **Data Connection**
    - [ ] Link all Apps to the `LeaveRequests` SharePoint list.
- [ ] **Validation**
    - [ ] Test end-to-end request submission and approval.
- [ ] **Deployment**
    - [ ] Share Apps and Flows with relevant organizational groups.
    - [ ] *Reference:* [Guide.md](./Guide.md)
