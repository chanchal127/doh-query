# doh-query

This script is used to perform DoH queries

| Supported Platforms  |
| ---------------------|
| Linux |


| Supported Protocols  |
| ---------------------|
| IPv4 |
| IPv6 |

# Installation

```

> git clone git@github.com:chanchal127/doh-query.git
> cd doh-query
> ./sysinfo
Initial setup is done..!!
Now you can use doh-query script to perform DoH queries from you terminal..!!

```

# Usages

```

$ doh-query --help

usage: doh-http2 [-h] [--time] [--dns DNS] [--cert CERT] [--post] [--get]
                 [--noverify] [--ipv6] [--edns]
                 domain rr

This script is used to perform DNS queries over HTTPs protocol

positional arguments:
  domain       The Domain Name System to resolve.
  rr           Supported DNS Resourse Records ['A', 'AAAA', 'CNAME', 'MX',
               'NS', 'TXT', 'PTR']

optional arguments:
  -h, --help   show this help message and exit
  --time       show Query time
  --dns DNS    Enter the DoH Server. Default - dns.google
  --cert CERT  Enter the absolute path of the certificate
  --post       Use this argument for post request
  --get        Use this argument for get request (default request type).
  --noverify   Use this argument for no certificate varification request
  --ipv6       Use this argument if your are using IPv6 server.
  --edns       Use this argument if you need to enable EDNS.

```


# Sample Output

DoH query on IPv4 Server with the help of GET request with EDNS0 padding.

```

$ doh-query google.com A --dns 10.196.105.244 --noverify --get --edns

Domain name is google.com and RR is A

Find the DOH response for the GET query google.com:

id 10962
opcode QUERY
rcode NOERROR
flags QR RD RA
edns 0
payload 1220
option Generic 12
;QUESTION
google.com. IN A
;ANSWER
google.com. 184 IN A 142.250.68.78
;AUTHORITY
;ADDITIONAL

```


DoH query on IPv4 Server with the help of POST request with EDNS0 padding.

```

$ doh-query example.com A --dns 10.196.105.244 --noverify --post --edns

Domain name is google.com and RR is A

Find the DOH response for the POST query google.com:

id 10962
opcode QUERY
rcode NOERROR
flags QR RD RA
edns 0
payload 1220
option Generic 12
;QUESTION
google.com. IN A
;ANSWER
google.com. 184 IN A 93.184.216.34
;AUTHORITY
;ADDITIONAL

```
DoH query on IPv6 Server with the help of GET request without EDNS0 padding.

```
$ doh-query example.com AAAA --dns 2403:8600:80cf:e10c:4680::58 --noverify --get --ipv6

Domain name is example.com and RR is AAAA

Find the DOH response for the GET query example.com:

id 35666
opcode QUERY
rcode NOERROR
flags QR RD RA
;QUESTION
example.com. IN AAAA
;ANSWER
example.com. 60213 IN AAAA 2606:2800:220:1:248:1893:25c8:1946
;AUTHORITY
;ADDITIONAL

```


DoH query on IPv4 Server with a CA singned certificate.

```
$ doh-query example.com A --dns master.infoblox --cert /mnt/home/csutradhar/ca.pem --noverify --get

Domain name is example.com and RR is A

Find the DOH response for the GET query example.com:

id 35666
opcode QUERY
rcode NOERROR
flags QR RD RA
;QUESTION
example.com. IN A
;ANSWER
example.com. 60213 IN A 93.184.216.34
;AUTHORITY
;ADDITIONAL

```
