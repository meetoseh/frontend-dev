# frontend-dev

This project is a technical detail that when we want to develop the app locally,
we need to connect over https if we want to use even a development oauth 2.0
app. This can be accomplished with a custom dns (e.g., dnsmasq, and for windows,
sudppipe to forward udp 53 to wsl 2), a custom root CA (using mkcert), installing
that CA on the phones user certificates, and configuring the app to allow user
trusted certificate authorities.

However, even after all that, google will reject the requests with the following
message:

```json
{
  "error": "invalid_request",
  "error_description": "\nYou can\u0026#39;t sign in to this app because it doesn\u0026#39;t comply with Google\u0026#39;s OAuth 2.0 policy for keeping apps secure.\n\nYou can let the app developer know that this app doesn\u0026#39;t comply with one or more Google validation rules.\n  "
}
```

To fix this, we need to actually register the domain, prove to Google we own
teh domain, _actually put something on the domain_, and finally it should
allow requests through.

This contains the contents of the domain, which is just a basic html file to
satisfy google that we have setup https correctly.

This is hosted on aws amplify using drag + drop hosting.
