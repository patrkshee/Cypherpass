![Cypherpass](/img/cypher_128.png)

# Cypherpass

Let's kill passwords.

Cypherpass is a public key authenticator browser extension.

Cypherpass is a proof of concept exercise in using public key cryptography for
authentication through a browser extension and is aimed at lazy users that
aren't too worried about authentication security and desire to bypass passwords.

## What Cypherpass **IS NOT**
 * Completely secure.
 * Better than TLS.
 * Better than OpenSSL.
 * Better than $secure_solution

## What Cypherpass **IS**
 * Sometimes better than lazy, security unconcerned users reusing passwords
   and blinding trusting websites with password security.

## How does cypherpass work?
* Cypherpass generates a public/private key pair in the browser and saves it to
  Google's cloud storage syncing all instances.
* Supporting websites first associate user's public key with their login.
* When offering authenticating, a website generates a random token.
* Cypherpass signs the token and sends it back with the public key.
* The website verifies the signature thereby authenticating the user.

## How does autologin work?
* Cypherpass looks for a form named `public_key_login`
* Form should have an attribute named `challenge` with a randomly generated
  value (we suggest something a few bytes long, like
  "a319237c42162360a711f6a3ef790625")
* Cypherpass signs the value and inserts the newly created signature,
  concatenated with the public key delimited by `:`, into the form input
  named `signature`.
* Cypherpass submits the form for login.

### Hopes
 * Easy to implement server side
 * Automatic identification and authentication
 * Using email account retrieval with Cypherpass, a website could do away with
   passwords entirely.

### Features/Behavior
* Autofill forms with a type, "public_key"
* Cypherpass will not autologin if the page is asking for public key.

### Known Issues And Concerns
* Chrome's storage area isn't encrypted meaning sensitive information is
  stored in plaintext.

### //TODO
* In browser extension unit testing.
* Support multiple crypto suites.
* Rate limit auto login, allow user to configure this in options page.
* Option: Add an area to manually verify signatures.

### Wishlist
* Option: Encrypt stored variables.
  * Javascript to encrypt, unencrypt using a password.
* Option: New keypair for each login.
  * Would need workaround from chrome storage constraint.
* Support for client side certificates.
* Firefox support.
* Internalization.
* Mobile.
* Multiple logins.

Cypherpass proudly uses the jsrsasign library from
https://github.com/kjur/jsrsasign
