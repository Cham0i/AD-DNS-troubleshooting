**THIS IS A CONTINUATION OF THE [ACTIVE DIRECTORY DOMAIN TUTORIAL](https://github.com/Cham0i/AD-creation-Azure)**

# Understanding DNS

**Operating System:**
- Windows Server 2022

**Commands Used:**
- ipconfig /flushdns
- ipconfig /displaydns
- nslookup [name]

**Chapters:**
- [What is a DNS Record?](https://github.com/Cham0i/Understanding-DNS/edit/main/README.md#what-is-a-dns-record)
- [The Record Search Hierarchy](https://github.com/Cham0i/Understanding-DNS/edit/main/README.md#the-record-search-hierarchy)
  - Cache
  - Host File
  - DNS
- [Accessing DNS Settings in Active Directory](https://github.com/Cham0i/Understanding-DNS/edit/main/README.md#accessing-dns-settings-in-active-directory)
  - Types of Records
    - A-Record
    - CNAME Record
- [DNS Commands and Configuration](https://github.com/Cham0i/Understanding-DNS/edit/main/README.md#dns-commands-and-configuration)
  - Commands for problem solving + A Record demonstration
  - CNAME demonstration

## What is a DNS Record?

The Domain Name System (DNS) is like a phone book but for computers.

Back when phones were less smart, commercials would list their phone numbers with words. Which is weird because phone numbers are numbers; you can't identify a specific phone user with letters. So what does 1-800-RUNAWAY mean? Well with dumb phones each number button would correspond to certain letters which would be used to text (you had to press the same button multiple times to get the letter you wanted).

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/flip.jpg)

Therefore, if you were to call 1-800 and then press the button with the letter R that would also be the same button for the number 7.
So R U N A W A Y would translate to
   7 8 6 2 9 2 9

DNS records work the same way. When you go to google.com what you are really asking is to connect to 8.8.8.8. That's why it's possible to have multiple domains lead to the same website; like how a comedic genius decided to register the domain [crappyschool.com](crappyschool.com) to route to the University of California at Berkeley's home page. 

## The Record Search Hierarchy

To find an IP Address, a computer refers to the following in this order:

### 1. Cache

A cache is a collection of records for recently visited domains that is stored locally on your device. If you have previously visited a website, the computer will look at its own history and use the previously used IP Address to connect to the website. This saves the trouble of having to rely on DNS each time it wants to find an IP Address. More importantly, it saves DNS servers from having to process every single record search from every computer connected to the internet.

### 2. Host File

Host Files are more of a legacy feature than anything. It is esssentially a cache that you had to manually write, edit, and keep updated in order for a computer to know which IP Address to connect to. The role of a host file has essentially been outsourced to DNS servers.

In case you were curious, on Windows you can find the host file under C:\Windows\system32\drivers\etc\hosts

### 3. DNS Servers

DNS servers are like the entire internets' collective host file. If your computer cannot find an IP Address stored in its cache nor host file, it will contact other computers, I.E DNS servers, to find an IP Address associated with the domain you searched. How DNS servers work collectively to find the record you're looking for is quite complicated and if you are interested in learning you can [click here for a detailed explanation](https://cloudinfrastructureservices.co.uk/what-is-dns-hierarchy/). 

## Accessing DNS settings in Active Directory

Using Server Manager in your Domain Controller, you can find the DNS settings under "Tools" at the top right.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/1.png)

Under your DC's folder click on "Foward Lookup Zones"

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/2.png)

Click on your domain folder (mine is StarbaseISD.com)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/3.png)

In here we can find the DNS records. As you can tell, we have two records here. One for our DC and another for our Client VM.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/4.png)

By right clicking on open space we can find the option to make a new record.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/5.png)

### Types of Records

- A-Records (Address records), AAAA, or host records, point a domain name to an IP

- CNAME Record (Canonical name records), or aliases, point a domain name to another domain name

## DNS commands and configuration

### Commands for problem solving and A Record demonstration

To demonstrate DNS records, we are going to create an A-Record called CNN which will point to cnn.co.jp (Japanese CNN: 35.73.15.162)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/6.png)

There it is in our domain host file.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/7.png)

We will attempt to ping CNN Japan by using our domain's record named "cnn"

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/8.png)

The ping kind of worked (the packet loss is normal for this website). But we (intentially) made our record point to the wrong CNN website.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/9.png)

We can go back to our A-Record and edit the IP Address to point to the correct IP Address (American CNN: 151.101.3.5).

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/10.png)

However, if we try to ping "cnn" under our domain, the computer will still attempt to ping CNN Japan.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/11.png)

Remember our record search hierarchy? The computer is currently preferring to use its cache rather than its host file. Using the command **nslookup [name]** we can find the record for "cnn" in our Domain's host file. Using the command **ipconfig /displaydns** we can look at our computer's cache records.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/13.png)

The IP Addresses don't match because the cache is being prefered. What's the solution to this problem? The cache must be cleared. Once we wipe the cache the computer will be forced to use DNS (our domain's DNS host file) to find the A-record.

To do this we use the command **ipconfig \flushdns**

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/14.png)

By the way, you might not be able to run the command unless you are using adminstrative priviliedges. To run the command prompt as an admin right click on the app and "Run as administrator"

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/15.png)

If we check our cache again, we will see nothing; and if we ping "cnn" again, we will ping the correct IP Address.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/16.png)

### CNAME Demonstration

Just for bonus practice, we can also demonstrate how CNAME records work. First, we will go back to our records and create a CNAME record.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/17.png)

This one will be named "notfakenews" and it will point to our "cnn" domain name.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/18.png)

When we ping "notfakenews" it will point the computer to look for the domain "cnn" which in turn will ping the same IP.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/19.png)

Every CNAME record will eventually lead to an A-Record. This means changing that one A-Record to another IP Address will also automatically change the CNAME Records, based of the domain name from the original A-Record, to that new IP Address. This saves you the headache of having to edit 30 different A-Records to point to a new IP Address.
