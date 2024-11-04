<h1> Documentation</h1>
<p> &#x2022; I had to reference Project1 for guidance on how to spin up an Ubuntu server.

 <p> &#x2022; Set an inbound rule for MYSQL in your security group. Click on Security① and select the Security group②.

![1](img/img_1.png)
![2](img/img_2.png)

<p> &#x2022; Click on Edit inbound rules.

![3](img/img_3.png)

<p> &#x2022; Click on Add rule.

![4](img/img_4.png)
<p> &#x2022; Click on Custom TCP① and select MySQL/Aurora②.

![5](img/img_5.png)

<p> &#x2022; I Entered the IP address I would use to allow access and click Save rules.

![6](img/img_6.png)

<p> &#x2022; Open your terminal and connect to your Ubuntu server via SSH.

![7](img/img_7.png)

<h2>Install Apache </h2>
<p> &#x2022; To install Apache, run the following commands in your terminal.

<code>sudo apt update </code>

![8](img/img_8.png)


<code>sudo apt install apache2</code>

![9](img/img_9.png)

<p> &#x2022; To enable Apache to start on boot, execute <code>sudo systemctl enable apache2</code>, and then verify its status with the <code>sudo systemctl status apache2</code> command.

![10](img/img_10.png)

<p> &#x2022;Now, let's check if our server is running and accessible both locally and from the Internet by executing the following command: <code>curl http://localhost:80 </code>.

![11](img/img_11.png)

<p> &#x2022; Copy your public IPv4 address from your EC2 dashboard.

![12](img/img_12.png)

<p> &#x2022; Open a web browser of your choice and try accessing the following URL: <code>http://<Public-IP-Address>:80</code>

![13](img/img_13.png)

<h3>Install MYSQL</h3>
<p> &#x2022;To install this software using 'apt', run the command sudo apt install mysql-server. When prompted, confirm the installation by typing 'Y' and then pressing ENTER.


![14](img/img_14.png)

<p> &#x2022; After the installation is complete, log in to the MySQL console by typing: sudo mysql.

<p> &#x2022; Run the following command to set the password for the root user with the MySQL native password authentication method: <code>ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'pass';</code>. Exit the MySQL shell when you're done by typing <code>exit></code>.

![15](img/img_15.png)

<p> &#x2022; Start the interactive script by running: <code>sudo mysql_secure_installation</code>. Answer y for yes, or any other key to continue without enabling specific options.

![16](img/img_16.png)

<p> &#x2022; Set your password validation policy level.

<p> &#x2022; Enable MySQL to start on boot by executing <code>sudo systemctl enable mysql</code>, and then confirm its status with the <code>sudo systemctl status mysql<code>② command.

![17](img/img_17.png)

<h2>Install PHP</h2>
<p> &#x2022; Install PHP along with required extensions by running the following script: <code>sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip</code>.

![18](img/img_18.png)

with <code>sudo apt install php libapache2-mod-php php-mysql</code>

![19](img/img_19.png)

<code>Confirm the downloaded PHP version by running php -v</code>.

![20](img/img_20.png)

<h2>Creating A Virtual Host For Your Website Using Apache<h2>
<p> &#x2022;Create the directory for Projectlamp using the 'mkdir' command as follows: <code>sudo mkdir /var/www/projectlamp</code> and assign ownership of the directory to our current system user using:<code>sudo chown -R $USER:$USER /var/www/projectlamp </code>

![21](img/img_21.png)

<p> &#x2022;Create and open a new configuration file in Apache's sites-available directory using your preferred command-line editor: <code>sudo vi /etc/apache2/sites-available/projectlamp.conf</code>.

<p> &#x2022;Creating this will produce a new blank file. Paste the configuration text provided below into it:
<code> <VirtualHost *:80>

ServerName projectlamp

ServerAlias www.projectlamp

ServerAdmin webmaster@localhost

DocumentRoot /var/www/projectlamp

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
</code>

![22](img/img_22.png)

<p> &#x2022; Save your changes by pressing the Esc key, then type :wq and press Enter.

<p> &#x2022; Run the ls command <code>sudo ls /etc/apache2/sites-available</code> to show the new file② in the sites-available directory.

![23](img/img_23.png)

<p> &#x2022;We can now enable the new virtual host using the a2ensite command: <code>sudo a2ensite projectlamp</code>.

<p> &#x2022; and to ensure your configuration file doesn’t contain syntax errors, run: sudo apache2ctl configtest. You should see "Syntax OK" in the output if your configuration is correct.

![24](img/img_24.png)

