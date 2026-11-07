# DNS resolution

> DNS maps a domain name to an IP address. It checks local caches first, then walks root → TLD → authoritative name server only if nothing local knows the answer.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 3–4)

## Key ideas
- **DNS (Domain Name System)** maps a domain name to an IP address.
- The lookup starts when the user enters a domain name and goes cheapest-first:
  1. **Browser cache**
  2. **OS DNS cache**
  3. **Hosts file**: a plain-text OS file that maps domains to IPs locally, before any external server is asked.
  4. **Recursive DNS server (ISP):** many users visit many domains and the ISP caches them, so your domain *might* already be there.
  5. **Root DNS server:** knows about the TLDs (top-level domains like `.com`, `.org`, `.net`) and returns the address of the right TLD server.
  6. **TLD server:** returns the domain's **authoritative name server (NS)**.
  7. **Authoritative NS:** maps the domain to its IP.
- Steps 1–4 are caches. Steps 5–7 are only needed on a full miss.

## Example
```
user types  shop.example.com
  browser cache? ── miss
  OS cache?      ── miss
  hosts file?    ── miss
  ISP resolver?  ── miss → asks on our behalf:
      root   → "for .com ask the .com TLD server"
      .com   → "example.com's NS is ns1.example-dns.net"
      NS     → "shop.example.com = 93.184.216.34"
  IP is cached back down the chain → browser connects
```

## Pitfalls
- Because of all these caches, a changed DNS record isn't visible everywhere instantly. Old IPs linger until the cached entries expire.
- The hosts file wins over external DNS. A stale entry there silently overrides the real record.
- The root server doesn't know your domain's IP. It only points you to the TLD.

## Related
- [HTTP basics](http-basics.md)
- [Browser rendering](browser-rendering.md)
- [Caching basics](../caching/caching-basics.md)
