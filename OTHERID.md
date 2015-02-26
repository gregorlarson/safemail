# Other Identification Options
If you are **not** using email for backup identification and account recovery, what are your other options (as a Provider)?
## [OpenID]
The OpenID protocol allows your users to authenticate to a Provider Site/Service using an identity provided by
another Provider. Your members probably have an account at one or more *Identity* *Providers* that support OpenID.
Popular ones in North America include Google, Microsoft and Facebook, however, there are many others.

Of course this raises a question about how much the member (and the Provider) can trust the OpenID provider
to be available and secure. If the OpenID provider is not trustworthy, or,
goes out of service, then the members will need another mechanism.

This also raises an awareness problem with Members not understanding the
nature of *federated* authentication. If, for example they are using Facebook
OpenID for authentication, but later, loose interest in Facebook, they may not
properly maintain and secure their Facebook account because they don't
understand how it is being used to authenticate to other providers.
  - so, if you are using a 3rd-party OpenID provider, you need to remind the
  user about this this dependency.
  - you may need to remind the member periodically, to set and maintain a
  second, separate password for access if their OpenID Provider fails for some
  reason.

## [OAUTH]
tbd
## Multi-factor
Mutli-factor genericly 
### Multi-factor using Phone Number
Meh. I don't consider this type of multi-factor as good or secure.
If the attacker gets your phone, then you really have to hope your
password is not cached in the browser or they could have all the
tokens necessary to take over your account.

When a member changes their phone number, they often don't think
about updating their accounts until they get their new number, and
the old number may be unavailable at that point, so now, you need to
make some exception for this situation.
### Multi-factor using Email Address
Meh, we are back where we started, using the Email address for something
it is really not designed for.
### Multi-factor using TOTP
In this mechanism, a key is installed into an authenticator app, usually on a
mobile device, and this app generates timed, single-use codes that can be
demanded during login.

This mechanism has significant advantages but some disadvantages.
   - because the key is installed on a mobile device, it is exposed to theft.
   - because the key is installed on a mobile device, the key may become
   unavailable because the mobile device can more easily be lost or damaged
   and may be more difficult to back-up.

## Account Recovery Key
Some of the more sophisticated providers (Microsoft and probably others) now allow members to
recover access to your account using a recovery key. This recovery key is generated when
requested by the member and can be saved or printed.
This is a bit like a multi-factor authenticator key, except that you use it like a backup password,
which, in some ways makes it more effective as an account recovery tool.
  - the recovery password is generated, high-entropy, unguessable
  (like an authenticator key).
  - because the recovery password is *not* designed to be used on a
regular basis and does not have to be installed in an authenticator
app, it can be stored securely and is not exposed to theft in the same
way as a frequently used password or key.
  - members can simulate some of this capability by (mis)-using a TOTP
authenticator key, that is, storing the key in their password vault rather than
in an authenticator app. Later, if they need to recover their account, they
can retrieve the key from their password vault, put it in an authenticator
app, and use the TOTP to assist in account recovery (if the Provider allows
a TOTP to support account recovery). I have to say, however,
that I *prefer* the pure recovery key mechanism, because it is fairly easy for
me to keep a key secure if I rarely have to use it.

Of course, this may require some prodding of users to remind them that they need to generate and keep this recovery key. It probably also requires periodic reminders to the user that they have generated this key, and, they need to make sure they still have it.
   - you could audit users periodically, asking them to enter a prefix or suffix
from there recovery key to prove they still have it (but the only time they
would enter the entire key, would be during account recovery).
   - please provide users will some way to validate that the recovery key
they have recorded is still good! Either with a date, a matching sequence
number, or by allowing the user to *test* their key somehow.

[OAUTH]: http://en.wikipedia.org/wiki/OAuth
[OpenID]: http://en.wikipedia.org/wiki/OpenID
