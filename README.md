# requester-headers for OTOBO

`requester-headers` is a package for OTOBO which makes it possible
to send custom request headers when using the GenericInterface
to send HTTP requests using `Kernel::GenericInterface::Transport::HTTP::REST`
and `Kernel::GenericInterface::Requester`.

It works similar to the support for custom headers in the
implementation of `Kernel::GenericInterface::Transport::HTTP::REST`
for `Kernel::GenericInterface::Provider`: It reads the appropriate
`TransportConfig` of the used webservice, takes the `AdditionalHeaders`
field and appends its key value pairs as headers.

Specifically it doesn't support the following things which may be
interesting to implement in the future:

* Interactive configuration via `AdminGenericInterfaceWebservice`
  (i. e. the OTOBO admin interface)
* Custom headers per request (currently the configured headers are
  used globally for the respective webservice)

This package exists mostly as an intermediate solution: Upstream has
implemented [an equivalent change][custom-headers], but it won't
be included in an OTOBO version before 10.1. We don't reuse upstream's
patch for historical reasons: Originally this was implemented for
OTRS 6 and we keep its API intact in order to not break
[`otobo-rocketchat`](../otobo-rocketchat).

Once OTOBO 10.1 is released, we'll be able to adjust `otobo-rocketchat`
and retire this package.

The alternative `REST.pm` file supplied by this package is based on
our [OTOBO fork][fork].

## Changes

### 0.2.0 2020-04-30

Port to OTOBO.

### 0.1.0 2020-09-03

Initial release.

Reads `AdditionalHeaders` and adds them to every request.

[fork]: https://git.rz.uni-augsburg.de/itinfo-h/otobo/tree/requester-headers
[custom-headers]: https://github.com/RotherOSS/otobo/commit/df2e584ba1cc0a524d2f5094851a40f380300c2f
