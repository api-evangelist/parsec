---
name: Issue time-limited guest access
description: Grant an external guest temporary access to a Parsec host machine and revoke it on demand.
api: openapi/parsec-teams-openapi.yml
operations: [getGuestAccessInviteCredits, createGuestAccessInvite, getGuestAccessInvites, kickGuestAccessGuest]
---

# Issue time-limited guest access

## Auth
Send `Authorization: Bearer YOUR_API_KEY`. Requires **View Guest Access Links** to
read guest invites.

## Steps
1. **Check credits** with `getGuestAccessInviteCredits`
   (`GET /v1/teams/{teamID}/guest-access-invite-credits`) — guest invites consume
   team credits.
2. **Create the invite** with `createGuestAccessInvite`
   (`POST /v1/teams/{teamID}/guest-access-invites`), defining the valid start/expiry
   window and the target machine.
3. **List / audit** outstanding invites with `getGuestAccessInvites`
   (`GET /v1/teams/{teamID}/guest-access-invites`).
4. To end a session immediately, **kick** the guest with `kickGuestAccessGuest`
   (`DELETE /v1/teams/{teamID}/guest-access-invites/{guestAccessInviteID}/guest`).
   If the invite is still within its valid window the guest can reconnect; to stop
   that, cancel the invite entirely with `cancelGuestAccessInvite`.
