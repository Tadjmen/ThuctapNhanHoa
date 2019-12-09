ls -t
ls -tr















# Centos 7



# SSH sai pass
**First**

Dec  9 10:57:47 centos-7-client sshd[1698]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.182.1  user=root
Dec  9 10:57:47 centos-7-client sshd[1698]: pam_succeed_if(sshd:auth): requirement "uid >= 1000" not met by user "root"
Dec  9 10:57:49 centos-7-client sshd[1698]: Failed password for root from 192.168.182.1 port 52522 ssh2


**Second**
Dec  9 10:59:06 centos-7-client sshd[1698]: pam_succeed_if(sshd:auth): requirement "uid >= 1000" not met by user "root"
Dec  9 10:59:09 centos-7-client sshd[1698]: Failed password for root from 192.168.182.1 port 52522 ssh2

# SSH đúng pass

Dec  9 11:01:27 centos-7-client sshd[1717]: Accepted password for root from 192.168.182.1 port 52619 ssh2
Dec  9 11:01:27 centos-7-client sshd[1717]: pam_unix(sshd:session): session opened for user root by (uid=0)


# SSH non User

**Sau khi nhập User**

Dec  9 11:04:25 centos-7-client sshd[1755]: Invalid user fokgofkg from 192.168.182.1 port 52684
Dec  9 11:04:25 centos-7-client sshd[1755]: input_userauth_request: invalid user fokgofkg [preauth]

**Nhập Pass**

Dec  9 11:05:12 centos-7-client sshd[1759]: pam_unix(sshd:auth): check pass; user unknown
Dec  9 11:05:12 centos-7-client sshd[1759]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.182.1
Dec  9 11:05:13 centos-7-client sshd[1759]: Failed password for invalid user fgfkogf from 192.168.182.1 port 52704 ssh2


# Đóng cửa sổ SSH

Dec  9 11:05:47 centos-7-client sshd[1759]: Connection closed by 192.168.182.1 port 52704 [preauth]






# Kali Linux

# SSH sai pass
**First*