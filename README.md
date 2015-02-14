# safemail
Sanitize email contents for forwarding to less secure zone or SMS.
# Background
## E-Mail as Identity and Authentication
Many companies and organization (Provider) use E-Mail as a proxy for identification. They use the email address to validate the identity of the Person, Company or Organization (Member) accessing their system. This relationship is usually established during the account signup. The Member is required to enter a valid email address into a web form along with their other identity information, and a code or URL containing a code is sent to the email address. When the Member follows the URL in the email or provides the code number back to a web-page, this validates that the relationship between the Provider account and that email address.

Later, if there is an authenication problem with that account, because the password has been forgotten, or stolen, then the Member can use an account recovery process where their email address is used re-set the password and re-establish ownership of the account.This is done by the Provider sending an password reset URL or code to the validated email address where the Member can follow the URL or enter the code into a web-form in order to reset their password.
### The Good
The good things about this approach are that the Provider is leverging the email authentication and identity into their own system. The Member has strong incentives to retain control and privacy of their email account. The email provider may have a stronger relationship to the Member than the Provider, via another service, organization, employment or billing.
   - For example, if the Member purchases their email, then there is a billing relationship that the email Provider can use to assure identity.
   - If the email address is associated with the Members residential internet service, then there may also be local offices and support staff who can assure identity.
   - If the email address is provided incendental to employment or membership in another organization, then there are IT staff who will help assure the identity of the person with that address.
### The Bad

### The Ugly

# Using Safemail
This utility can be used with a local delivery agent (LDA) like postfix or procmail to process the contents of an email message in order to remove attachments, html sections and message text that presents a security risk.
## Obcuring Codes and URLs
Safemil can obscure things like one-time-passwords (OTP), email verification links or account recovery and password reset links. What this means is that the email can then be forwarded to a less secure device or individual who may read the message but not be expected to handle all the security considerations associated with an email address. 
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
