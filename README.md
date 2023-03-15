# AD-DNS-troubleshooting
[DRAFT]

What is DNS?
Back when phones were less smart, commercials would list their phone
numbers with words. Which is weird because phone numbers are numbers,
You can't identify a specific phone user with letters. 
So what does 1-800-RUNAWAY mean? 
Well with dumb phones each number button would correspond
To 3 letters which would be used to text
(You had to press the same button multiple times to get the 2nd or 3rd letter)
So if you were to call 1-800 and then press 
the button with the letter R that would also be the same button
For the number X
So runaway would be a simple cypher which would translate
To the number 7862929

Domains and IP address work the same way. When you go to google.com 
What you are really asking is to connect to 8.8.8.8
This is why it's possible to have multiple domains lead to the same website
Yale troll domain example

A DNS server is like a phone book containing IP address
Associated with each domain. It works weirdly (look at my CS50 notes)

A-Records (Address records)
They point a domain name to an IP

Local DNS Cache
When you drive home from work, you don't need turn on a navigation app to know how to get there 
Similarly, if a computer has previously looked up a domain for it's IP address, it can look at it's 
Own local history instead of searching for the IP again in DNS.

A problem with that is that sometimes the IP address for a domain changes
And the local DNS cache is still using the old IP addresS.
In order for our computer to get the updated a record, our 
Cache must be cleared. Since we wipe the memory of ever going to a domain.
The computer will be forced to use DNS to find the a record
Instead of using its own history.

CNAME Record (Canonical name records)
Point a domain name to another domain name
