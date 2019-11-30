# Cài đặt WordPress qua Script
Cài đặt `Nghinx`  
`sudo yum install epel-release `  
`sudo yum install nginx  `
```
sudo systemctl start nginx  
sudo systemctl status nginx  
sudo systemctl enable nginx  
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

## Confing Nginx kết hợp cùng PHP

Tạo 1 file mới trong thư mục `conf.d` của nginx  
```
touch /etc/nginx/conf.d/default.conf
vi /etc/nginx/conf.d/default.conf  
```
Config như sau: (thay IP hay Domain phù hợp)
```
server {  
    listen   80;
    server_name  SERVER_IP_OR_DOMAIN;

    # note that these lines are originally from the "location /" block
    root   /usr/share/nginx/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
`sudo service nginx restart  `  

Config `php-fpm`:  

`vi /etc/php-fpm.d/www.conf  `  

```
user = apache => user = nginx

group = apache => group = nginx

listen.owner = nobody => listen.owner = nginx

listen.group = nobody => listen.group = nginx

;listen = 127.0.0.1:9000 => listen = /var/run/php-fpm/php-fpm.sock
```

```
systemctl start php-fpm.service
systemctl enable php-fpm.service 
```

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

