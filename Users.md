For access to the `/api/v2/users` endpoint you must be [Authenticated](https://github.com/bkon-connect/phy-api-docs/wiki/Authentication).

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
<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"email"</td>
    <td>"test@example.com"</td>
    <td>`String` - Required.</td>
  </tr>
</table>

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

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"firstName"</td>
    <td>"John"</td>
    <td>`String` - Optional.</td>
  </tr>
  <tr>
    <td>"lastName"</td>
    <td>"Doe"</td>
    <td>`String` - Optional.</td>
  </tr>
  <tr>
    <td>"email"</td>
    <td>"test@example.com"</td>
    <td>`String` - Optional.</td>
  </tr>
  <tr>
    <td>"locale"</td>
    <td>"en"</td>
    <td>`String` - Optional. (`en`, `fr`, `da` or `de`)</td>
  </tr>
  <tr>
    <td>"timezone"</td>
    <td>"America/Chicago"</td>
    <td>`String` - Optional.</td>
  </tr>
</table>

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

<table>
  <tr>
    <th>Parameter</th>
    <th>Example</th>
    <th>Notes</th>
  </tr>
  <tr>
    <td>"accountManagement"</td>
    <td>true</td>
    <td>`Boolean` - Optional.</td>
  </tr>
  <tr>
    <td>"userManagement"</td>
    <td>true</td>
    <td>`Boolean` - Optional.</td>
  </tr>
  <tr>
    <td>"addBeacons"</td>
    <td>true</td>
    <td>`Boolean` - Optional.</td>
  </tr>
  <tr>
    <td>"toggleBeacons"</td>
    <td>true</td>
    <td>`Boolean` - Optional.</td>
  </tr>
  <tr>
    <td>"viewMetrics"</td>
    <td>true</td>
    <td>`Boolean` - Optional.</td>
  </tr>
</table>

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
