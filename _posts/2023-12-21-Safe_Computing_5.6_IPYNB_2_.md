---
toc: True
comments: True
layout: notebook
title: Safe Computing
courses: {'csp': {'week': 12, 'categories': ['4.A']}}
categories: ['C1.4']
---

### Essential Knowledge:

<font color="yellow">

**IOC-2.A.5** Technology enables the collection, use, and exploitation of information about, by, and for individuals, groups, and institutions.

**IOC-2.A.6** Search engines can use search history to suggest websites or for targeted marketing.

**IOC-2.A.7** Disparate personal data, such as geolocation, cookies, and browsing history, can be aggregated to create knowledge about an individual.

**IOC-2.B** Explain how computing resources can be protected and can be misused.

**IOC-2.C** Explain how unauthorized access to computing resources is gained.
</font>

# Safe Computing

<font color="yellow">

**IOC-2.A.5** Technology enables the collection, use, and exploitation of information about, by, and for individuals, groups, and institutions.

**IOC-2.A.6** Search engines can use search history to suggest websites or for targeted marketing.

**IOC-2.A.7** Disparate personal data, such as geolocation, cookies, and browsing history, can be aggregated to create knowledge about an individual.
</font>

## Personal Identifiable Information (PII)

Personal Identifiable Information (PII): Information about someone that can be used to identify them.

- Name

- Race

- Age

- Phone number

- DOB

- Email

- Address

- Credit Card

- Medical Information 

- Biometric Data

Credit card, medical, and biometric information can not be shared without your consent.

Others can use it to steal your identity, money, or other personal information.

Search engines collect information without you knowing. They collect information about a user’s devices, networks, and websites visited and often use it to suggest things for you. The information we put out there is often there permanently.


### Good and bad things about PII

Good:

- It can be used to enhance user experience by suggesting things that you like

- The user can access websites and other info by looking at their history

Bad:

- Others can exploit it to access a user’s personal information

- Ex: If you book a trip to another country, this is what happens

     - The search engine knows all the details of your trip, such as dates, places, hotels, etc.

     - The second you search something up, it knows your IP address and email (from your user info)

     - Your internet service provider provides your name and address

     - The federal government has access to where you are traveling

     - Dozens of sites are tracking your information via your use of cookies

     - And even when you don’t have a device, cameras might be tracking you

**Risk to Privacy**

- Information you put online is very difficult to delete

- Information that you put online, knowingly or unknowingly can be used to know very personal information that you might not intend to share.

### <font color = "Green">Popcorn Hack 1:</font> 

List at least three apps or websites that might use PII:

- 1: 23&Me
- 2: Google
- 3: College Board

## Authentication
<font color="yellow">

**IOC-2.B** Explain how computing resources can be protected and can be misused.
</font>

Authentication measures protect devices and information from unauthorized access

Authentication measures:

- Strong passwords

- Multi-factor authentication

Strong Passwords:

- 10 or more characters

- Must contain a symbol

- Must contain a number

- Must contain lowercase and uppercase letters


Multi-Factor Authentication 

- Types of Authentication:

    - What You Know (IE: Your Password)

    - What You Have (IE: Personal Information)

    - What You Are (IE: Fingerprint)

- Why Use? 
    - Multi-Factor Authentication ensures that there's two steps before gaining access to personal or important information instead of strictly using a password. Examples of this are connecting phone numbers to accounts or connecting emails to accounts.   

        
- Viruses and Malware:

    - Viruses: Malicious programs that can copy themselves and gain access to systems that they are not supposed to be allowed in

    - Malware: Often intended to damage a computing system or take partial control over its operation

        - It can infiltrate a system by posing as legitimate programs or by attaching itself to legitimate programs, like an email attachment

    - Virus scans can help to prevent malicious code from getting into and affecting your system

Encryption and Decryption:

- Once legitimate access to a system is gained, it is important to ensure data sent to and from the system remains uncompromised

- Encryption: The process of encoding data to prevent unauthorized access

- Decryption: The process of decoding data

    - Two Types

        - Symmetric Encryption: one key used to both encrypt and decrypt data (IE: Caesar Cipher)

        - Asymmetric encryption
            
            - Public Key Encryption: uses two keys
            
                - A public key for encrypting
            
                - A private key for decrypting
            
            - A sender does not need the receiver’s private key to encrypt a message
            
            - The receiver’s private key IS required to decrypt the message


