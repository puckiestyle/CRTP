# LDAP enum

Tried LDAP enumeration with the domain info

```text
puck@parrot-lt]─[~/htb/blackfield]
$ldapsearch -x -h 10.10.10.192 -s base namingcontexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectclass=*)
# requesting: namingcontexts 
#

#
dn:
namingcontexts: DC=BLACKFIELD,DC=local
namingcontexts: CN=Configuration,DC=BLACKFIELD,DC=local
namingcontexts: CN=Schema,CN=Configuration,DC=BLACKFIELD,DC=local
namingcontexts: DC=DomainDnsZones,DC=BLACKFIELD,DC=local
namingcontexts: DC=ForestDnsZones,DC=BLACKFIELD,DC=local

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1


```

Later when I found credentials for user "support" tey worked

```text
$ldapsearch -h 10.10.10.192 -b "DC=BLACKFIELD,DC=local" -D 'support@blackfield.local' -w '#00^BlackKnight' > support_ldapdump
$wc support_ldapdump 
 20361  45385 594230 support_ldapdump