<p> &#x2022;To disable Apache's default website, use the a2dissite command. Type:<code>sudo a2dissite 000-default</code>.

<p> &#x2022; Finally run: <code>sudo systemctl reload apache2</code>. This will reload Apache for the changes to take effect

<p> &#x2022; To create the index.html file with the content "Hello LAMP from Jay" in the /var/www/projectlamp directory, use the following command: <code>sudo echo 'Hello LAMP from Jay' > /var/www/projectlamp/index.html</code>.

![25](img/img_25.png)

Now, let's open our web browser and try to access our website using the IP address:
<code>http://<EC2-Public-IP-Address>:80</code>

![26](img/img_26.png)

<p> &#x2022;Enable PHP On The Website
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To change the precedence of index files (such as index.php over index.html) in Apache, you'll need to edit the dir.conf file. Here’s how you can do it:

<p> &#x2022; Edit dir.conf file using a text editor (such as nano or vi): <code>sudo nano /etc/apache2/mods-enabled/dir.conf</code>

Look for the DirectoryIndex directive within this file. It typically looks like this:
<code> <IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
</code>

![27](img/img_27.png)

<p> &#x2022; To prioritize index.php over index.html, move index.php to the beginning of the list, like this:
<code> <IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
</code>



<p> &#x2022; Press ctrl + x① on your keyboard to save and exit.

<p> &#x2022; Finally, reload Apache for the changes to take effect: <code>sudo systemctl reload apache2</code>.

![28](img/img_28.png)

<p> Now, Apache will prioritize index.php over index.html when both files exist in the same directory.

<p> &#x2022;To create a new file named index.php inside your custom web root folder (/var/www/projectlamp), you can use the following command to open it in the nano text editor: nano /var/www/projectlamp/index.php.

<p> &#x2022;This will create a new file. Copy and paste the following PHP code into the new file:

<code><?php

phpinfo(); </code>

<p> &#x2022; Once I saved and closed the file, I went beck to web browser and refresh the page. and this was the result

![29](img/img_29.png)

<h3>Install Wordpress</h3>
After setting up our LAMP environment, we can start installing WordPress. First, we'll download the WordPress installation files and place them in the default web server root directory: /var/www/html.

<p> &#x2022; Navigate to the directory using the cd command cd /var/www/html, and then download the WordPress installation files using the following command: <code>sudo wget -c http://wordpress.org/latest.tar.gz</code>

![30](img/img_30.png)

<p> &#x2022;Extract the files from the downloaded WordPress archive using the command: <code>sudo tar -xzvf latest.tar.gz</code>

![31](img/img_31.png)

<p> &#x2022;Run the command ls -l to confirm the existence of the wordpress directory in the current location (/var/www/html).

![32](img/img_32.png)

<p> &#x2022;Check the user running your web server with the command: <code>ps aux | grep apache | grep -v grep</code>.

![33](img/img_33.png)

<p> &#x2022;Grant ownership of the WordPress directory and its files to the web server user (www-data) by running the command: <code>sudo chown -R www-data:www-data /var/www/html/wordpress</code>.

![34](img/img_34.png)

<h3>Create a Database For Wordpress</h3>
Access your MySQL root account with the following command: <code>sudo mysql -u root -p</code>. Enter the password② you set earlier when prompted.

![35](img/img_35.png)

<p> &#x2022;To create a separate database named wp_db for WordPress to manage, execute the following command in the MySQL prompt: <code>CREATE DATABASE wp_db;</code>

![36](img/img_36.png)

<p> &#x2022;To access the new database, you can create a MySQL user account with a strong password using the following command: <code>CREATE USER jay@localhost IDENTIFIED BY 'wp-password';</code>

![37](img/img_37.png)

<p> &#x2022;To grant your created user (jay@localhost) all privileges needed to work with the wp_db database in MySQL, use the following commands:
<code>GRANT ALL PRIVILEGES ON wp_db.* TO jay@localhost;
FLUSH PRIVILEGES;</code>

![38](img/img_38.png)

<p> &#x2022;Type <code>exit</code> to exit the MySQL shell.

![39](img/img_39.png)

<p> &#x2022;Grant executable permissions recursively (-R) to the wordpress folder using the following command:<code>sudo chmod -R 777 wordpress/</code>


![40](img/img_40.png)
<p> &#x2022;Change into the WordPress directory by running the command: <code>cd wordpress </code>

<h3>Configure Wordpress</h3>
Once you've established a database for WordPress, the next crucial step is setting up and configuring WordPress itself. To begin, you'll need to create a configuration file tailored for WordPress.

