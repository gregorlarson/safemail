# safemail
Sanitize email contents for forwarding to less secure zone or SMS.

This utility can be used with a local delivery agent (LDA) like postfix or procmail to process the contents of an email message in order to remove attachments, html sections and message contents that present a security risk.

In particular, this utility can obscure things like one-time-passwords (OTP), email verification links or account recovery and password reset links. What this means is that the email can then be forwarded to a less secure device or individual who may not be expected to handle the security considerations associated with an email address. 

The script uses standard input and output which can be piped to sendmail or another message transport agent (MTA). I use the postfix (sendmail) MTA.

Use ```safemail -h``` to get a help message. Most of the args should self explanatory.

## Usage examples
Note that an email message with full headers is expected on standard input.

### Include only text/plain sections
```sh
safemail -p | sendmail
```
### Forward the email rather than redirect/relay.
Ignore (remove) From/To from incoming email.
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
safemail -sa | sendmail
```
