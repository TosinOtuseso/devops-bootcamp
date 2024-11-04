# Setup Multiple Static Websites on a Single Server Using Nginx Virtual Hosts

### Install Nginx and Setup Your Website
<p> &#x2022; Execute the following commands. <code> sudo apt update</code> <code> sudo apt upgrade </code>

<code> sudo apt install nginx </code>

<p> &#x2022; Start your Nginx server by running the <code> sudo systemctl start nginx </code> command, enable it to start on boot by executing sudo systemctl enable nginx, and then confirm if it's running with the sudo systemctl status nginx command.

Visit your instances IP address in a web browser to view the default Nginx startup page.

Download your website template from your preferred website by navigating to the website, locating the template you want.

Right click and select Inspect from the drop down menu.

![1](img/image_1.png)

<p> &#x2022; Click on the Network tab and then click Download button.

![2](img/image_02.png)

<p> &#x2022; Right click on the website name, select Copy and click on Copy link address.

![3](img/image_002.png)

<p> &#x2022; To install the unzip tool, run the following command: sudo apt install unzip.

<p> &#x2022; Execute the command to download and unzip your website files <code> sudo curl -o /var/www/html/2098_health.zip https://www.tooplate.com/zip-templates/2098_health.zip && sudo unzip -d /var/www/html/ /var/www/html/2098_health.zip && sudo rm -f /var/www/html/2098_health.zip. </code>

![4](img/image_3.png)
<br>

### Here's an explanation of the command:


<p> &#x2022; The command <code>  sudo curl -o /var/www/html/2129_crispy_kitchen.zip https://www.tooplate.com/zip-templates/2129_crispy_kitchen.zip && sudo unzip -d /var/www/html/ /var/www/html/2129_crispy_kitchen.zip && sudo rm -f /var/w 
ww/html/2129_crispy_kitchen.zip <code>

<br>
<p> &#x2022;  <h3>> 1 </h3> <code> sudo curl -o /var/www/html/2098_health.zip https://www.tooplate.com/zip-templates/2098_health.zip

![5](img/image_4.png)

&#x2022; <code> sudo </code>: Runs the command with superuser (root) privileges.
<code> curl -o /var/www/html/2098_health.zip</code>: Downloads the file from the specified URL <code>(https://www.tooplate.com/zip-templates/2098_health.zip) </code> and saves it as 2098_health.zip in the /var/www/html directory.

<h3>2</h3> <code> && </code>: Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

<h3> 3 </h3> <code> sudo unzip -d /var/www/html/ /var/www/html/2098_health.zip </code>:

<code> sudo</code>: Runs the command with superuser (root) privileges.
<code> unzip -d /var/www/html/</code>: Extracts the contents of the zip file into the <code>/var/www/html/ </code> directory.
<code> /var/www/html/2098_health.zip:</code> Specifies the path to the zip file to be unzipped.

<h3>4</h3> <code> && </code> Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

<h3>5</h3> <code> sudo rm -f /var/www/html/2098_health.zip</code>

<code>sudo</code>: Runs the command with superuser (root) privileges.
 <code> rm -f </code>: Removes (deletes) the specified file forcefully (without prompting for confirmation).
</code> /var/www/html/2098_health.zip </code>: Specifies the path to the zip file to be deleted.
 
<br>In summary, this command downloads the website template file, extracts its contents to the web server directory, and then deletes the downloaded zip file to clean up the directory.

&#x2022; Download the 2nd website template by running the following command:

</code> sudo curl -o /var/www/html/2132_clean_work.zip https://www.tooplate.com/zip-templates/2132_clean_work.zip && sudo unzip -d /var/www/html/ /var/www/html/2132_clean_work.zip && sudo rm -f /var/www/html/2132_clean_work.zip </code>

To set up your website's configuration, start by creating a new file in the Nginx sites-available directory. Use the following command to open a blank file in a text editor: <code> sudo nano /etc/nginx/sites-available/cleaning </code>

![6](img/image_5.png)

Copy and paste the following code into the open text editor.

<code>
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html/example.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
</code>

&#x2022; Configure your second website by creating a new file in the Nginx sites-available directory with the following command: <code> sudo nano /etc/nginx/sites-available/health </code>.

![7](img/image_6.png)

&#x2022; Edit the <code> root </code> directive within your server block to point to the directory where your downloaded website content is stored.

Create a symbolic link for both websites by running the following command. <code> sudo ln -s /etc/nginx/sites-available/cleaning /etc/nginx/sites-enabled/ sudo ln -s /etc/nginx/sites-available/health /etc/nginx/sites-enabled/ </code>

![8](img/image_7.png)

<br>

![9](img/image_8.png)

# Create An A Record
To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Namecheap and then moving hosting to AWS Route 53, where I set up an A record.

![10](img/image_9.png)

&#x2022; Paste your IP address① and then click on Create records②.

![11](img/image_10.png)

Repeat the same process while creating your second subdomain record, and confirm that they both exist in the records list.

![12](img/image_11.png)

&#x2022; Open your terminal and run <code> sudo nano /etc/nginx/sites-available/cleaning </code> to edit your settings. Enter the name of your domain and then save your settings. 
&#x2022; Repeat the same for crispy_kitchen <code> sudo nano /etc/nginx/sites-available/crispy_kitchen </code>

&#x2022;  Restart your nginx server by running the <code> sudo systemctl restart nginx </code> command.

&#x2022; Go to your domain name in a web browser to verify that your website is accessible.

[14](img/image_15.png)

<br>

[15](img/image_16.png)


## You may notice the sign that says Not secure. Next, you'll use certbot to obtain the SSL certificate necessary to enable HTTPS on your site.

<br>

## Install certbot and Request For an SSL/TLS Certificate
Install certbot by executing the following commands: <code> sudo apt update sudo apt install python3-certbot-nginx sudo certbot --nginx </code>

[16](img/image_13.png)

 &#x2022; Execute the <code> sudo certbot --nginx </code> command to request your certificate. Follow the instructions provided by certbot and select the domain name for which you would like to activate HTTPS.

[17](img/image_14.png)

 &#x2022; Verify the website's SSL using the OpenSSL utility with the command: <code> openssl s_client -connect cleaning.cloudghoul.online:443 </code>

[18](img/image_17.png)

[19](img/image_18.png)


## End of project

## E choke!


