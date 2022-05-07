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
- A DNS TTL of one minute.

