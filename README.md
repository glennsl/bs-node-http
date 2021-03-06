# bs-node-http

Node `http` bindings for
[Bucklescript](https://github.com/BuckleScript/bucklescript) in
[Reason](https://github.com/facebook/reason)

## Status
Obligatory "this is just a WIP" section. Feel free to pull down and extend
the API and/or make it better ... I don't pretend to be a ReasonML wizard.

I will be accepting PR's. Node HTTP is one of my most used modules and I'm
surprised this wasn't done yet. A good alternative, though, is the
[bs-express](https://github.com/reasonml-community/bs-express) project if
you are after routing as well.

## Installation

Install `bs-node-http` from npm. `npm i -S bs-node-http`.

Then, add `bs-node-http` to yor `bs-dependencies` in your `bsconfig.json`.

```json
{
  "bs-dependencies": ["bs-node-http"]
}
```

## Usage

The api is modified to favour piping the response so doesn't map 1 to 1 with
the Node API. It's very minimal at the moment - if what you want isn't added
feel free to add a binding in `src/NodeHTTP.re` then implement the API in
`src/Http.re`

```reasonml
open Http;

let handler = (~request as _, ~response) =>
  response
  |> Response.setStatusCode(200)
  |> Response.setHeader("X-some-fancy-header", "hederz 4 dayz")
  |> Response.write("Foo")
  |> Response.write("Bar")
  |> Response.close;

let server = create_server(handler) |> Server.listen(~port=3000);
```