---
title: "REST API Design"
draft: true
---

```
GET - get resource
POST - create resource
PUT - either creates or replaces the resouce if it doesn't exist
PATCH - update partially
DELETE - delete resource
```

Use Nouns not Verbs.

HTTP Methods are already verbs.

```
// no
GET https://site.com/api/v1/getPosts

// yes
GET https://site.com/api/v1/posts
```

Name resources with plural nouns. Not a hard rule but prefer.

```
/api/v1/users/{id} over /api/v1/user/{id}
```

Use nesting to show relationship

```
/api/v1/posts/author
```

HTTP code ranges

```
2xx - Sucess
3xx - Resource has moved
4xx - Client side error
5xx - Server side error
```

Return and recieve JSON data type over XML.

Url parameter types:  
**query parameters** = `/users?age=29&location=us`  
**path parameter** = `/users/{id} /users/:id`

Use query strings for complex parameters.

-   Pagination
-   Sorting
-   Filtering
-   Limits
-   Start
-   File extensions

`/users?location=us&sort=-age&active=true`

Avoid underscores in url since they can look like links so use dash instead.

Use lowercase for urls.

`/posts/author` over `/Posts/Author`

Cache data for performance.

Version your API.

```
/api/v1/
/api/v1.0/
/api/v1.0.0/
```

No sensitive information in the url.  
Restrict method execution for routes.  
Validate incoming data from query, params, and malformed JSON.  
Give generic error messages. Don't give attackers more information then they need.  
But give enough information for end users to fix their errors.  
Authentication and Authorization. Cookies, Server Sessions, JWT, OAuth, OAuth2.
