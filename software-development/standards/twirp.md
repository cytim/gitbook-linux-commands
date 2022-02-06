# Twirp

> Twirp is a framework for service-to-service communication emphasizing
> simplicity and minimalism. It generates routing and serialization from API
> definition files and lets you focus on your application's logic instead of
> thinking about folderol like HTTP methods and paths and JSON.
>
> Twirp is similar to [gRPC](http://www.grpc.io/), but without the custom HTTP
> server and transport implementations.
>
> \- [Twirp](https://github.com/twitchtv/twirp)

## What is RPC?

> RPC (Remote Procedure Call) is a request–response protocol. An RPC is
> initiated by the client, which sends a request message to a known remote
> server to execute a specified **procedure** with supplied **parameters**.
>
> \- [Wikipedia](https://en.wikipedia.org/wiki/Remote_procedure_call)

There are many RPC implementations - JSON-RPC, SOAP, gRPC, Twirp, etc.

## RPC vs REST

Both RPC and REST exist for client-server communication. The main difference is
that RPC focuses on "actions" while REST focuses on "resources".

Assume we are building a social media site. If Alice wants to
follow Bob for the news feed...

In RPC, we will define a `follow(user)` procedure that submit a "follow" request.

In REST, we will define a `POST /friendships` API to create a "friendship"
resource.

The difference sounds subtle but the ultimate solution will vary greatly using
the two approaches.

On one hand, the PRC approach is more standardised. The problem is that we can
easily get a bunch convoluted procedures when the application grows.

On the other hand, the REST approach supposes to be more scalable because
handling the resources should not involve complicated business logic
theoretically. However, there are many cases that it is hard to follow the REST
standard strictly.

## Twirp vs gRPC

Twirp is created by Twitch. gRPC is created by Google. They both serialize the
data as [protobuf](https://developers.google.com/protocol-buffers).

Twitch was using gRPC originally but they decided to develop Twirp because

1. gPRC only works with http/2 which is too new to have mature libraries; and
2. gRPC only works with protobuf which makes it hard for debugging.

Twirp is created to support both http/1.1 and http/2. It trades off some
runtime performance for a more stable ecosystem. Twirp also supports JSON
encoding that developers can test the API easily with cURL.
