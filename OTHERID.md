# Other Identification Options
If you are **not** using email for backup identification and account recovery, what are your other options (as a Provider)?
## [OpenID]
The OpenID protocol allows your users to authenticate to a Provider Site/Service using an identity provided by another Provider. Your users probably have an account at one or more *Identity* *Providers* that support OpenID. Big ones in North America include Google and Microsoft..

## [OAUTH]

## Multi-factor

## Account Recovery Key
Some of the more sophisticated providers (Microsoft and probably others) now allow you to recover access to your account
using recovery key that you can print or save in order to recovery your account at some point in the future.
This is a bit like a multi-factor authenticator key, except that you use it like a backup password, which, in some ways
makes it more effective as an account recovery tool.
  - the recovery password is generated, high-entropy, unguessable
(like an authenticator key).
  - because the recovery password is *not* designed to be used on a
regular basis and does not have to be installed in an authenticator
app, it can be stored securely and is not exposed to theft in the same
way as a frequently used password or key.

[OAUTH]: http://en.wikipedia.org/wiki/OAuth
[OpenID]: http://en.wikipedia.org/wiki/OpenID
