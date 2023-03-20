[DRAFT]
**THIS IS A CONTINIOUATION OF THE ACTIVE DIRECTORY DOMAIN TUTORIAL**

## What is DNS Record?

The Domain Name System (DNS) is like a phone book but for computers.

Back when phones were less smart, commercials would list their phone numbers with words. Which is weird because phone numbers are numbers; you can't identify a specific phone user with letters. So what does 1-800-RUNAWAY mean? Well with dumb phones each number button would correspond to certain letters which would be used to text (you had to press the same button multiple times to get the letter you wanted).

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/flip.jpg)

Therefore, if you were to call 1-800 and then press the button with the letter R that would also be the same button for the number 7.
So R U N A W A Y would translate to
   7 8 6 2 9 2 9

DNS records work the same way. When you go to google.com what you are really asking is to connect to 8.8.8.8. This is why it's possible to have multiple domains lead to the same website. For example, some comedic genius decided to register the domain [crappyschool.com](crappyschool.com) to route to the University of California at Berkeley's home page. 

## The record search hierarchy

To find an IP Address, a computer refers to the following in this order:

### 1. Cache

A cache is a collection of records for recently visited domains that is stored locally on your device. If you have previously visited a website, the computer will look at its own history and use the previously used IP Address to connect to the website. This saves the trouble of having to rely on DNS each time it wants to find an IP Address. More importantly, it saves DNS servers from having to process every single record search from every computer connected to the internet.

### 2. Host File

Host Files are more of a legacy feature than anything. It is esssentially a cache that you had to manually write, edit, and keep updated in order for a computer to know which IP Address to connect to. The role of a host file has essentially been outsourced to DNS servers.

In case you were curious, on Windows you can find the host file under C:\Windows\system32\drivers\etc\hosts

### 3. DNS Servers

DNS servers are like the entire internets' collective host file. If your computer cannot find an IP Address stored in its cache nor host file, it will contact DNS servers to find an IP Address associated with the domain you searched. How DNS servers work collectively to find the record you're looking for is quite complicated and if you are interested in learning you can [click here for a detailed explanation](https://cloudinfrastructureservices.co.uk/what-is-dns-hierarchy/). 

## Accessing DNS settings in Active Directory

Using Server Manager in your Domain Controller, you can find the DNS settings under "Tools" at the top right.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/1.png)

Under your DC's folder click on "Foward Lookup Zones"

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/2.png)

Click on your domain folder (mine is StarbaseISD.com as established in the previous tutorial)

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/3.png)

In here we can find the DNS records. As you can tell we have two records here. One for our DC and another for our Client VM.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/4.png)

By right clicking on open space we can find the option to make a new record.

![alt text](https://github.com/Cham0i/Understanding-DNS/blob/main/DNS_pics/5.png)

## Types of Records

A-Records (Address records)
They point a domain name to an IP

CNAME Record (Canonical name records)
 a domain name to another domain name

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
