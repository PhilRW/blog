---
author: philrw
categories:
- Personal
- Tech
comments: true
date: "2015-03-09T16:25:04Z"
link: https://philrw.wordpress.com/2015/03/09/phils-guide-to-modern-communications-technology-options/
slug: phils-guide-to-modern-communications-technology-options
tags:
- email
- technology
- VoIP
title: Phil's Guide to Modern Communications Technology Options
wordpress_id: 85009
---

It appears that some of you may not know which communication tool to use or when to use it. Here is a helpful guide:

(Note: Sync = synchronous means real-time communication, asynchronous means not real-time.)

| Name                           | Privacy        | Sync         | Speed       | Form                    | Description                                                  |
| ------------------------------ | -------------- | ------------ | ----------- | ----------------------- | ------------------------------------------------------------ |
| Postal Mail (Snail Mail, USPS) | medium to high | asynchronous | slow        | printed text            | This is the original form of written correspondence. It is still useful and relatively secure from eavesdropping, provided you didn't compose the letter on a computer to start with. |
| Telephone (phone)              | medium         | synchronous  | real-time   | voice                   | What one gains in instantaneous communications, one loses in the ability to compose thoughts before communicating them. Use this method when you have to have a conversation with another person involving a lot of words and back-and-forth. Assume everything you say is being monitored or recorded unless you are using a VoIP service like [Ostel](https://ostel.co/). |
| Faxsimile (fax)                | medium         | synchronous  | real-time   | printed text            | Don't use this anymore. Just don't. Stop it. Stop. Stop using fax. |
| Email                          | none to high   | asynchronous | medium-fast | text, multimedia, files | Advantages: the ability to think before you communicate. Also it can (and should) be encrypted with S/MIME or PGP. Otherwise you get the security and privacy level of a traditional postcard (i.e., none whatsoever). Note that when encrypting email, header fields such as to/from addresses and subject lines are not encrypted, but the body (contents) of the message is. Use this when you have a relatively lengthy message to send to one or more people. Not suitable for short, conversational messages or sending large files since most servers still impose a 10 or 20 MB message limit. Use an online file sharing service such as Dropbox to send files and pictures to avoid clogging the recipient's inbox. |
| SMS (text, text message)       | low            | asynchronous | medium      | text, images            | Best used for short information that needs to go to a person's cell phone, such as an address or phone number. Do not use for sensitive information as SMS is not secure against eavesdropping. It is also fast to transmit but _slow_, _error-prone_, and generally _cumbersome_ to compose. Best to place a phone call or start an IM instead. |
| IM (Instant Message, chat)     | none to high   | asynchronous | fast        | text                    | Can (and should) be secured using OTR (Off-The Record) encryption technology. If using Google's service, they will keep your chat messages, possibly forever. Can be very fast, depending on the participant's speed in typing. Best for interruptible and informal conversations, especially in an office or other quiet environment where talking is discouraged but typing noise is not. Much faster than SMS assuming the users are using real computers with real keyboards. |
| Walkie Talkie (PTT, Zello) | low | asynchronous | fast | voice | The speed of talking with the asynchronicity of texting. The best of both worlds, but unfortunately not secure when using popular apps. Also not suitable for office or other quiet environments. Best used while driving or when ever a two-way radio would come in handy. |

Now let's look at modern comms from a use-case perspective.


* I need to ask a brief, unimportant question

  * IM (if "available"), otherwise [Wickr](https://wickr.com) or SMS as a last resort	

* I need (to send/receive relatively detailed) information and message receipt confirmation is critical.

  * Email, encrypted

* I just want to chat, but the other person is at work or otherwise unable to talk

  * Check his status, then start an encrypted IM session if "available"

* We're both away from our computers/on the road/in the field and need some quick back-and-forth communication without a lot of typing
	
  * Walkie Talkie/Zello

* At least one of us is driving a motor vehicle

  * NONE

* I need to have a conversation

  * [Encrypted VoIP](https://ostel.co/)

* I need to have a conversation RIGHT NOW
	
  * Telephone; don't say anything meaningful

* I need to send a password or a PIN or some other potentially devastating information

  * 1st choice: [Wickr](https://wickr.com). Set message expiration to as short as practical.	
  * 2nd choice: encrypted IM. Chat history should be OFF.

  * 3rd choice: encrypted email.

* I want to rant and rave to the world about something, with no particular audience in mind.

  * Blog post

The key points I want to make here are:

1. Think what the best available technology is at your disposal for the type of communication you want to achieve.
2. Consider your privacy and security before transmitting data. Operate under the assumption that any unencrypted end-to-end communication will be a part of the public record at some point in the future.


