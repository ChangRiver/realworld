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
    "updatedAt": "2016-02-18T03:48:35.824Z"
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
    "updatedAt": "2016-02-18T03:48:35.824Z"
  }, {
    "description": "So toothless",
    "slug": "how-to-train-your-dragon-2",
    "title": "How to train your dragon 2",
    "tagList": ["dragons", "training"],
    "createdAt": "2016-02-18T03:22:56.637Z",
    "updatedAt": "2016-02-18T03:48:35.824Z"
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

Request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```
No authentication required, returns a User object



### Registration:

`POST /api/users`

Request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```

No authentication required, returns a User object



### Get Current User

`GET /api/user`

Authentication required, returns a User object for the current user



### Update User

`PUT /api/user`

Request body:
```
{
  "user":{
    "email": "jake@jake.jake",
    "bio": "I like to skateboard",
    "image": "https://i.stack.imgur.com/xHWG8.jpg"
  }
}
```

Authentication required, returns a User object



### Get Profile

`GET /api/profiles/:username`

Authentication optional, returns a profile object



### Follow user

`POST /api/profiles/:username/follow`

Authentication required, returns profile object



### Unfollow user

`DELETE /api/profiles/:username/follow`

Authentication required, returns profile object



### List Articles

`GET /api/articles`

Authentication optional, will return array of articles most recent first

Use to get all articles globally, provide tag or author query param to filter

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



### Feed articles

`GET /api/articles/feed`

Can also take `limit` and `offset` query parameters like [List Articles](https://github.com/GoThinkster/productionready/blob/master/API.md#list-articles)

Authentication required, will return array of articles more recent first created by followed users



### Create Article

`POST /api/articles`

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

Authentication required, will return article object



### Update article

`PUT /api/articles/:slug`

```
{
  "article": {
    "title": "Did you train your dragon?"
  }
}
```

Authentication required, will return article object



### Adding comments to an article

`POST /api/articles/:slug/comments`

```
{
  "comment": {
    "body": "His name was my name too."
  }
}
```

Authentication required, returns the created comment object



### Getting comments to an article

`GET /api/articles/:slug/comments`

Authentication optional, returns multiple comments




### Favoriting an article

`POST /api/articles/:slug/favorite`

Authentication required



### Unfavoriting an article

`DELETE /api/articles/:slug/favorite`

Authentication required