Digital certificates:

A certificate authorities issue digital certificates that validate the ownership of encryption keys used in secure communication and are based on a trust model. It makes sure that the decryption key that people recieve are issued by users or owners that own a true trusted key.


### <font color = "Green">Popcorn Hack 2:</font>

Create an encrypted code using symmetric encryption, and provide the code, and the actual message:


```python
import numpy as np

#Generate a completely random scrambled alphabet
ab_ori = np.array(['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'])
ab_scramble = np.array(['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'])
np.random.shuffle(ab_scramble)

message = 'parastratiosphecomyia stratiosphecomyioides'
encryption = ''

#Substitute letters in original message with the scrambled alphabet
for index in message:
    if index != ' ':
        encryption += ab_scramble[np.where(ab_ori == index)[0]][0]
        
decryption = ''
#Decrypt - spaces will be lost but the message is still readable, and cannot be guessed based on typography
for index in encryption:
    decryption += ab_ori[np.where(ab_scramble == index)[0]][0]

print(encryption)
print(decryption)

#Of course, the key still needs to be sent to the recipient, creating a security gap.
```

    nhfhmjfhjadmntgcduyahmjfhjadmntgcduyadavgm
    parastratiosphecomyiastratiosphecomyioides


## Risk Factors

<font color="yellow">

**IOC-2.C** Explain how computing resources can be protected and can be misused.
</font>

- Phishing: Tricking a user into giving personal information such as usernames, passwords, account numbers, or social security numbers.

    - Phishing emails: These emails look like companies you know and trust. These fake emails will trick you into clicking a link or an attachment

        - These links will either put a virus on your computer, send you to a website that looks like the real thing,  or a keylogger.

- Keylogger: records keys typed on the keyboard to gain access to a username, password, or any other personal information.

    - How do keyloggers get onto your computer?

        - One way is by plugging in a physical device to your computer.

        - Phishing emails through links

        - Clicking on a bad website

- Rogue access point: wireless network giving unauthorized access to secure networks

    - People intercept data traveled as it travels through networks.

        - Ex: A router installed in a secure network within an organization. A person could easily access the network and install any software, intercept communication, or steal network information.

    - Normal people trying to access their computers more easily leads to a lack of security. This makes it easy for other people to access the network.

### <font color = "Green">Popcorn Hack 3:</font>

Go to a website that checks your password and make a strong password.

Using individual keyboard characters as units of entropy with a full character set:
P40ANf@?g1a_ (est. 48000 years to guess randomly)

Although arguably if units of entropy are the only measure needed and the password is meant to be usable, an alternate approach (xkcd.com/936) may result in something like this:
corner_resign_freeze_bulletin_incongruous (6.2x10^20 years to guess randomly character-by-character)

### Homework

**Please answer these questions and send them to Daniel Lee on Slack. Graded on accuracy.**

    What is Personal Identifiable Information (PII), and list three examples of it?

- PII is any information unique to a user that can identify who they are, such as their address, SSN, or email address.

    What is a possible risk or cons to using PII?

- Giving out PII online can cause it to fall into the hands of scammers or other malicious actors.

    What are traits of a strong password?

- A strong password has high entropy (many possible character combination states), so that it is difficult to guess. Common methods of increasing entropy are to include ASCII symbols, capital and lowercase letters, and numbers to expand the possible states of each character.

    What does having a strong password prevent?

- A strong password makes it more difficult for third parties to gain access to a user's accounts for any reason, preventing them from modifying accounts in malicious ways.

    What are the two types of decryption and what is the difference between the two?

- Symmetric encryption uses a single key to encode and decode messages, while asymmetric encryption uses a public key to encrypt data, which is then decrypted using a separate private key that only the recipient has access to.

    What is phishing?

- Phishing is impersonating a trusted service in order to steal the personal information of that service's users.

    What is a way a keylogger can get into your computer?

- Keyloggers can be installed onto a device through links to malicious sites, downloading unkown software, or through external devices like USB drives.

    What is a rogue access point and how is it used?

- A rogue access point is an access point to a wireless network which has not been approved by security. They allow third parties to harvest data that moves through an organization's secure networks unknowingly.
