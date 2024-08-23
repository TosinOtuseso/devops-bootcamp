# Documentation
## Create An Ubuntu Server
<p> &#x2022; Locate and click on EC2 within the AWS management console. </p> 

![1](img/image_11.png)

<p> &#x2022; Click on Launch Instance </p> 

![2](img/image_12.png)

<p> &#x2022; Name your instance and select the Ubuntu AMI. </p> 

![3](img/image_013.png)

<p> &#x2022; Click the Create new key pair button to generate a key pair for secure connection to your instance. </p>

![4](img/image_13.png)
<h1> A proper documention of my first Devops project. </h1>

<p> &#x2022; Enter a Key pair name and click on Create key pair. </p>

![5](img/image_14.png)

<p> &#x2022; Enable SSH, HTTP, and HTTPS access, then proceed to click Launch instance. </p>

![6](img/image_15.png)
<p> &#x2022;  Click on View all instances. </p>

![7](img/image_16.png)

![8](img/image_17.png)

<p> &#x2022; Click on View all instances. </p>

<p> &#x2022;  Click on the created instance. </p>

![9](img/image_18.png)

<p> &#x2022; Click on the Connect button </p>

![10](img/image_19.png)

<p> &#x2022; Copy the command provided under SSH client. </p>

![11](img/image_20.png)

<p> &#x2022; Open a terminal in the directory where your .pem file was downloaded, paste the command and press Enter. </p>

![12](img/image_21.png)

# Create And Assign an Elastic IP
<p> &#x2022; Return to your AWS console and click on the menu icon to open the dashboard menu. </p>

![13](img/image_22.png)

<p> &#x2022; Click on the Allocate Elastic IP address button. </p>

![14](img/image_23.png)

<p> &#x2022; Keep the settings unchanged and proceed to click Allocate. </p>

![15](img/image_24.png)

<p> &#x2022; Associate this Elastic IP address with your running instance. </p>

![16](img/image_25.png)

<p> &#x2022; Select the instance you wish to associate with the elastic IP address, then click on Associate. </p>

![17](img/image_26.png)

<p> &#x2022; Paste the command into your terminal and then press Enter. When prompted, type "yes" and press Enter to connect.  </p>

![18](img/image_27.png)


# Install Nginx and Setup Your Website
<p> &#x2022; Execute the following commands.</p>
<code> sudo apt update </code>

<code>sudo apt upgrade </code>

<code> sudo apt install nginx </code>

<p> &#x2022; Start your Nginx server by running the  <code> sudo systemctl start nginx </code> command, enable it to start on boot by executing  <code>sudo systemctl enable nginx </code>, and then confirm if it's running with the <code> sudo systemctl status nginx </code> command. </p>

![19](img/image_28.png)


 <p> &#x2022; Go back to your EC2 dashboard and copy your Public IPv4 address. </p>

![20](img/image_29.png)

<p> &#x2022; Visit your instances Public IPv4 address in a web browser to view the default Nginx startup page. </p>

![21](img/image_30.png)

### How to obtain the website template URL from tooplate.com:

 <p> &#x2022; Visit Tooplate and select the website template you prefer.

 <p> &#x2022; Scroll down to the download section, right-click to open the menu, and select Inspect from the options.

<p> &#x2022; Click the Download button.

<p> &#x2022; You’ll see the website zip folder appear. Hover your mouse or trackpad pointer over it and right-click again.
Click the Download button.

<p> &#x2022; Hover your mouse cursor over Copy① and then click on Copy URL② from the list that appears on the right.

</p>

![22](img/image_31.png)

<p> &#x2022; Paste the URL into a notebook to use alongside the <code> curl </code> command when downloading the website content to your machine.</p>

![23](img/image_32.png)

<p> &#x2022; Run this command <code> sudo curl -o /var/www/html/2137_barista_cafe.zip https://www.tooplate.com/zip-templates/2137_barista_cafe.zip </code>to download the websites file to your html directory. </p>

![24](img/image_33.png)

<p> &#x2022; To install the unzip tool, run the following command: sudo apt install unzip.

<p> &#x2022; Navigate to the web server directory by running the following command: cd /var/www/html.

![25](img/image_34.png)

<p> &#x2022; Unzip the contents of your website by running sudo unzip 2137_barista_cafe.zip. 

![25](img/image_34.png)

<p> &#x2022; Update your nginx configuration by running the command <code> sudo nano /etc/nginx/sites-available/default </code>. Then, edit the <code>root </code> directive within your server block to point to the directory where your downloaded website content is stored.

![26](img/image_35.png)

![27](img/image_36.png)

### Restart Nginx to apply the changes by running: sudo systemctl restart nginx.

<p> &#x2022; Open a web browser and go to your Public IPv4 address/Elastic IP address to confirm that your website is working as expected. </p>

![28](img/image_037.png)

<p> &#x2022; Go back to your AWS console, search for Route 53①, and then choose Route 53② from the list of services shown. </p>
![29](img/image_39.png)

<p> &#x2022; Click on Get started. </p>

![30](img/image_40.png)

<p> &#x2022; Select Create hosted zones① and click on Get started②. </p>

![31](img/image_41.png)

<p> &#x2022; Enter your Domain name①, choose Public hosted zone② and then click on Create hosted zone③. </p>

![31](img/image_41.png)



<p> Although the project was very interresting, alot of challenges were encountered , yet given up wasnt part of the deal. </p>
<br>
<h2>Tutorial videos and Demos</h2>
<p>Tutorial videos and Demos really helped out as i had to watch and rewater them just to be able to understand what i was doing and give out the best in my expected results</p>

![1](img/image_1.png)
### The image above is an example of the results and more work needs to be done. 

![2](img/image_2.png)

![3](img/image_3.png)