how user1 is able to login in pc1.iforward.in

1- pc1 should part of domian
2- dns to be resolved form pc1
	-verification cmd	
	- telnet
	- nslookup (dns verify)
	- dig 
	- ping  (connectivity check)

3- dc should work
	- telnet (port 88- kerbrose )
4- dc (A) record must be in DNS

OR

1 - pc1 - ON
	pc1 Auth packet str

SIP - 10.11
DIP DC(10.10)
SPort - any random port
DPort - 88
DATA- user1 credentials (enc by kerbrose)

how pc1 know who is dc?
DNS query generate by pc1
DNS response by dns 

2 - DC (88 - listning state)
pc1 Auth packet recived
ntds.dit check user cread using LDAP

DC response to Auth packet 

if successfull then user1 will login in pc1

watch is video curefully
https://drive.google.com/file/d/1tW2Z9fuv4fCIefnx4bAfi5wI67qAxOkK/view?usp=sharing