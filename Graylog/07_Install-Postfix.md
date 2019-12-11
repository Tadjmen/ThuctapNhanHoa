#

## Step 1 – Install Postfix
```
yum remove sendmail
yum -y install postfix cyrus-sasl-plain mailx
yum install postfix
```
```
systemctl restart postfix
```
## Step 2 – Configure Postfix
```
vi /etc/postfix/main.cf
```
Thêm vào cuối tập tin  
```
myhostname = hostname.example.com

relayhost = [smtp.gmail.com]:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-bundle.crt
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
```

## Configure Postfix SASL Credentials
Create a `/etc/postfix/sasl_passwd` file and add following line:
```
[smtp.gmail.com]:587 username:password
```

Phân quyền
```
postmap /etc/postfix/sasl_passwd
chown root:postfix /etc/postfix/sasl_passwd*
chmod 640 /etc/postfix/sasl_passwd*
systemctl reload postfix
```
## Kiểm tra 

```
echo "This is a test." | mail -s "test message" ngocattuong1997@gmail.com
```

<img src="https://i.imgur.com/Nw8puFo.png">

```
systemctl restart postfix
systemctl enable postfix
```

```
iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 25 -j ACCEPT
iptables -A INPUT -m state --state NEW -m udp -p udp --dport 25 -j ACCEPT
```
```
firewall-cmd --permanent --add-port=25/tcp
firewall-cmd --permanent --add-port=25/udp
firewall-cmd --reload
```
