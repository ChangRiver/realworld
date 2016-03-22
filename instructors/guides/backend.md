
# Backend Instructor Guide

# Setting up the Initial GitHub Repo

Create a GitHub repo for the students to clone to start off their app (rather
than starting from scratch). This ensures that the students will have a
consistent file structure for their application, as well as resolving any
dependencies up front. Be sure to lock-in any dependencies that may be fast-
changing or in beta so that the application will still work later down the road
when dependencies shift.

# Application Overview

Here is the list of features & subfeatures that make up the backend:

- Users
  - Login with Email/Password
  - Authenticated Requests using JWT Tokens
  - Following/Follower Support
  - Additional Fields (username, bio, image)
- Articles
  - Basic articles CRUD
  - Save a parameterized slug to be used as the identifier (downcase and replace punctuation/spaces with dashes)
  - Ability to favorite articles
  - Ability to fetch multiple articles and filter based on author, favorited by and tag
    - Accept a Limit/Offset query parameter for pagination
- Tags
  - Ability to add tags to Articles upon creation
  - Endpoint to fetch tags used in the application, with the most popular tags returned first
- Feed
  - Endpoint to fetch a list of articles for the current user that are written by the authors the user is following
    - Accept a Limit/Offset query parameter for pagination

# Endpoints & Implementation Details

See [API.md](https://github.com/GoThinkster/productionready/blob/master/API.md)
for exact parameters and expected results of each endpoint. All endpoints must
receive and return objects that are namespaced, so instead of returning
something like:

```
{
  "email":"hello@thinkster.io",
  "username":"thinkster"
}
```

the following is preferred:

```
{
  "user":{
    "email":"hello@thinkster.io",
    "username":"thinkster"
  }
}
```

This gives us the ability to add fields in the future for any addition features
or add-on courses.

Payloads returned and received by all endpoints must also be in lowerCamelCase
format. This lets our clients can stick with lowerCamelCase parameters when
when communicating with the backend, and gives them the ability to hot-swap
backends without worrying about what case the parameters should be.

The backend must run on port 3000, and should be as RESTful as possible. All
routes should begin with `/api`. We provide a postman file for testing the
endpoints.

The backend determines which user is logged in my checking the `Authorization`
header of the request. which should contain a JWT token. The header is in the
following format: `Token jwt.token.here`

Timestamps `createdAt` and `updatedAt` should automatically be generated
whenever a model is created or touched, and should be returned in ISO8601
format (2016-02-18T03:22:56.637Z).

## Error handling

When a request requires authentication and the JWT token is missing or invalid,
the backend should respond with the status code `401`.

When a request requires authentication and a valid token is provided, but the
user is not allowed to perform the operation (for example, attempting to edit
an article that doesn't belong to them), the backend should respond with the
status code `403`

When a request recieves missing or invalid parameters, the backend should
respond with the status code `422` and provide information about what went
wrong in the following format:

```
{
  "errors": {
    "username": [
      "can't be blank"
    ]
  }
}
```

The `errors` object should contain keys for every field of the request that
requires attention, and the value should always be an array so that you can
return multiple errors per field if necessary.

## Users & Authentication

Upon registration, be sure to check if the `username` and `email` have already
been taken.

Throughout the app there are two different types of user models returned, one
that's used for authentication (usually referred to as `user`) and private to
the current user, and the other that's public facing (usually referred to as
`profile`) that omits sensitive fields like `email`.

The JWT token needs to contain an `id` and `exp` field. `id` should be the
database identifier for the user, and `exp` should be Unix time in seconds,
set to 60 days in the future.

The [`/api/user`](https://github.com/GoThinkster/productionready/blob/master/API.md#get-current-user)
endpoint returns the current user's user object, which should contain a new JWT
token. This can be treated as a token refresh endpoint, and the client hits
this endpoint on hard page loads to verify the token is still valid.

## Profile

The profile is the public-facing user model, and used by the client to display
user profiles. By default, if the user hasn't set a profile picture yet, use the
![default profile image](//static.productionready.io/images/smiley-cyrus.jpg).

Users shouldn't be able to follow their own profiles

## Articles

Article slugs are titles that are downcased and have punctuation replaced with
dashes. They're used as identifiers on the client and should be globally unique.

`feed` is a reserved article title in order to avoid a route collision with
[`/api/articles/feed`](https://github.com/GoThinkster/productionready/blob/master/API.md#feed-articles)

The index endpoint [`/api/articles`](https://github.com/GoThinkster/productionready/blob/master/API.md#list-articles)
for articles should be able to handle three filters as query parameters:

Get articles favorited by user:

`?favorited=:username`

Get articles written by user:

`?author=:username`

Get articles tagged with tag:

`?tag=:tag`

By default the list of articles are limited to 20 results. The client can
should be able to provide `limit` and `offset` query parameters to fetch
additional results.

Tags should be deduplicated and case insensitive.

Articles should include a `favoritesCount` in the response, and shouldn't be
able to be favorited more than once per user.

## Tags

The tag endpoint [`/api/tags`](https://github.com/GoThinkster/productionready/blob/master/API.md#list-articles)
returns an array of tags sorted by popularity.
