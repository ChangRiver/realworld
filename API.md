# ProductionReady API Spec

### Authentication Header:

`Authorization: Token jwt.token.here`

## JSON Objects returned by API:

### Users (for authentication)

```
{
  "user": {
    "username": "jake",
    "email": "jake@jake.jake",
    "token": "jwt.token.here"
  }
}
```

### Profile

```
{
  "profile": {
    "username": "jake",
    "bio": "I work at statefarm",
    "image": "https://i.stack.imgur.com/xHWG8.jpg",
    "following": false
  }
}
```

### Single Article

```
{
  "article": {
    "slug": "how-to-train-your-dragon",
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "It takes a Jacobian",
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0
  }
}
```

### Multiple Articles

```
{
  "articles":[{
    "description": "Ever wonder how?",
    "slug": "how-to-train-your-dragon",
    "title": "How to train your dragon",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0
  }, {
    "description": "So toothless",
    "slug": "how-to-train-your-dragon-2",
    "title": "How to train your dragon 2",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z",
    "favorited": false,
    "favoritesCount": 0
  }],
  "articlesCount": 2
}
```

### Single comment

```
{
  "comment": {
    "body": "It takes a Jacobian",
    "createdAt": "2016-02-18T03:22:56.637Z",
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }
}
```

### Multiple comments

```
{
  "comments": [{
    "body": "It takes a Jacobian",
    "createdAt": "2016-02-18T03:22:56.637Z",
    "author": {
      "username": "jake",
      "bio": "I work at statefarm",
      "image": "https://i.stack.imgur.com/xHWG8.jpg",
      "following": false
    }
  }]
}
```


## Endpoints:

### Authentication:

`POST /api/users/login`

Example request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```
No authentication required, returns a [User](#users-for-authentication)



### Registration:

`POST /api/users`

Example request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```

No authentication required, returns a [User](#users-for-authentication)



### Get Current User

`GET /api/user`

Authentication required, returns a [User](#users-for-authentication) that's the current user



### Update User

`PUT /api/user`

Example request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "bio": "I like to skateboard",
    "image": "https://i.stack.imgur.com/xHWG8.jpg"
  }
}
```

Authentication required, returns the [User](#users-for-authentication)



### Get Profile

`GET /api/profiles/:username`

Authentication optional, returns a [Profile](#profile)



### Follow user

`POST /api/profiles/:username/follow`

Authentication required, returns a [Profile](#profile)



### Unfollow user

`DELETE /api/profiles/:username/follow`

Authentication required, returns a [Profile](#profile)



### List Articles

`GET /api/articles`

Returns most recent articles globally be default, provide `tag`, `author` or `favorited` query parameter to filter results

Query Parameters:

Filter by tag:

`?tag=AngularJS`

Filter by author:

`?author=jake`

Favorited by user:

`?favorited=jake`

Limit number of articles (default is 20):

`?limit=20`

Offset/skip number of articles:

`?offset=0`

Authentication optional, will return [multiple articles](#multiple-articles), ordered by most recent first



### Feed articles

`GET /api/articles/feed`

Can also take `limit` and `offset` query parameters like [List Articles](#list-articles)

Authentication required, will return [multiple articles](#multiple-articles) created by followed users, ordered by most recent first.



### Create Article

`POST /api/articles`

Example request body:

```
{
  "article": {
    "title": "How to train your dragon",
    "description": "Ever wonder how?",
    "body": "You have to believe",
    "tagList": ['reactjs', 'angularjs', 'dragons']
  }
}
```

Authentication required, will return an [Article](#single-article)



### Update article

`PUT /api/articles/:slug`

Example request body:

```
{
  "article": {
    "title": "Did you train your dragon?"
  }
}
```

Authentication required, returns the updated [Article](#single-article)



### Adding comments to an article

`POST /api/articles/:slug/comments`

Example request body:

```
{
  "comment": {
    "body": "His name was my name too."
  }
}
```

Authentication required, returns the created [Comment](#single-comment)



### Getting comments to an article

`GET /api/articles/:slug/comments`

Authentication optional, returns [multiple comments](#multiple-comments)




### Favoriting an article

`POST /api/articles/:slug/favorite`

Authentication required, returns the [Article](#single-article)



### Unfavoriting an article

`DELETE /api/articles/:slug/favorite`

Authentication required, returns the [Article](#single-article)
