Install adminer nginx Debian/Ubuntu

First, you need to create a directory inside `/usr/share` folder using the following command

```sudo mkdir /usr/share/adminer```

To get an updated version of adminer use following command:

```bash
sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/index.php
```

Now go to your Nginx default file of nginx and paste the following code (If you don't know vim, you might feel difficulty in existing. Please take a cup of vim first. Or replace any text editor you know in below command)

```
sudo vim /etc/nginx/sites-enabled/default
```
Change 7.3 to 8.1 or something if you use different version of php.
```
   location /adminer {
      root /usr/share/;
      index index.php index.html index.htm;
      location ~ ^/adminer/(.+\.php)$ {
         try_files $uri $uri/ /index.php?$query_string;
         fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
         include fastcgi_params;
         fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      }
   }

```
Simple restart your nginx server using the following commands 
```
sudo service nginx restart
```

Now visit Adminer here
http://your-domain-or-ip/adminer/
