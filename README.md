```
##############################################
# Sample client-side OpenVPN 2.0 config file #
# for connecting to multi-client server.     #
#                                            #
# This configuration can be used by multiple #
# clients, however each client should have   #
# its own cert and key files.                #
#                                            #
# On Windows, you might want to rename this  #
# file so it has a .ovpn extension           #
##############################################

# Specify that we are a client and that we
# will be pulling certain config file directives
# from the server.
client

# Use the same setting as you are using on
# the server.
# On most systems, the VPN will not function
# unless you partially or fully disable
# the firewall for the TUN/TAP interface.
;dev tap
dev tun

# Windows needs the TAP-Win32 adapter name
# from the Network Connections panel
# if you have more than one.  On XP SP2,
# you may need to disable the firewall
# for the TAP adapter.
;dev-node MyTap

# Are we connecting to a TCP or
# UDP server?  Use the same setting as
# on the server.
proto tcp
;proto udp

# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote 45.33.198.90 443
;remote my-server-2 1194

# Choose a random host from the remote
# list for load-balancing.  Otherwise
# try hosts in the order specified.
;remote-random

# Keep trying indefinitely to resolve the
# host name of the OpenVPN server.  Very useful
# on machines which are not permanently connected
# to the internet such as laptops.
resolv-retry infinite

# Most clients don't need to bind to
# a specific local port number.
nobind

# Downgrade privileges after initialization (non-Windows only)
user nobody
group nogroup

# Try to preserve some state across restarts.
persist-key
persist-tun

# If you are connecting through an
# HTTP proxy to reach the actual OpenVPN
# server, put the proxy server/IP and
# port number here.  See the man page
# if your proxy server requires
# authentication.
;http-proxy-retry # retry on connection failures
;http-proxy [proxy server] [proxy port #]

# Wireless networks often produce a lot
# of duplicate packets.  Set this flag
# to silence duplicate packet warnings.
;mute-replay-warnings

# SSL/TLS parms.
# See the server config file for more
# description.  It's best to use
# a separate .crt/.key file pair
# for each client.  A single ca
# file can be used for all clients.
;ca ca.crt
;cert client.crt
;key client.key

# Verify server certificate by checking that the
# certicate has the correct key usage set.
# This is an important precaution to protect against
# a potential attack discussed here:
#  http://openvpn.net/howto.html#mitm
#
# To use this feature, you will need to generate
# your server certificates with the keyUsage set to
#   digitalSignature, keyEncipherment
# and the extendedKeyUsage to
#   serverAuth
# EasyRSA can do this for you.
remote-cert-tls server

# If a tls-auth key is used on the server
# then every client must also have the key.
;tls-auth ta.key 1

# Select a cryptographic cipher.
# If the cipher option is used on the server
# then you must also specify it here.
# Note that v2.4 client/server will automatically
# negotiate AES-256-GCM in TLS mode.
# See also the ncp-cipher option in the manpage
;cipher AES-256-CBC
cipher AES-256-GCM
auth SHA256
key-direction 1
; script-security 2
; up /etc/openvpn/update-resolv-conf
; down /etc/openvpn/update-resolv-conf

 script-security 2
 up /etc/openvpn/update-systemd-resolved
 down /etc/openvpn/update-systemd-resolved
 down-pre
 dhcp-option DOMAIN-ROUTE .

# Enable compression on the VPN link.
# Don't enable this unless it is also
# enabled in the server config file.
#comp-lzo

# Set log file verbosity.
verb 3

# Silence repeating messages
;mute 20
<ca>
-----BEGIN CERTIFICATE-----
MIIB4jCCAWegAwIBAgIUKE4D3+sA5+CM+wTahTU58w3RJ9AwCgYIKoZIzj0EAwQw
DTELMAkGA1UEAwwCY2EwHhcNMjEwODEyMjIwODQwWhcNMzEwODEwMjIwODQwWjAN
MQswCQYDVQQDDAJjYTB2MBAGByqGSM49AgEGBSuBBAAiA2IABOHjTFz6bTO6GcCe
ivFXhl8zRGJXvmrx7g8nGBKYkdJLhVz3jHwUDPeDIj+vD1TQoc9mk06I3knqkjTL
IcWoq6MjsvDOm8ifGg/wSH4lnEFGNX99KzgKQvDCBefQZHONRKOBhzCBhDAdBgNV
HQ4EFgQUHHNaQZvsl5P099zIYoPwXvqCpzgwSAYDVR0jBEEwP4AUHHNaQZvsl5P0
99zIYoPwXvqCpzihEaQPMA0xCzAJBgNVBAMMAmNhghQoTgPf6wDn4Iz7BNqFNTnz
DdEn0DAMBgNVHRMEBTADAQH/MAsGA1UdDwQEAwIBBjAKBggqhkjOPQQDBANpADBm
AjEA//b35V5a20XyIlka9/T+nxMKxsCSCtDt8MZ5qLSQvfrdkWwL/fdSmq6NL1y0
nwuDAjEA6hN+IMAHURC4Lr/t+o3qRSDk1Eb4hV24b0+yKv+6sQ8tyaxu2mZgfi/R
TNBMXrNH
-----END CERTIFICATE-----
</ca>
<cert>
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            4a:f4:22:a1:15:2f:41:53:17:e2:49:63:ca:aa:d3:ae
        Signature Algorithm: ecdsa-with-SHA512
        Issuer: CN=ca
        Validity
            Not Before: Aug 13 07:19:37 2021 GMT
            Not After : Jul 28 07:19:37 2024 GMT
        Subject: CN=client1
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (384 bit)
                pub:
                    04:d8:c6:fe:64:23:f4:ec:fe:ab:9a:3f:a2:5a:24:
                    bd:87:31:6a:b7:74:20:e3:f0:2a:4c:a1:bf:09:75:
                    3e:13:ae:a6:f5:a7:98:55:35:08:67:f8:73:79:a6:
                    10:9b:9f:0b:3f:93:4f:c2:b6:4f:7b:59:c2:1e:95:
                    70:c3:70:12:a2:2b:3e:65:24:42:04:c2:41:fe:90:
                    f4:68:b5:f6:4e:a7:7a:98:62:a2:36:e4:4d:94:9d:
                    f8:a5:a8:53:16:d6:04
                ASN1 OID: secp384r1
                NIST CURVE: P-384
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            X509v3 Subject Key Identifier: 
                4F:78:A0:66:55:C3:35:8D:9F:8A:2B:9A:81:F4:B2:88:35:2D:82:FE
            X509v3 Authority Key Identifier: 
                keyid:1C:73:5A:41:9B:EC:97:93:F4:F7:DC:C8:62:83:F0:5E:FA:82:A7:38
                DirName:/CN=ca
                serial:28:4E:03:DF:EB:00:E7:E0:8C:FB:04:DA:85:35:39:F3:0D:D1:27:D0

            X509v3 Extended Key Usage: 
                TLS Web Client Authentication
            X509v3 Key Usage: 
                Digital Signature
    Signature Algorithm: ecdsa-with-SHA512
         30:64:02:30:42:c4:54:02:79:4b:a0:f4:1d:b7:f8:9b:85:34:
         eb:af:99:be:fe:c0:63:b5:bd:10:27:0b:f4:04:36:7c:32:78:
         fe:df:f3:8d:82:9e:44:90:2b:23:9b:76:96:66:78:b9:02:30:
         7a:a7:6b:d8:bb:26:99:e0:d7:1d:da:59:04:18:e0:c8:84:0d:
         f8:2a:84:1f:22:17:3c:a9:0c:ea:10:c9:c9:39:1a:88:6e:8f:
         8a:35:d6:05:1f:4c:56:c3:bf:bf:21:20
-----BEGIN CERTIFICATE-----
MIIB8zCCAXqgAwIBAgIQSvQioRUvQVMX4kljyqrTrjAKBggqhkjOPQQDBDANMQsw
CQYDVQQDDAJjYTAeFw0yMTA4MTMwNzE5MzdaFw0yNDA3MjgwNzE5MzdaMBIxEDAO
BgNVBAMMB2NsaWVudDEwdjAQBgcqhkjOPQIBBgUrgQQAIgNiAATYxv5kI/Ts/qua
P6JaJL2HMWq3dCDj8CpMob8JdT4Trqb1p5hVNQhn+HN5phCbnws/k0/Ctk97WcIe
lXDDcBKiKz5lJEIEwkH+kPRotfZOp3qYYqI25E2UnfilqFMW1gSjgZkwgZYwCQYD
VR0TBAIwADAdBgNVHQ4EFgQUT3igZlXDNY2fiiuagfSyiDUtgv4wSAYDVR0jBEEw
P4AUHHNaQZvsl5P099zIYoPwXvqCpzihEaQPMA0xCzAJBgNVBAMMAmNhghQoTgPf
6wDn4Iz7BNqFNTnzDdEn0DATBgNVHSUEDDAKBggrBgEFBQcDAjALBgNVHQ8EBAMC
B4AwCgYIKoZIzj0EAwQDZwAwZAIwQsRUAnlLoPQdt/ibhTTrr5m+/sBjtb0QJwv0
BDZ8Mnj+3/ONgp5EkCsjm3aWZni5AjB6p2vYuyaZ4Ncd2lkEGODIhA34KoQfIhc8
qQzqEMnJORqIbo+KNdYFH0xWw7+/ISA=
-----END CERTIFICATE-----
</cert>
<key>
-----BEGIN PRIVATE KEY-----
MIG2AgEAMBAGByqGSM49AgEGBSuBBAAiBIGeMIGbAgEBBDCq1X1XGndQMEuVF20a
QQhSjJ/5mII4jEmSttXE/K/8p/ARUYaAmP5VR2rbofe6Pn+hZANiAATYxv5kI/Ts
/quaP6JaJL2HMWq3dCDj8CpMob8JdT4Trqb1p5hVNQhn+HN5phCbnws/k0/Ctk97
WcIelXDDcBKiKz5lJEIEwkH+kPRotfZOp3qYYqI25E2UnfilqFMW1gQ=
-----END PRIVATE KEY-----
</key>
<tls-crypt>
#
# 2048 bit OpenVPN static key
#
-----BEGIN OpenVPN Static key V1-----
0aab45ab70ba67840c7ca6864498271e
887a713cf4b699eba05f3214e148b2c8
39e21c416541d0d441044e3c96820d7b
6ad9aca4a77f5906d9043eb449332f59
37d4f767225f4a092ede617030d6d067
47c3295178dbedcc0fd5d5ad08772174
a6784eccde0e06a246fa75e2f01500f5
4607351109124c937737c513fd54575a
38321114ac4a4645160d425b71a11cc0
f13a18e3ddef947c55be5e6cc4ed5e7f
6418f4e3fb99c314e2c27716e577d28d
a07fc20aadd265cf48d8f95557529141
703ded11d02cafce15301599dcc52a25
f0b77a0c7f40ff24392fd25e9ad7b379
510bfd8db6f0fc37a2a9ce3d016fb12c
9d589f9d2c753546fce47ee1431f8ae9
-----END OpenVPN Static key V1-----
</tls-crypt>
```
