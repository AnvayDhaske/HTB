# Skill Assessment for Windows CommandLine

0. ssh user0@{IP}

1. ssh user1@{IP}
cd Desktop
dir
type fag.txt 

2. ssh user2@{IP}
hostname

3. ssh user3@{IP}
cd Desktop
dir /ah

4. ssh user4@{IP}
cd Documents
where /r ~\Documents flag.txt > paths.txt
for /f %f in (paths.txt) do type %f & pause

5. ssh user5@{IP}
cd ..
net users

6. ssh user6@{IP}
systeminfo

7. ssh user7@{IP}
ssh user7@172.16.5.155 "pwd is the same as user"
powershell
get-module
get-flag

8. ssh user8@{IP}
Get-Module -Name ActiveDirectory -ListAvailable
Get-ADUser -FIlter *

9. ssh user9@{IP}
tasklist /svc | sort /r

10. ssh user10@{IP}
ssh user10@172.16.5.155
powershell
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625'} 
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625'}| select-object -expandproperty message 


