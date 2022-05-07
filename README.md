# High-Availability Domain Name Server

A DNS server for very specific circumstances only.

It is not suitable for 99% of use-cases, including *all* situations where eventual consistency is
not good enough.


Features and Requirements:

- HADNS is an authorative-only DNS server.
- It must be run on at least two geographically-diverse internet servers.
- Each HADNS instance monitors multiple (identical) webservers.
- The DNS replies exclude servers which are not currently proven to be working correctly.


Provided that your website:

- does not have a database, or
- uses MySQL multi-master (carefully and correctly)

it may work for you.


The simplest installation is:

- Two geographically-diverse internet servers.
- Each server runs HADNS and NGINX.

- When both are working, both HADNS servers will reply with with the address of both NGINX servers.
- If either server's website fails, both HADNS servers will reply with just the working server.
- If a server fails entirely, the single remaining server will reply with just the working server.
- TTLs are dynamic, but always less than five minutes.
