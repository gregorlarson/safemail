# safemail
Sanitize email contents for forwarding to less secure zone or SMS.
# Background
## E-Mail as Identity and Authentication
Many companies and organization (Provider) use E-Mail as a proxy for identification. They use the email address to validate the identity of the Person, Company or Organization (Member) accessing their system. This relationship is usually established during the account signup. The Member is required to enter a valid email address into a web form along with their other identity information, and a code or URL containing a code is sent to the email address. When the Member follows the URL in the email or provides the code number back to a web-page, this validates that the relationship between the Provider account and that email address.

Later, if there is an authenication problem with that account, because the password has been forgotten, or stolen, then the Member can use an account recovery process where their email address is used to re-set the password and re-establish ownership of the account. This is done by the Provider sending a password reset URL or code to the validated email address where the Member can follow the URL or enter the code into a web-form in order to reset their password.
### The Good
The good things about this approach are that the Provider is leverging the email authentication and identity into their own system. The Member has strong incentives to retain control and privacy of their email account. The email provider may have a stronger relationship to the Member than the Provider, via another service, organization, employment or billing.
   - For example, if the Member purchases their email, then there is a billing relationship that the email Provider can use to assure identity.
   - If the email address is associated with the Members residential internet service, then there may also be local offices and support staff who can assure identity.
   - If the email address is provided incendental to employment or membership in another organization, then there are IT staff who will help assure the identity of the person with that address.
   - Some of the big free email providers (Google, Microsoft, Apple) now have very sophisticated account security proceedures using mutli-factor authentication and phone number OTP delivery.
   - If the email address is associated with their Domain registrar or Hosting provider, there are other systems, billing arragements and staff who can assure identity, however, there is more risk of a circular authentication dependancy here (see below).

### The Bad
Using email as a secondary authentication mechanism is really using email for something it was not designed for. It is *overloading* communication and authentication. In fact, using email addresses in this way is creating a security contradiction where we want email to be easy to access, and things like password-resets to be very difficult to access. Because the same email address will be used for communication and authentication, you can't simply lock-down the email address and only check it once or twice a year (or when you need a security override). In an organization, there may be more than one individual who should recieve emails from an important service provider.

Many (if not most) users do not have a really close relationship with their personal email provider. End-users are enticed to choose free email providers that provide portability, high-availability, good user-experiece and very high storage limits. The big free providers in North America are Google, Microsoft, Apple and Yahoo. There are a number of smaller providers as well.  Because these email accounts are free, there may be no billing information that can be used to support identity.  Also, users are moving away from the ISP or employer provided email and using the free email as their primary personal email address. In many cases there may no good backup email address that can be used to recover their primary email address.
#### Broken Authentication Chains
Users may abandon an email address or phone number, sometimes without considering all the consequences. A free email account may be closed simply because the user no longer logs into it regularly. 
When an email account or phone number is closed, the owner may forget that these addresses have the seconary use as an identity provider.
#### Accessing and Forwarding Email
Users will often want their email forwarded to a facility and device that is convenient to them. This raises the primary security contradiction with email.
> The user wants fast easy access to their email, and, we actually want them to have the fast, easy access in order that they may be informed and take actions based on that email.
An email address which is only available at a secure terminal in the office quickly becomes less useful, and there is a cascading effect where the less often an email address is checked, the less important email is sent there.
Because email must be very available to be useful, it is also more exposed to theft.

A person who checks their email 20 times a day is unlikely to enter a long password each time.

For these reasons, an email access theft is often the first step in a ugly security breach. A device with access to the email is misplaced or stolen. A user forgets to log out or lock their terminal.  Often there is a social component where the executive who is the one who will act on an email message is not trained or thinking about system security.
### The Ugly
You have strong system passwords, safely stored in a good password vault, that you never use on an insecure device, never cache in a browser. Perhaps you even use multi-factor authentication...
You may still be exposed to the email based account-attack.

> Even if you have not changed your password in years, and have logged into a system reqularly and recently, you might be unpleasantly surprised at what happens when some attacker clicks the I-Forgot-My-Password link.

Many providers will simply send the password-reset link to the email address they have on file for you. Sometimes they will ask a personal question, but not always. Sometimes they will ask for the email address associated with the account, which is not an effective sercurity measure. The attacker often already has access to an email account and it trying to use that email account to increase their level of control and access.
# How Safemail may protect you
Safemail allows you to *lock-down* an important email address and then forward santizied messages to less secure zones. In this way, the people who need to see the email can read it on whatever device they choose, but the forwarded emails do not have sufficient information for someone to assume ownership of the account.

If someone attempts a password reset using the email address, the forwarded version will contain the URL obscured such that is is not usable.
# Using Safemail
This utility can be used with a local delivery agent (LDA) like postfix or procmail to process the contents of an email message in order to remove attachments, html sections and message text that presents a security risk.
## Obcuring Codes and URLs
Safemil can obscure things like one-time-passwords (OTP), email verification links or account recovery and password reset links. What this means is that the email can then be forwarded to a less secure device or individual who may read the message but not be expected to handle all the security considerations associated with an email address.
## Retaining Useful Text in the Message
## HTML E-Mail
## Mutli-part (MIME) email
## Encoded Email (Base32/Base64)
## Limiting Message Size and Content Type
## Message Header Manipulations
### Redirecting
### Redirecting with Addresses Removed
### Forwarding

# Scripting and Installation

The script uses standard input and output which can be piped to sendmail or another message transport agent (MTA). I use the postfix (sendmail) MTA.

Use ```safemail -h``` to get a help message. Most of the args should self explanatory.

## Usage examples
Note that an email message with full headers is expected on standard input.

### Include only text/plain sections
```sh
safemail -p | sendmail user@example.com
```
### Forward the email rather than redirect/relay.
```sh
safemail -f | sendmail user@example.com
```
### Forward the message to a less secure device.
Remove any codes which could be used to override security.
```sh
safemail -fs | sendmail user@me.com
```
### Forward the message to an SMS gateway
Limit the content to text/plain and the size to 140 characters.
```sh
safemail -fpm 140 | sendmail 6135555555@vmobile.ca
```
### Redirect the message in safe mode, but allow some HTML
```sh
safemail -sa | sendmail user@example.com
```
### Redirect the email but remove From address from header.
```sh
safemail -up | sendmail user@example.com
```
### Redirect the email in safe mode, but allow numbers and html
```sh
safemail -sao | sendmail user@example.com
```
