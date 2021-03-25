# Specification

A client known by its SSB ID `cid` is connected via secret-handshake and muxrpc to a server known by its SSB ID `sid`. The server is hosted at `serverHost`. A browser controlled by the same person or agent as the `cid` peer wishes to request an access-restricted resource (such as an admin dashboard) at the server over HTTP. All HTTP requests **MUST** be done with HTTPS.

The three sides (browser client, SSB client `cid`, and SSB server `sid`) perform a [challenge-response authentication](https://en.wikipedia.org/wiki/Challenge%E2%80%93response_authentication) protocol, specified as UML sequence diagrams. We use the shorthands `sc`, `cc`, and `sol` to mean:

- `sc`: "server's challenge"
- `cc`: "client's challenge"
- `sol`: "solution"

The challenges, `cc` and `sc`, are 256-bit [cryptographic nonces](https://en.wikipedia.org/wiki/Cryptographic_nonce) encoded in base64. The solution `sol` is a cryptographic signature using the cryptographic keypair `cid` that identifies the client, described below:

- `sid` is the servers's identity from their cryptographic keypair
- `cid` is the client's identity from their cryptographic keypair
- `sc` is a 256-bit nonce created by the server, encoded in base64
- `cc` is a 256-bit nonce created by the client, encoded in base64
- `sol` is the client's cryptographic signature of the string `=http-auth-sign-in:${sid}:${cid}:${sc}:${cc}` where `${x}` means string interpolation of the value `x`

Both sides generate the nonces, but there are use cases where one side should start first. In other words, the challenge-response protocol described here can be either **client-initiated** or **server-initiated**.

The HTTPS endpoints `/login`, `/sse/login/${sc}`, `/logout` **MAY** be employed as specified here, but are not strictly required for SSB HTTP Authentication to succeed. On the other hand, the muxrpc APIs `httpAuth.requestSolution(sc, cc)`, `httpAuth.sendSolution(sc, cc, cr)`, `httpAuth.invalidateAllSolutions()` and the SSB URI `ssb:experimental?action=start-http-auth&sid=${sid}&sc=${sc}` **MUST** be employed.

