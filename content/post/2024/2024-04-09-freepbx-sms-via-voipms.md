---
title: "FreePBX SMS Messaging via VoIP.ms"
date: 2024-04-09T11:09:22-06:00
draft: false
categories:
- Tech
tags:
- VoIP
- SMS
- SIP
- asterisk
- self-hosting
- homelab
- telephony
- FreePBX
---
Today I share my success with configuring SMS messaging on FreePBX (running Asterisk) through [VoIP.ms](https://voip.ms). Now I can text to and from other numbers using my landline SIP phones through my self-hosted PBX at home. If you don't know what any of that means, then this probably isn't for you.

<!--more-->

I ported my DIDs over to VoIP.ms because they allow SMS messaging, and they're a bit cheaper than my previous provider. Plus they use [SIMPLE](https://en.wikipedia.org/wiki/SIMPLE_(instant_messaging_protocol)) to send/receive SMS over their SIP trunks. 

I encountered a couple of problems. First I wanted to test text messaging between internal extensions. PJSIP only returns the first contact on an endpoint using `MessageSend()`, so my messages weren't going through to all devices since I register multiple devices to a single extension. A lot of the dialplan was taken directly from their excellent [wiki](https://wiki.voip.ms/article/SIP/SMS_with_FreePBX), with special thanks to [this discussion](https://community.asterisk.org/t/messagesend-to-all-pjsip-contacts/75485) (the key was `PJSIP_DIAL_CONTACTS()`). Here's the final dialplan that's working with multiple devices per extension:

```ini
[sms-in]
exten => _.,1,NoOp(Inbound SMS dialplan invoked)
same => n,NoOp(To: ${MESSAGE(to)})
same => n,NoOp(From: ${MESSAGE(from)})
same => n,NoOp(Body: ${MESSAGE(body)})
same => n,Set(NUMBER_TO=${MESSAGE_DATA(X-SMS-To)})
same => n,Set(HOST_TO=${CUT(MESSAGE(to),@,2)})
same => n,Set(ACTUAL_FROM=${MESSAGE(from)})
same => n,Set(ACTUAL_TO=pjsip:${NUMBER_TO}@${HOST_TO})
same => n,Set(TO_EXTEN=102)  ; default extension if no match
same => n,ExecIf($["${NUMBER_TO}" == "3035551234"]?Set(TO_EXTEN=101))
same => n,ExecIf($["${NUMBER_TO}" == "7205551234"]?Set(TO_EXTEN=102))
same => n,GosubIf($["${TO_EXTEN}" != ""]?pjsip-sms-send-sub,s,1)
same => n,Hangup()

[sms-out]
; Deliver to local 3-digit extension
exten => _XXX,1,Set(FROM_USER=${CUT(MESSAGE(from),<,2)})
same => n,Set(FROM_USER=${CUT(FROM_USER,@,1)})
same => n,Set(FROM_USER=${CUT(FROM_USER,:,2)})
same => n,Set(TO_EXTEN=${EXTEN})
same => n,Gosub(pjsip-sms-send-sub,s,1)
same => n,Hangup()

; Deliver to trunk if 10-digit number
exten => _NXXNXXXXXX,1,Verbose(Outboud Message dialplan invoked)
same => n,Set(VOIPMS_ACCOUNT=<our VoIP.ms subaccount>)
same => n,Set(VOIPMS_SERVER_NAME=<the VoIP.ms SIP server name>)
same => n,Set(TRUNK_NAME=<the name of the PJSIP VoIP.ms trunk>)
same => n,NoOp(To: ${MESSAGE(to)})
same => n,NoOp(From: ${MESSAGE(from)})
same => n,NoOp(Body: ${MESSAGE(body)})
same => n,Set(NUMBER_FROM=7205551234)  ; default CID if no match
same => n,Set(EXTEN_FROM=${CUT(CUT(MESSAGE(from),@,1),:,2)})
same => n,ExecIf($["${EXTEN_FROM}" == "101"]?Set(NUMBER_FROM=3035551234))
same => n,ExecIf($["${EXTEN_FROM}" == "102"]?Set(NUMBER_FROM=7205551234))
same => n,Set(NUMBER_TO=${CUT(CUT(MESSAGE(to),@,1),:,2)})
same => n,Set(ACTUAL_FROM="${NUMBER_FROM}" <sip:${VOIPMS_ACCOUNT}@${VOIPMS_SERVER_NAME}>)
same => n,Set(ACTUAL_TO=pjsip:${TRUNK_NAME}/<sip:${NUMBER_TO}@${VOIPMS_SERVER_NAME}>)
same => n,MessageSend(${ACTUAL_TO},${ACTUAL_FROM})
same => n,NoOp(Send status is ${MESSAGE_SEND_STATUS})
same => n,Hangup()

[pjsip-sms-send-sub]
exten => s,1,Verbose("Sending SMS to PJSIP extension: ${TO_EXTEN}")
same => n,Verbose(4, "DEVICE_STATE: ${DEVICE_STATE(PJSIP/${TO_EXTEN})}")
same => n,Set(TO_CONTACTS=${PJSIP_DIAL_CONTACTS(${TO_EXTEN})})
same => n,Verbose("TO_CONTACTS: ${TO_CONTACTS}")
same => n,Set(TECH=${DB(DEVICE/${TO_EXTEN}/tech)})
same => n,While($["${SET(TO_CONTACT=${SHIFT(TO_CONTACTS,&):6})}" != ""])
same => n,Set(ACTUAL_TO=${TECH}:${TO_CONTACT})
same => n,Verbose("Sending message now: To ${ACTUAL_TO}, From ${MESSAGE(from)}");
same => n,MessageSend(${ACTUAL_TO},${FROM_USER})
same => n,Verbose("Send status is ${MESSAGE_SEND_STATUS}")
same => n,EndWhile
same => n,Return()
```

The trunk's `message_context` is set to `sms-in` and each extension's `message_context` is set to `sms-out`. That's it.