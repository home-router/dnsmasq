# Ansible role to setup dnsmasq

[dnsmasq](https://thekelleys.org.uk/dnsmasq/doc.html) is a useful tool for small networks.
It can provide DNS, DHCP, TFTP, and PXE services. This ansible role setup
dnsmasq to provide DNS and DHCP services.

## Which TLD to use for a home network?

**It's confusing**.

[RFC 6762 Multicast DNS](https://datatracker.ietf.org/doc/html/rfc6762#appendix-G) uses `.local` as TLD.
Quoting from this RFC:

> we recommend against using ".local" as a private Unicast DNS top-level domain. 
> We do not recommend use of unregistered top-level
> domains at all, but should network operators decide to do this, the
> following top-level domains have been used on private internal
> networks without the problems caused by trying to reuse ".local." for
> this purpose:
>
>     .intranet.
>     .internal.
>     .private.
>     .corp.
>     .home.
>     .lan.

So `.local` domain name is used for network without DNS infrastructure.

[RFC 7788 Home Networking Control Protocol](https://datatracker.ietf.org/doc/html/rfc7788#section-8) written in 2016,
recommended using `.home` as home network TLD.
But 2018 written [RFC 8375 Special-Use Domain 'home.arpa.'](https://www.rfc-editor.org/rfc/rfc8375.html)
corrected this "mistake" because `.home` and `.corp` TLD can easily leak to external DNS name servers.
So those names will not become public registered TLDs.

I use `.home` as TLD for my home network and config dnsmasq to not forward
`.home` queries to external DNS servers.