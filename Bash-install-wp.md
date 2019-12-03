# Cài đặt WordPress qua Script
Cài đặt `Apache`  

`yum install httpd`  
`systemctl start httpd`  
`systemctl enable httpd.service`  
`systemctl status httpd.service`
```
firewall-cmd --add-service=http --permanent
firewall-cmd --reload
```
Cài đặt MySQL


`yum install wget  `  
`wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm `  
`sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm  `  
`sudo yum install mysql-server  `  
```
sudo systemctl start mysqld  
sudo systemctl status mysqld 
sudo mysql_secure_installation  
```

Cài đặt PHP

`wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm  
rpm -Uvh remi-release-7.rpm  `  
`yum -y install php  `  
`yum --enablerepo=remi,remi-php71 install php-fpm php-common  `  
`yum --enablerepo=remi,remi-php72 install php-opcache php-pecl-apcu php-cli php-pear php-pdo php-mysqlnd php-pgsql php-pecl-mongodb php-pecl-redis php-pecl-memcache php-pecl-memcached php-gd php-mbstring php-mcrypt php-xml  `  
`php -v  `
``


Nhập lệnh chạy Script kèm tham số luôn 

<img src="https://i.imgur.com/t73Abo8.png">

# Command

`bash wpcai tuongdb admin password13`


Sử dụng nội dung Script

```
#!/bin/bash -e
clear
echo "============================================"
echo "WordPress Install Script"
echo "============================================"
echo "Database Name: "
echo -e $1
echo "Database User: "
echo -e $2
echo "Database Password: "
echo -s $3
echo "run install? (y/n)"
read -e run
if [ "$run" == n ] ; then
exit
else
echo "============================================"
echo "A robot is now installing WordPress for you."
echo "============================================"
#download wordpress
curl -O https://wordpress.org/latest.tar.gz
#unzip wordpress
tar -zxvf latest.tar.gz
#change dir to wordpress
cd wordpress
#copy file to parent dir
cp -rf . ..
#move back to parent dir
cd ..
#remove files from wordpress folder
rm -R wordpress
#create wp config
cp wp-config-sample.php wp-config.php
#set database details with perl find and replace
perl -pi -e "s/database_name_here/$1/g" wp-config.php
perl -pi -e "s/username_here/$2/g" wp-config.php
perl -pi -e "s/password_here/$3/g" wp-config.php

#set WP salts
perl -i -pe'
  BEGIN {
    @chars = ("a" .. "z", "A" .. "Z", 0 .. 9);
    push @chars, split //, "!@#$%^&*()-_ []{}<>~\`+=,.;:/?|";
    sub salt { join "", map $chars[ rand @chars ], 1 .. 64 }
  }
  s/put your unique phrase here/salt()/ge
' wp-config.php

config_database(){
    mysql -u root -e "CREATE DATABASE $1"
    mysql -u root -e "GRANT ALL PRIVILEGES ON $1.* TO $2@localhost IDENTIFIED BY '$3'"
}

config_database

#create uploads folder and set permissions
mkdir wp-content/uploads
chmod 775 wp-content/uploads
echo "Cleaning..."
#remove zip file
rm latest.tar.gz
#remove bash script
rm wp.sh
echo "========================="
echo "Installation is complete."
echo "========================="
fi

```

