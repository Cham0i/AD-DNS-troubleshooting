[DRAFT]
**THIS IS A CONTINIOUATION OF THE ACTIVE DIRECTORY DOMAIN TUTORIAL**

## What is DNS?

A DNS server is like a phone book but for computers.

Back when phones were less smart, commercials would list their phone numbers with words. Which is weird because phone numbers are numbers; you can't identify a specific phone user with letters. So what does 1-800-RUNAWAY mean? Well with dumb phones each number button would correspond to certain letters which would be used to text (you had to press the same button multiple times to get the letter you wanted).

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/flip.jpg)

Therefore, if you were to call 1-800 and then press the button with the letter R that would also be the same button for the number 7.
So R U N A W A Y would translate to
   7 8 6 2 9 2 9

Domains and IP address work the same way. When you go to google.com what you are really asking is to connect to 8.8.8.8. This is why it's possible to have multiple domains lead to the same website. For example, some comedic genius decided to register the domain Crappyschool.com to route to the University of California at Berkeley's home page. 

## The DNS Hierarchy

Local DNS Cache
When you drive home from work, you don't need turn on a navigation app to know how to get there 
Similarly, if a computer has previously looked up a domain for it's IP address, it can look at it's 
Own local history instead of searching for the IP again in DNS.

It works weirdly (look at my CS50 notes)

## Accessing DNS settings in Active Directory

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/1.png)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/2.png)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/3.png)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/4.png)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/5.png)

## Types of Records

A-Records (Address records)
They point a domain name to an IP

CNAME Record (Canonical name records)
Point a domain name to another domain name

## DNS commands and configuration in Active Directory

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/6.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/7.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/8.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/9.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/10.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/11.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/12.png)
![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/13.png)

A problem with that is that sometimes the IP address for a domain changes
And the local DNS cache is still using the old IP addresS.
In order for our computer to get the updated a record, our 
Cache must be cleared. Since we wipe the memory of ever going to a domain.
The computer will be forced to use DNS to find the a record
Instead of using its own history.
