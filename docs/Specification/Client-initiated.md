## Client-initiated protocol

In the client-initiated variant of the challenge-response protocol, the first step is the client creating `cc` and opening a web page in the browser. Then, the server attending to that HTTP request will call `httpAuth.requestSolution(sc, cc)` on the client SSB peer.

The UML sequence diagram for the whole client-initial protocol is shown below:

```mermaid
sequenceDiagram
  participant Umux as SSB client `cid`
  participant Uweb as Browser client
  participant Serv as SSB server `sid`

  note over Umux: Generates<br/>challenge `cc`
  Umux->>Uweb: `https://${serverHost}/login<br/>?ssb-http-auth=1cid=${cid}&cc=${cc}`
  Uweb->>+Serv: `https://${serverHost}/login<br/>?ssb-http-auth=1cid=${cid}&cc=${cc}`
  Note over Serv: Generates<br/>challenge `sc`
  alt client is disconnected from the server
    Serv-->>Uweb: HTTP 403
  else client is connected to the server
    Serv->>+Umux: (muxrpc async) `httpAuth.requestSolution(sc, cc)`
    Note over Umux: Generates<br/>signature `sol`
    Umux-->>-Serv: respond httpAuth.requestSolution with `sol`
    alt `sol` is incorrect
      Serv-->>Uweb: HTTP 403
    else `sol` is correct
      Serv-->>-Uweb: HTTP 200, auth token
      Note over Uweb: Stores auth token as a cookie
    end
  end
```
