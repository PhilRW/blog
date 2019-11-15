---
title: "Mastodon and Keycloak SAML"
date: 2019-11-15T09:44:44-07:00
draft: false
categories:
- Tech
tags:
- social-media
- self-hosting
- sso
- passwords
- security
---

I managed to get [Mastodon](https://en.wikipedia.org/wiki/Mastodon_(software)) SAML sign-ins working with [Keycloak](https://en.wikipedia.org/wiki/Keycloak). Since I never bothered to learn anything about SAML, this made it difficult. But I persevered. I would like to share what finally made it work.

<!--more-->

# Mastodon

Mastodon's `.env.production` file:

```bash
SAML_ENABLED=true
SAML_ACS_URL=https://{your mastodon server}/auth/auth/saml/callback
SAML_ISSUER=mastodon
SAML_IDP_SSO_TARGET_URL=https://{your keycloak server}/auth/realms/{your realm}/protocol/saml
SAML_IDP_CERT=-----BEGIN CERTIFICATE-----MIIC...QKML-----END CERTIFICATE----- 
#SAML_IDP_CERT_FINGERPRINT=
SAML_NAME_IDENTIFIER_FORMAT=urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified
#SAML_CERT=
#SAML_PRIVATE_KEY=
SAML_SECURITY_WANT_ASSERTION_SIGNED=true
#SAML_SECURITY_WANT_ASSERTION_ENCRYPTED=true
SAML_SECURITY_ASSUME_EMAIL_IS_VERIFIED=true
SAML_ATTRIBUTES_STATEMENTS_UID=uid
SAML_ATTRIBUTES_STATEMENTS_EMAIL=email
#SAML_ATTRIBUTES_STATEMENTS_FULL_NAME="urn:oid:2.16.840.1.113730.3.1.241"
SAML_ATTRIBUTES_STATEMENTS_FIRST_NAME=first_name
SAML_ATTRIBUTES_STATEMENTS_LAST_NAME=last_name
#SAML_UID_ATTRIBUTE=uid
#SAML_ATTRIBUTES_STATEMENTS_VERIFIED=
#SAML_ATTRIBUTES_STATEMENTS_VERIFIED_EMAIL=
```

Get the `SAML_IDP_CERT` from Keycloak's Realm Settings -> Keys -> Certificate

# Keycloak

Create a new SAML client with the following:

## Settings

| Field                  | Value                                                  |
| ---------------------- | ------------------------------------------------------ |
| Client ID              | mastodon                                               |
| Include AuthnStatement | ON                                                     |
| Sign Documents         | ON                                                     |
| Sign Assertions        | ON                                                     |
| Name ID Format         | username                                               |
| Valid Redirect URIs    | https://{your mastodon server}/auth/auth/saml/callback |
| Base URL               | https://{your mastodon server}                         |

## Mappers

| Mapper Type | Property | SAML Attribute Name | SAML Attribute NameFormat |
| --- |  --- | --- | --- |
| User Property | lastName | last_name | Basic |
| User Property | email | email | Basic |
| User Property | firstName | first_name | Basic |
| User Property | uid | uid | Basic |

You could probably turn on Encrypted Assertions if you filled in the `SAML_CERT` and `SAML_PRIVATE_KEY` for Mastodon.

Keep in mind this is just one way of setting it up and naming the fields. But after looking at Mastodon's code and both servers' debug logs for a while, this seems to work for me.