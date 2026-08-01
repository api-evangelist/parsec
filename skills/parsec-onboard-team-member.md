---
name: Invite and organize a team member
description: Invite a new member to a Parsec team and place them into the right group.
api: openapi/parsec-teams-openapi.yml
operations: [createTeamInvites, getTeamMembers, getTeamGroups, assignTeamGroupMembers]
---

# Invite and organize a team member

Use the Parsec for Teams API to invite a person to a team and assign them to a group.

## Auth
Every request sends `Authorization: Bearer YOUR_API_KEY`. The key's team role must
hold the required permission (e.g. **Create Team Invites**, **View Groups**) or the
endpoint returns `403`.

## Steps
1. **List groups** with `getTeamGroups` (`GET /v1/teams/{teamID}/groups`) to find the
   target group's `groupID`. Requires the *View Groups* permission.
2. **Create the invite** with `createTeamInvites`
   (`POST /v1/teams/{teamID}/member-invites`), supplying the member `email`,
   optional `team_group_id`, and `is_admin`. This endpoint is rate limited to
   **50 requests / 5 minutes** — batch invites and back off on `429`.
3. Once the member accepts, **confirm** they appear via `getTeamMembers`
   (`GET /v1/teams/{teamID}/members`).
4. If they need to move groups, **assign** them with `assignTeamGroupMembers`
   (`POST /v1/teams/{teamID}/groups/{groupID}/add-members`).

## Notes
- Pagination on list endpoints is offset/limit.
- Removing a member (`removeTeamMember`) unassigns their team machines.
