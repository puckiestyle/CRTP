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

root@kali:~/CTF/HTB/Blackfield# ldapsearch -H ldap://blackfield.local:389 -x -b DC=blackfield,DC=LOCAL
# extended LDIF
#
# LDAPv3
# base <DC=blackfield,DC=LOCAL> with scope subtree
# filter: (objectclass=*)
# requesting: ALL
#

# search result
search: 2
result: 1 Operations error
text: 000004DC: LdapErr: DSID-0C090A69, comment: In order to perform this opera
 tion a successful bind must be completed on the connection., data 0, v4563

# numResponses: 1
```

Later when I found credentials for user "support" it also failed to bind

```text
root@kali:~/CTF/HTB/Blackfield# ldapsearch -h blackfield.local:389 -U support@10.10.10.192 -b DC=blackfield,DC=LOCAL
SASL/DIGEST-MD5 authentication started
Please enter your password:
ldap_sasl_interactive_bind_s: Invalid credentials (49)
        additional info: 8009030C: LdapErr: DSID-0C090597, comment: AcceptSecurityContext error, data 52e, v4563
