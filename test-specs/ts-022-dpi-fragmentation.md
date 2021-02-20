# Specification version number

2017-12-18-001

# Specification name

[XXX] DPI Detection Test?

# Test preconditions

  * An internet connection.
  * A URL we suspect is being blocked by a stateless/non-reassembling DPI box.

# Expected impact

  * If a URL is being blocked by DPI (not by IP or DNS blocking) into the TCP
    stream, we should be able to determine whether that DPI box reassembles
    streams or if it only looks at one packet at a time.

# Expected inputs
 bassosimone edited 23 days ago
% ./miniooni -i http://www.un.org/ urlgetter
[      0.000454] <info> miniooni home directory: $HOME/.miniooni
[      0.002826] <info> Looking up OONI backends; please be patient...
[      0.613004] <info> session: using probe services: {Address:https://ps2.ooni.io Type:https Front:}
[      0.613052] <info> Looking up your location; please be patient...
[      1.062837] <info> - country: IT
[      1.062869] <info> - network: Vodafone Italia S.p.A. (AS30722)
[      1.062879] <info> - resolver's IP: 91.80.36.85
[      1.062887] <info> - resolver's network: Vodafone Italia S.p.A. (AS30722)
[      1.062930] <info> [1/1] running with input: http://www.un.org/
[      1.406371] <warn> measurement failed: map[error:eof_error]
[      1.406422] <info> submitting measurement to OONI collector; please be patient...
[      1.504477] <info> New reportID: 20210119T133854Z_urlgetter_IT_30722_n1_KBFwIlfxPe0lfoUr
[      1.603306] <info> saving measurement to disk
[      1.604541] <info> experiment: recv 135  byte, sent 276  byte
[      1.605301] <info> sessionresolver: failure rate: primary: 0/3; fallback: 0/0
[      1.605573] <info> whole session: recv  10 kbyte, sent   7 kbyte


## Semantics

The test takes as input a list of URLs, one per line. For example:

    http://torproject.org
    https://ooni.nu

# Test description

For every hostname, we perform two HTTP connections--one with fragmentation
and one without--and compare them to see if the response differs. If the
input scheme is http, we fragment on the HTTP Host header; if the scheme
is https, we fragment on the SNI header in the TLS Client Hello.

# Expected output

## Parent data format

df-001-httpt [XXX?]

## Semantics

[XXX] I think there will be one boolean value for each URL input: whether
or not fragmenting around the plaintext hostname results in a different
HTTP response. Also, we will want to include the DNS requests
and responses, and the full HTTP requests and responses.

## Possible conclusions

Determing whether or not a censorship device reassembles TCP streams can
narrow down what type of technology is being used. For example, an HTTP
proxy like Squid has a stream-level view of the connection, while a DPI
box from Cisco probably does not reassemble lower-level packets into a
stream.

## Example output sample

```
{
}
```

# Privacy considerations

[XXX]
