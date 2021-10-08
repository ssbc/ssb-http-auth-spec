<!--
SPDX-FileCopyrightText: 2021 Andre 'Staltz' Medeiros

SPDX-License-Identifier: CC-BY-4.0
-->

## Sign-out

An optional (but recommended) muxrpc API `httpAuth.invalidateAllSolutions` on the server to allow the SSB peer to invalidate *all* auth tokens associated with the `cid`. See UML sequence diagram:

```mermaid
sequenceDiagram
  participant Umux as SSB client `cid`
  participant Uweb as Browser client
  participant Serv as SSB server `sid`

  Umux->>+Serv: (muxrpc async) `httpAuth.invalidateAllSolutions()`
  Note over Serv: Invalidates every `sc`<br/>and `authtoken` associated<br/>with `cid`
  Serv-->>-Umux: respond httpAuth.invalidateAllSolutions with `true`
  Note over Uweb,Serv: Potentially thereafter...
  Uweb->>+Serv: Authenticate using `authtoken`
  Serv-->>-Uweb: HTTP 401
```

The browser client also has the option of signing out with HTTP endpoints. This does not require a muxrpc call with the SSB peer. See UML sequence diagram:

```mermaid
sequenceDiagram
  participant Uweb as Browser client
  participant Serv as SSB server `sid`

  Uweb->>+Serv: Some URL on the `serverHost`
  Note over Serv: Invalidates `authtoken`
  Serv-->>-Uweb: HTTP 200
  Note over Uweb,Serv: Potentially thereafter...
  Uweb->>+Serv: Authenticate using `authtoken`
  Serv-->>-Uweb: HTTP 401
```
