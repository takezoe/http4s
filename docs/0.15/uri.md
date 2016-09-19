---
layout: default
title: URI handling
---

## Literals

http4s is a bit more strict with handling URIs than e.g. the [play http client].
Instead of passing plain `String`s, http4s operates on URIs. You can construct
literal URI with

```scala
import org.http4s._
// import org.http4s._

val uri = Uri.uri("http://http4s.org")
// uri: org.http4s.Uri = http://http4s.org
```

## Building URIs

Naturally, that's not enough if you want dynamic URIs. There's a few different
ways to build URIs, you can either use a predefined URI and call methods on it,
or you could use the URLTemplates.

### URI

Use the methods on the [uri class].

```scala
val docs = uri.withPath("/docs/0.15/")
// docs: org.http4s.Uri = http://http4s.org/docs/0.15/
```

### URI Template

```scala
import org.http4s.util.CaseInsensitiveString.ToCaseInsensitiveStringSyntax
// import org.http4s.util.CaseInsensitiveString.ToCaseInsensitiveStringSyntax

import org.http4s.UriTemplate._
// import org.http4s.UriTemplate._

val template = UriTemplate(
  authority = Some(Uri.Authority(host = Uri.RegName("http4s.org"))),
  scheme = Some("http".ci),
  path = List(PathElm("docs"), PathElm("0.15"))
)
// template: org.http4s.UriTemplate = http://http4s.org/docs/0.15

template.toUriIfPossible
// res0: scala.util.Try[org.http4s.Uri] = Success(http://http4s.org/docs/0.15)
```

[play http client]: https://www.playframework.com/documentation/2.5.x/api/scala/index.html#play.api.libs.ws.WS$
[uri class]: http://http4s.org/api/0.15/#org.http4s.Uri