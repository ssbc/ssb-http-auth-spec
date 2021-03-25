# Security considerations

## Client consent

Because the sign-in process is seemless and happens in the background via muxrpc, without any input from the user who controls the client SSB peer, there is potential for vulnerabilities if the SSB URI is manipulated or the URL is manipulated.

SSB applications that control the client SSB peer therefore MUST prompt user consent before `httpAuth.requestSolution` or `httpAuth.sendSolution` are sent. The prompt SHOULD display the server's SSB ID and ask the user to confirm their intent to sign-in.

## Client impersonation

To be done.

## Tokens

To be done.