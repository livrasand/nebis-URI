# Nebis URI

Specification for Nebis URIs (aka Nebis keys, or identified by `nebis://`)

The basic Nebis URI scheme consists of the protocol identifier `nebis://`, followed by a username, a password, and the database name at the end of the URL. The general format is as follows:

##### Basic scheme:
```arduino
nebis://[username]:[password]@[url]/[database_name]
```

The username and password are used to authenticate the connection to the database on the server specified in the URL. The [database_name] at the end of the URL specifies the specific database on the server to be accessed.

#### Nebis DNS system (optional):
In addition, Nebis supports a DNS system that allows aliases to be created for database keys. This system is based on querying a special record in the domain, or else querying a TXT record in the DNS, to obtain the value of the URI.

In these cases, the part following the protocol identifier is a domain name from which the Nebis database key can be retrieved.

##### Nebis URI example with DNS:
```arduino
nebis://example.com
```

In this case, the database key can be obtained by querying a `.well-known/nebis` file or a TXT record named `nebiskey` in the domain `example.com`, which will contain the Nebis database URI.

##### Structure of `.well-known/nebis`:
The `.well-known/nebis` file on the server must contain the database URI, following either the basic or extended scheme. Additionally, it may contain a [TTL](https://en.wikipedia.org/wiki/Time_to_live) in milliseconds, in the following format:

```csharp
[URI]
ttl=<milliseconds>
```

#### Summary:
Nebis URIs are identified by one of the following schemes:

- Basic scheme: Uses the format `nebis://[username]:[password]@[url]/[database_name]`.
- DNS scheme: Uses a domain name to retrieve the Nebis database URI from a `.well-known/nebis` file or a TXT record in the DNS.