<p> &#x2022;Rename the sample WordPress configuration file with the command:<code> mv wp-config-sample.php wp-config.php.</code>

<p> &#x2022;Edit the wp-config.php file using the command: <code>sudo nano wp-config.php</code>.

![41](img/img_41.png)

<p> &#x2022;Update the database settings in the wp-config.php file by replacing placeholders like database_name_here, username_here, and password_here with your actual database details.

![42](img/img_42.png)

<p> &#x2022;Modify the configuration file projectlamp.conf: <code>sudo nano /etc/apache2/sites-available/projectlamp.conf</code> to update the document root to the directory where your WordPress installation is located.

![43](img/img_43.png)

<p> &#x2022;After updating the document root to /var/www/html directory in your editor, save the changes and exit.

![44](img/img_44.png)

<p> &#x2022;Reload Apache for the changes to take effect: <code>sudo systemctl reload apache2</code>.

<p> &#x2022;Once you've completed these steps, you can access your WordPress page to complete the installation. Open your web browser and go to <code>http://<EC2 IP>/wordpress/</code>. This will lead you to the WordPress setup wizard where you can finalize the installation process.

<p> &#x2022;Select your preferred language and then click on Continue to proceed.

![45](img/img_45.png)

<p> &#x2022;Enter the required information and click on Install WordPress once you have finished.

<p> &#x2022;Site Title①: Enter the name of your WordPress website. It's recommended to use your domain name for better optimization.
<p> &#x2022;Username②: Choose a username for logging into WordPress.
<p> &#x2022;Password③: Set a secure password to protect your WordPress account.
<p> &#x2022;Your email④: Provide your email address to receive updates and notifications.
<p> &#x2022;Search engine visibility⑤: You can leave this box unchecked to prevent search engines from indexing your site until it's ready.


![46](img/img_46.png)

WordPress has been successfully installed. You can now log in to your admin dashboard using the previously set up information by clicking the Log In button.

![47](img/img_47.png)
Once you successfully log in, you will be greeted by the WordPress dashboard page.

![48](img/img_48.png)

<h3>Create An A Record</h3>
To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Namecheap and then moving hosting to AWS Route 53, where I set up an A record.

To update your Apache configuration file in the sites-available directory to point to your domain name, use the command: <code>sudo nano /etc/apache2/sites-available/projectlamp.conf.</code>

<p> &#x2022;Ensure that the server settings in your Apache configuration point to your domain name, and that the document root accurately points to your WordPress directory. Once you've made these adjustments, save the changes and exit the editor.
<code>
<VirtualHost *:80>
    ServerName <Your root domain name>
    ServerAlias <Your sub domain name>
    ServerAdmin webmaster@<Your root domain name>

    DocumentRoot /var/www/html/wordpress

    <Directory /var/www/html/wordpress>
        Options Indexes FollowSymLinks
       # AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
</code>

![49](img/img_49.png)
To update your wp-config.php file with DNS settings, use the following command: <code>sudo nano wp-config.php</code> and add these lines to the file:
<code>
/** MY DNS SETTINGS */
define('WP_HOME', 'http://<domain name>');

define('WP_SITEURL', 'http://<domain name>');
</code>

Replace http://<domain name> with your actual domain name. Save the changes and exit the editor.


![50](img/img_50.png)

Reload your Apache server to apply the changes with the command: <code>sudo systemctl reload apache2</code>, After reloading, visit your website at http://<domain name> to view your WordPress site. Replace with your actual domain name.


![51](img/img_51.png)

To log in to your WordPress admin portal, visit http://<domain name>/wp-admin, Enter your username① and password②, then click on log In③. Replace with your actual domain name.

![52](img/img_52.png)

Now that your WordPress site is successfully configured to use your domain name, the next step is to secure it by requesting an SSL/TLS certificate.

![53](img/img_53.png)

<h3>Install certbot and Request For an SSL/TLS Certificate</h3>
<p> &#x2022;Install certbot by executing the following commands: sudo apt update sudo apt install certbot python3-certbot-apache

<p> &#x2022;Run the command sudo certbot --apache to request your SSL/TLS certificate. Follow the instructions provided by Certbot to select the domain name for which you want to enable HTTPS.

![54](img/img_54.png)

A message confirming that the certificate has been successfully obtained.


![54](img/img_54.png)

Visit your website to confirm, and you'll notice that the "not secure" warning no longer appears, indicating that your site is now secure with HTTPS.

![55](img/img_55.png)

<h3>Adeventure</h3>
