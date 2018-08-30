# Introduction

Welcome to _Deneb_ API service. It is used by the
[Cygnus](https://github.com/stellar-fox/cygnus) client to provide augmented
services around [Stellar](https://stellar.org) _Account_.

We support cross-origin resource sharing, allowing you to interact securely
with our API from a client-side web application. Most of requests will require
a valid JSON Web Token ([JWT](https://https://jwt.io/)) in order to succeed.
There are however, some public open and throttled requests that we allow for
third party applications.

Currently we provide _Bash_ and _JavaScript_ language examples.
You can view code examples in the dark area to the right.

# Authentication

> You can verify token validity on the back-end with the following POST request:

```Bash
# Replace TOKEN with the actual JWT string.
curl "https://api.stellarfox.net/v1/auth/"
  -H "Content-Type: application/json"
  -d '{"token":"TOKEN"}'
```

```JavaScript
import Axios from "axios"

Axios.post("https://api.stellarfox.net/v1/auth/", {
  token: "your.jwt.string"
}).then(response => {
  // JWT token was successfuly verified.
}).catch(error => {
  // JWT token could not be verified or some other error occured.
})
```

> The above code should return JSON structured like this:

```json
{
  "uid": "userId",
}
```

_Deneb_ uses JWTs to allow access to the API. Those are created and managed
by the Firebase's __User__ object and validated on the server against their
claims and signature. JWT is created only if the __User__ object is valid. JWT
should be included in the JSON body or as a param string mapping to the key
`token`.

Most of the requests require `token`. In the side example you can `POST`
to the `auth` end point and check the validity of the JWT.

<aside class="notice">
You must replace <code>TOKEN</code> with actual content of JWT token returned
by the authenticated Firebase User object.
</aside>

# User

## Get User

```bash
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```bash
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve
