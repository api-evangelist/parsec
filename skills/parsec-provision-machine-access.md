---
name: Provision and assign a team machine
description: Find a team machine and assign it to a member or group, with the ability to kick active users.
api: openapi/parsec-teams-openapi.yml
operations: [getTeamMachines, setTeamMachineAssignment, kickUserFromMachine]
---

# Provision and assign a team machine

## Auth
Send `Authorization: Bearer YOUR_API_KEY`. Requires **View Team Computers** to read
and **Manage Team Computers** to change assignments; **Team Machine Kick User** to
disconnect a user.

## Steps
1. **Find the machine** with `getTeamMachines`
   (`GET /v1/teams/{teamID}/machines`). Filter with `is_online`, `is_guest_access`,
   or `name` query params to narrow the result. Grab the `machineID`.
2. **Assign it** with `setTeamMachineAssignment`
   (`PUT /v1/teams/{teamID}/machines/{machineID}/assignment`) to a member, group, or
   reservation. (The older `createTeamMachineAssignment` POST is deprecated — use PUT.)
3. If a user must be disconnected, **kick** them with `kickUserFromMachine`
   (`DELETE /v1/teams/{teamID}/machines/{machineID}/users/{userID}`); they are
   disconnected immediately.

## Notes
- Deleting a machine (`deleteTeamMachine`) immediately invalidates its live session.
- Removing an assignment clears member, group, and reservation assignments.
