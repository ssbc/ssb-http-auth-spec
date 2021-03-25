# Conditions

This specification makes clear assumptions about the setup involved peers authenticating.

**Server:** an SSB peer, known as the "server", **MUST** have an internet-public host address, **MUST** be accessible for secret-handshake connections under a multiserver address, and **MUST** support HTTP requests.

**Client:** another SSB peer, known as the "client", **MUST** be able to open a secret-handshake and muxrpc connection with the server. The user controlling this SSB peer also **SHOULD** control a web browser used to make requests to the server. The client's browser and operating system **SHOULD** support hyperlinks to [SSB URIs](https://github.com/ssb-ngi-pointer/ssb-uri-spec), redirecting them to SSB applications that recognize and parse SSB URIs. The client's SSB application employed during SSB HTTP Authentication **MUST** be able to recognize and parse SSB URIs.

**Connections:** the server and the client **SHOULD** recognize each other's SSB IDs as mutually trusted (such as a mutual follow relationship, or "membership" relationship where the client has claimed an invite token from the server). For the authentication protocol described in this document to succeed, the two SSB peers **MUST** be connected to each other via muxrpc and secret-handshake for the entire duration of the protocol. The purpose of SSB HTTP Authentication is to extend the trust that exists between these peers from the muxrpc context to the context of HTTP in the browser.
