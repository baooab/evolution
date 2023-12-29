# evolution

A note on the evolution of important versions of popular front-end libraries/frameworks.

## Express

### [5.0.0-alpha.1](https://github.com/expressjs/express/releases/tag/5.0.0-alpha.1)

> WARNING:This version was released in November 2014, but is [still in beta as of today](https://github.com/expressjs/express/tree/v5.0.0-beta.1).

remove:

- `app.del - use `app.delete`
- `req.acceptsCharset` - use `req.acceptsCharsets`
- `req.acceptsEncoding` - use `req.acceptsEncodings`
- `req.acceptsLanguage` - use `req.acceptsLanguages`
- `res.json(obj, status)` signature - use `res.json(status, obj)`
- `res.jsonp(obj, status)` signature - use `res.jsonp(status, obj)`
- `res.send(body, status)` signature - use `res.send(status, body)`
- `res.send(status)` signature - use `res.sendStatus(status)`
- `res.sendfile` - use `res.sendFile` instead
- `express.query` middleware

change:

- `req.host` now returns host (`hostname:port`) - use `req.hostname` for only hostname
- `req.query` is now a getter instead of a plain property

add:

- `app.router` is a reference to the base router

### [v4.17.0](https://github.com/expressjs/express/releases/tag/4.17.0)

- Add `express.raw` to parse bodies into `Buffer`
- Add `express.text` to parse bodies into string

### [v4.16.0](https://github.com/expressjs/express/releases/tag/4.16.0)

- Add `express.json` and `express.urlencoded` to parse bodies

### [v4.15.0](https://github.com/expressjs/express/releases/tag/4.15.0)

- Add `next("router")` to exit from router

