# Auth

## Authentication

Try to use just OAuth to authenticate a user.

## Authorization

Once you have validated that a user is a register user, you have two options `session` or `jwt tokens`

### Sessions

Create a secret for the user, and store it in a login sessions table along with the user's id.

Each time a requests come through you will need to check if the session token that's in the request is in the db.

You could change this to reading from cache.

Easy to logout a user, just delete the record.

### JWT

Created with (userId, secretKey, expiresIn)

Don't need to store anything, but harder to log someone out.

Have a `access` token and a `refresh` token. Access token lasts for shorted (e.g. 15 min), refresh last longer e.g. (30 days).

When the access token expires, server checks the refresh token. If refresh token is still valid then create a new access token.

## Storing on client

How to store jwt's or session tokens on user's device.

Either use `local storage` or `cookies`. Cookies are a bit better to use.

## Telling if a user is logged in (Front end)

Add a api call to get the current user based on the jwt or session token.
