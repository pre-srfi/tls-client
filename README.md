# SRFI nnn: TLS client

by Firstname Lastname, Another Person, Third Person

# Status

Early Draft

# Abstract

This SRFI lets users make connections to Transport Layer Security
(TLS) servers. A TLS connection is essentially a bidirectional,
encrypted pipe over which arbitrary binary data can be sent. TLS was
formerly known as Secure Sockets Layer (SSL).

# Issues

One crucial requirement for such an API is to provide a way to do
server certificate verification, or to specify how it should be done
by the underlying software. Clients that don't check servers'
certificates are surprisingly common, and put their users at risk. I
encountered another such unfixed project just yesterday.

Another requirement is to allow control of exactly what crypto
algorithms and TLS/SSL versions will be accepted. There are well-known
vulnerabilities in earlier versions, and it's important that users who
want to can avoid accepting connections using those versions.

Ideally, the API should support sending client certificates.

# Rationale

## Survey of TLS implementations in C

* [OpenSSL](https://www.openssl.org) /
  [LibreSSL](https://www.libressl.org) /
  [BoringSSL](https://github.com/google/boringssl)

* [Mbed TLS](https://github.com/ARMmbed/mbedtls)

* [axTLS](http://axtls.sourceforge.net/)

* [GnuTLS](https://www.gnu.org/software/gnutls/)

* [WolfSSL](https://www.wolfssl.com/)

* [Google Tink](https://github.com/google/tink)

* [Amazon s2n](https://github.com/awslabs/s2n)

* [Mozilla Network Security Services (NSS)](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS)

* [Microsoft Secure Channel (Schannel)](https://docs.microsoft.com/en-us/windows/win32/secauthn/secure-channel)

* [Apple Secure Transport](https://developer.apple.com/documentation/security/secure_transport)

## Survey of TLS implementations in Java/C#

* [Bouncy Castle](https://bouncycastle.org/)

* [Java Secure Socket Extension (JSSE)](https://docs.oracle.com/javase/9/security/java-secure-socket-extension-jsse-reference-guide.htm)

## Survey of existing Scheme TLS interfaces

* Chibi-Scheme -- `(chibi ssl)` -- Basic bindings for establishing SSL connections -- http://snow-fort.org/s/gmail.com/alexshinn/chibi/ssl/0.1/

* Chicken -- `openssl` -- Bindings to the OpenSSL SSL/TLS library -- https://wiki.call-cc.org/eggref/5/openssl

* Chicken -- `TerribleTLS` -- Inadvisible pure-Scheme TLS client -- https://akkuscm.org/packages/TerribleTLS/

* Gambit -- (make-tls-context [options]) http://www.iro.umontreal.ca/~gambit/doc/gambit.html#Network-devices

* Gauche

* Guile -- `gnutls`

# Specification

## Get information

(**tls-implementation-name**) -> string

(**tls-implementation-version**) -> string

(**tls-version-list**) -> string list

Return a list of all TLS/SSL versions supported by the implementation.

Sorted from older to newer. [What does this mean precisely?]

(**tls-cipher-list**) -> string list

Returns a list of all cipher algorithms supported by the
implementation.

## Open connection

(**tls-open** _host_ _port_ _options_) -> port

Recognizes at least the following options:

**allowed-ip-versions** `4` or `6`

Whether to allow connections over IPv4, IPv6, or either. Default is
either.

**allowed-tls-versions** string list

`'("1.3")`

**allowed-tls-chipers** string list

**network-interface** string

**check-remote-certificate** `#t` or `#f`

**check-remote-certificate-stapling** `#t` or `#f`

# Implementation

# Acknowledgements

Arthur Gleckler suggested the features to send client certificates,
force server certificate verification, and select algorithms and TLS
versions.

The SSL options were inspired by the `curl` program.

# References

# Copyright

Copyright (C) Firstname Lastname (20XY).

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
