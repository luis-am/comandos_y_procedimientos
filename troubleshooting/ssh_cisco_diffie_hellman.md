update-crypto-policies --set LEGACY
update-crypto-policies --show
ip ssh server algorithm encryption aes256-ctr aes192-ctr aes128-ctr

#Legacy changes
KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1
Ciphers 3des-cbc,aes128-cbc,aes128-ctr,aes256-ctr
