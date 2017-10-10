server {
        listen 80;
        listen [::]:80;

        server_name mysoch.com;
        client_max_body_size 32m;
        root /home/ulnda/www/wordpress;
        index index.html index.php;

        location / {
              try_files $uri $uri/ /index.php?$args;
        }
        location ~ \.php$ {                
              include snippets/fastcgi-php.conf;
              include fastcgi_params;
              fastcgi_pass unix:/run/php/php7.0-fpm.sock;
              fastcgi_param SCRIPT_FILENAME /home/ulnda/www/wordpress$fastcgi_script_name;
              fastcgi_param PHP_VALUE post_max_size=20M;
              fastcgi_param PHP_VALUE upload_max_filesize=20M;
        }
}
