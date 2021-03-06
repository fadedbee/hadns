# High-Availability Domain Name Server

A DNS server for very specific circumstances only.

It is not suitable for 99% of use-cases, including *all* situations where eventual consistency is
not good enough.

Almost everyone is better-off using a commercial CDN, some of which have free tiers.


Features and Requirements:

- HADNS is an authorative-only DNS server.
- It must be run on at least two geographically-diverse internet servers.
- Each HADNS instance monitors multiple (identical) webservers.
- The DNS replies exclude servers which are not currently proven to be working correctly.
- If there are many possible servers, just a few of the nearest-to-the-asker will be sent.


Provided that your website:

- does not have a database, or
- uses MySQL multi-master (carefully and correctly)

it may work for you.

<br>

The simplest installation:

- Two geographically-diverse internet servers.
- Each server runs both HADNS and NGINX.
- Any file-store must be rsync'd in both directions, between all servers, and must avoid clashing filenames.
- Any database must be multi-master and eventually consistent.

Its behaviour:

- When both are working, both HADNS servers will reply with with the addresses of both NGINX servers.
- If either server's website fails, both HADNS servers will reply with just the working server's address.
- If a server fails entirely, the single remaining server will reply with just the working server's address.
- TTLs are dynamic, but always less than five minutes.

