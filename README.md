# Simple Authentication

The simple authentication utility service provides hashed password-based authentication with automatically generated salts and constant-time password verification with SHA and MD5 hashing algorithms. The authentication is good enough for non-critical use cases but should not be considered very secure due to the limited nature of the hashing algorithms in use.

## Configuration

This app has the following configuration options:

* *hashMethod* (optional): cryptographic hash function to use for new passwords. Default: `"sha256"`.
* *saltLength* (optional): length of new salts. Default: `16`.

## JavaScript API

This app exposes its functionality via a JavaScript API.

**Examples**

First add this app to your dependencies:

```js
{
  ...
  "dependencies": {
    "auth": "util-simple-auth:^2.0.0"
  }
  ...
}
```

Once you've configured both apps correctly, you can use it like this:

```js
var Foxx = require('org/arangodb/foxx');
var controller = new Foxx.Controller(applicationContext);
var auth = applicationContext.dependencies.auth;

// later ...

var result = auth.hashPassword('keyboardcat');
```

### Generate an authentication object

Generates an authentication object for a given password.

`auth.hashPassword(password)`

Returns an authentication object with the following properties:

* *hash*: the generated base64-encoded hash.
* *salt*: the salt used to generate the hash.
* *method*: see [Configuration](#configuration).

*Parameter*

* *password*: the password to hash.

### Verify a password

Verifies a password against a given authentication object.

`auth.verifyPassword(authData, password)`

Generates a hash for the given password using the properties stored in the authentication object and performs a constant time string comparison on them. Returns *true* if the password is valid or *false* otherwise.

*Parameter*

* *authData*: an authentication object.
* *password*: a password to verify.

## License

This code is distributed under the [Apache License](http://www.apache.org/licenses/LICENSE-2.0).
