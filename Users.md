For access to the `/api/v2/users` endpoint you must be [Authenticated](Authentication.md).

#### GET `/api/v2/users/`

The index endpoint that returns all users for an account.

Example payload:

```
[
  {
    _id: 123,
    firstName: 'John',
    lastName: 'Doe',
    email: 'john@example.com',
    locale: 'en',
    timezone: 'UTC'
  },
  {
    _id: 321,
    firstName: 'Jane',
    lastName: 'Doe',
    email: 'jane@example.com',
    locale: 'fr',
    timezone: 'Europe/Paris'
  }
]
```

#### GET `/api/v2/users/:id`

The show endpoint for an individual user. It requires the ID of the user.

Example payload:

```
{
  _id: 123,
  firstName: 'John',
  lastName: 'Doe',
  email: 'john@example.com',
  locale: 'en',
  timezone: 'UTC'
}
```

#### POST `/api/v2/users`

Invite a new user with the given email address.

Parameters:

|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"email"|"test@example.com"|`String` - Required.|

Example payload:
```
{
  "email": "tester@phy.net"
}
```


`200` Response payload returns a success message.  Example:

```
{
  "error": false,
  "message": "User invited.",
  "statusCode": 200
}
```

#### PUT or PATCH `/api/v2/users/:id`

Update an existing `User` by `User` ID.

Arguments:

|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"firstName"|"John"|`String` - Optional.|
|"lastName"|"Doe"|`String` - Optional.|
|"email"|"test@example.com"|`String` - Optional.|
|"locale"|"en"|`String` - Optional. (`en`, `fr`, `da` or `de`)|
|"timezone"|"America/Chicago"|`String` - Optional.|

Example response:

```
{
  _id: 123,
  firstName: 'John',
  lastName: 'Doe',
  email: 'john@example.com',
  locale: 'en',
  timezone: 'UTC'
}
```

#### POST `/api/v2/users/:id/perms`

Update user permissions for an account.

Arguments:

|Parameter|Example|Notes|
|:---:|:---:|:---:|
|"accountManagement"|true|`Boolean` - Optional.|
|"userManagement"|true|`Boolean` - Optional.|
|"addBeacons"|true|`Boolean` - Optional.|
|"toggleBeacons"|true|`Boolean` - Optional.|
|"viewMetrics"|true|`Boolean` - Optional.|

Example response:

```
{
  accountManagement: false,
  userManagement: false,
  addBeacons: true,
  toggleBeacons: false,
  viewMetrics: true
}
```

#### POST `/api/v2/users/:id/activate`

Activate a user in an account.

Example response:

```
{
  "error": false,
  "message": "User activated",
  "statusCode": 200
}
```

#### POST `/api/v2/users/:id/deactivate`

Deactivate a user in an account.

Example response:

```
{
  "error": false,
  "message": "User deactivated",
  "statusCode": 200
}
```
