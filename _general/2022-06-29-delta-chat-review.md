---
layout: post
title:  "My new favorite messaing app: Delta Chat"
date:   2022-06-29 04:07:08 -0800
category: blog
tags: [linux_desktop, android, messaging, encryption]
---
# My new favorite messaing app: Delta Chat
*June 29, 2022*  
I am always on the search for a safe, secure messaging app that also has an easy on-ramp for my family and friends. Recently I was introduced to [Delta Chat](https://delta.chat/en/) and I have been truly enjoying the experience. What makes Delta Chat unique is it doesn't have a central system or even registration. Rather, it uses the Push-IMAP protocol to send messages via email. Instead of creating yet another account with a messaging system, you simply login with your email provider credentials (or OAUTH) and can start chatting. You don't even need other people to use the app, they can receive and reply to messages in their email. 

Couple quick notes:
1. Delta Chat uses the Autocrypt standard for encryption. Encrypted messages can be sent between Delta Chat users and groups (who verify with each other) or with other [Autocrypt enabled applications](https://delta.chat/en/help#what-do-i-have-to-do-to-activate-the-end-to-end-encryption). 
2. If you send a message to someone not on Delta Chat or a compatible email client, the message will not be encrypted. 
3. Standard metadata is not encrypted, such as the To/CC headers.

In general, messaging apps are a nightmare. Most offer little to no privacy and have no qualms with using the content from your messages for ads. Plus, most of them have systems for tracking certain types of speech. Although I don't promote, share, or use hate speech, the threat is always that these systems for monitoring for this type of speech can easily be used to stifle free speech. Just because the messaging app or service is your buddy now, it doesn't mean it will always be that way. 

We are watching this happen in real-time since Roe was overturned. Suddenly there are a lot of people that can be in real jeopardy if their private conversations can be requested by law enforcement. Every company that promises to not work with law enforcement on political or social issues will always cave when a court-order comes down. Therefore the best apps and services to use are the ones that don't collect information and can't access your content. 

Many people recommend using [Signal](https://www.signal.org/) and is generally the encrypted messaging app of choice. Technically I can't argue with that choice. Signal has proven again and again they cannot provide chats to law enforcement and their encryption is strong. However, I have a couple of personal reasons why I don't like to use Signal. First, I'm not a fan of being forced to use a phone number to register. I also don't need yet *another* app with a separate login system. Last is the direction of Signal in general and their (former) leader Moxie. With the addition of an [alt-cryptocoin](https://www.wired.com/story/signal-mobilecoin-cryptocurrency-payments/), plus notifying anyone that has your phone number that you also have Signal installed. 

For me, what I'm looking for in a messaging app is:
- End-to-end encrypted by default, using good standards and not custom-built (*ahem* Telegram)
- Cross-platform with the Android app available on F-Droid.
- Full gif support.
- Not app-specific. Meaning I can chat with people who don't have the app installed.
- Open source and uses existing standards instead of "inventing" yet another messaging platform.
- Available on F-Droid.

Delta Chat checks all of these boxes for me. It uses Autocrypt for E2EE and can message those not using the app (although the messages may not be encrypted). It is open source and available on essentially [every major platform](https://delta.chat/en/download).

## Daily usage
For the last week my wife and I have been using Delta Chat as our primary messaging system and so far, everything has worked fine. To get setup I was able to log us both in on our Android devices using our existing mail accounts. I am using a newer email provider that emphasizes more privacy and it worked out-of-the-box. To link our accounts and start sending encrypted messages I simply scanned a QR code on her device adn we could start chatting immediately. 

Delta Chat was able to create a folder in both email accounts for the chats, so our email inboxes don't fill up with encrypted messages. This is very nice and eliminates unnecessary clutter in my email inbox, but the messages are still accessible in a folder. I can view the messages in my email, but they are encrypted and cannot be read unless I am using a compatible email client that supports Autocrypt. More on that below. I was concerned in the beginning that messages would be slow since it is built to be sent through IMAP. As a marketer, I often run into problems with emails taking minutes to send. But, on average the messages take 10-15 seconds to appear, which is plenty fast. 

After setting up my mobile device, I installed the desktop client on my Pop_OS!-based laptop from the Pop Shop. Delta Chat provides a way to export by going to Settings > Chats and Media > Backup. This will export a backup and then you can import that into another client. Doing this will transfer the chat history and the encryption keys. In usage this is a nice and I can read the messages from my wife on both devices. However, my messages only exist on the devices they were sent from which means my wife's responses look a little strange and out-of-context. In the end it is not *that* big of a deal, just a small change I'd like to see in the future.

I have to say I am a pretty big fan of using existing standards or technology, and then building something new on top of them. Delta Chat is doing something really interesting with email and makes it much easier to approach since everyone already has an email account. No proprietary bits, no blockchain or Web3 mumbo-jumbo, and no MITM requirements like a registration server or phone number. Since I'm using a privacy-centered email platform, I did not need to give up any additional info to them. In my testing I have also been using [Orbot](https://guardianproject.info/apps/org.torproject.android/) to proxy my messages through Tor. This adds a small amount of additional privacy by hiding my IP and location. 

In general I've really enjoyed using Delta Chat and I am starting to send feelers out to other family members to see if they are interested. Honestly, the hardest part about messaging apps is convincing the people you know to switch. Many people are innundated with messaging apps. For me, I have Google Chat, Telegram, and Discord, plus several organizations I work with that push hard for me to use Slack. Adding Delta Chat on top of all of these apps is hard ask others to join in. But, with the growing political strain and how obvious the need for privacy on our most intimate conversations, I think asking people to switch will get easier especially for those with a tight inner circle. 

## Autocrypt keys on Android & Linux
Delta Chat will generate an [Autocrypt](https://autocrypt.org/index.html) key (which is integrated with OpenPGP standards). This key is used to encrypt messages in Delta Chat. But, this key can be used in other Autocrpyt compatible apps and services and is a nice feature of integrating Autocrypt encryption for this messaging app since I can then add the key to other apps and be able to decrypt the messages. Additionally, this means I can use the same key to encrypt other things and or easily migrate to a different app in the future using the same encryption process. 

[ DeltaChat FAQ: Can I re-use my existing private key? ](https://delta.chat/nb/help#can-i-re-use-my-existing-private-key)

To backup the keypair, go to Settings > Advanced > Manage Keys, then you can export the key. Once exported you can import into other OpenPGP/Autocrypt services.

On Android, the key can be imported using the [OpenKeychain](https://f-droid.org/en/packages/org.sufficientlysecure.keychain/) app and then accessed in [K-9 mail](https://k9mail.app/). Just add the keypair to an accessible folder (or a LAN accessible only Nextcloud instance in my case) and import. In K-9, go to Settings > General Settings > Select email account > End-to-end encryption. in this menu we can turn on OpenPGP support and select the key from OpenKeychain. 

On desktop Linux, the key can be imported in [Thunderbird](https://www.thunderbird.net/en-US/). Go to Menu > Account Settings and choose "End-to-End Encryption" for the account you want to use the key with. 

Once the key is imported in the apps, all Delta Chat messages will be decrypted and can be read. This is a nice feature just in case the app ever disappears, the messages are all in email and can be decrypted. This also means that I can have encrypted files and emails using the same key outside of the Delta Chat app.