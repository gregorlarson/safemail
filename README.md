# safemail
Sanitize email contents for forwarding to less secure zone or SMS.
# Background
  - Refer to [Mail Identity](MAILIDENT.md) discussion (rant).
  - Also see [Other ID] (OTHERID.md) for discussion other identity options.

# How Safemail Can Protect your Account from an Email Takeover
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
