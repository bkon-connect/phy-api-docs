For access to the API, users must either:

### Login via Web Client `/login`

Login via the web client and have a cookie-based session running. Note: this will mainly be for internal usage for building out SPA-style pages and accessing payloads via AJAX in React.

Examples:

a) If a user has logged in via web client, then that user's client, via session cookie, can access the endpoints.

b) Alternatively, any client that supports cookie sessions can also log in. An example via `curl` is:

```
$ curl -H "Accept: application/json" \
-H "Content-Type: application/json" \
-X POST \
-d '{"email": "<your email>", "password": "<your password>"}' \
--cookie-jar ./cookies.txt \ ## example of saving a cookie
https://my.phy.net/login
```

### Login via JWT `/api/v2/login`

`POST`ing to `/api/login` a payload of `{"email": "<your email>", "password": "<your password>"}`.  It must pass the headers `Content-Type: application/json` and `Accept: application/json`.  Upon doing so you'll receive a JWT token that must be passed up as a header in the form of `Authorization: BEARER <token>`

An example of a request to authenticate would look like:

```
$ curl -H "Accept: application/json" \
-H "Content-Type: application/json" \
-X POST \
-d '{"email":"testing.demo@phy.net", "password":"testing.demo"}' \
https://my.phy.net/api/v2/login
```

Note: Although this is via `curl`, inside of React apps, you would simply use `superagent` to just `request` a `POST` to these endpoints.  As an internal developer, you will just allow them to log in as they normally do - the JWT endpoints exist for external developers / users.
