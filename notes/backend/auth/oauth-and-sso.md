# OAuth and SSO

> OAuth lets a third-party app act on a user's behalf with a short-lived, limited access token instead of the user's password. SSO (via OpenID or SAML) lets one login cover many apps.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 16–18)

## Key ideas
- **OAuth** lets **third-party apps access protected resources on behalf of a user**. Two apps communicate **without sharing the password**.
- **Actors:**
  - user (resource owner)
  - user agent (browser)
  - client app (the 3rd party)
  - authorization server
  - resource server (e.g. Google Calendar)
- The **authorization server** generates an **access token** that is:
  - short-lived
  - limited: it doesn't have the user's full capability
  - used only to act on the user's behalf
- It's a **bearer token**, sent in the request **header**.
- In **OAuth 2.0**, a **JWT** can be used to represent the access token.
- **Flows:**
  - **authorization code flow**: a user is involved and grants consent in the browser
  - **client credentials flow**: machine-to-machine, no user
- **SSO (Single Sign-On)** is built with **OpenID** or **SAML**.

## Example
"Scheduling app wants to add events to my Google Calendar":
```
1. App redirects me (browser) → Google authorization server
2. I log in at Google and approve "manage calendar events"
3. Auth server → app: authorization code → exchanged for access token
4. App → Google Calendar API
   Authorization: Bearer <access_token>
5. Token expires soon and only covers calendar scope.
   The app never saw my Google password.
```

## Pitfalls
- OAuth is about **delegated access**, not login itself. Identity on top of it comes from OpenID, which is the SSO side.
- A bearer token works for whoever holds it, so keep it short-lived and send it only over TLS.
- Don't request broader scopes than the app actually needs.

## Related
- [API authentication](api-authentication.md)
- [JWT authentication](jwt-authentication.md)
- [Session authentication](session-authentication.md)
