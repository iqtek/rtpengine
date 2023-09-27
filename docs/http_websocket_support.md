# HTTP/WebSocket support

If enabled in the config, *rtpengine* can handle requests made to it via HTTP,
HTTPS, or WebSocket (WS or WSS) connections. The supported HTTP URIs and
WebSocket subprotocols are described below.

## Dummy Test Interfaces

For HTTP and HTTPS, the URI `/ping` is provided, which simply responds with
`pong` if requested via `GET`. For WebSockets, the subprotocol
`echo.rtpengine.com` is provided, which simply echoes back any messages that
are sent to it.

## CLI Interface

This interface supports the same commands as the CLI tool `rtpengine-ctl` that
comes packaged with `rtpengine`. For HTTP and HTTPS, the command is appended to
the URI base `/cli/` and the request is made via `GET`, with spaces replaced by
plus signs as required by HTTP (e.g. `GET /cli/list+totals`). For WebSockets,
the subprotocol is `cli.rtpengine.com` and each WebSocket message corresponds
to one CLI command and produces one message in response. The format of each
response is exactly the same as produced by the CLI tool `rtpengine-ctl` and
therefore meant for plain text representation.

## *ng* Protocol Interface

This interface can be used to send and receive *ng* protocol messages over HTTP
or WebSocket connections instead of plain UDP.

For HTTP and HTTPS, the URI `/ng` is used, with the request being made by
`POST` and the content-type set to `application/x-rtpengine-ng`. The message
body must be in the same format as the body of an UDP-based *ng* message and
must therefore consist of a unique cookie string, followed by a single space,
followed by the message in *bencode* format. Likewise, the response will be in
the same format, including the unique cookie.

For WebSockets, the subprotocol `ng.rtpengine.com` is used and the protocol
follows the same format. Messages must consist of a unique cookie and a string
in bencode format, and responses will also be in the same format.

## Prometheus Stats Exporter

The Prometheus metrics can be found under the URI `/metrics`.
