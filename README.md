# Install Wordpress on AWSLightsail for blogs
 Steps performed
# Install Apache Web Server
sudo apt update -y
sudo apt install apache2 -y
# Install PHP
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update -y

# Enable the PHP-FPM module best practice

sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php8.0-fpm
sudo a2dismod php8.0
sudo systemctl enable php8.0-fpm
sudo service apache2 restart;sudo service php8.0-fpm restart

# Install Maria-DB

curl -LsS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | sudo bash -s -- --mariadb-server-version="mariadb-10.5"

sudo apt install mariadb-server -y

# Add permission to website folder and verify same

sudo usermod -a -G www-data ubuntu

sudo chown -R ubuntu:www-data /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} \;
find /var/www -type f -exec sudo chmod 0664 {} \;



