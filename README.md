# Web-Application-Firewall
Step 1: Setup and Installation
1. Install Apache & ModSecurity: On a fresh Ubuntu Server VM, installthe Apache web server and
the ModSecurity module.
sudo apt update
sudo apt install -y apache2 libapache2-mod-security2
2. Enable ModSecurity: Enable the module and restart Apache.
sudo a2enmod security2
sudo systemctl restart apache2
3. Configure ModSecurity: Turn the engine on by editing the configuration f
4. sudo nano /etc/modsecurity/modsecurity.conf
Find the line SecRuleEngine DetectionOnly and change it to SecRuleEngine On.
Step 2: Deploy a Vulnerable App
For simplicity, we'll create a single vulnerable PHP page instead of installing a complex application like
DVWA.
1. Install PHP:
sudo apt install -y php libapache2-mod-php
Step 3: Create and Test a WAF Rule
1. Create a Custom Rules File
2. sudo systemctl restart apache2
2. Test the WAF:
o Benign Request: Open a web browser and go to http://<VM_IP>/login.php. Enter a
normal username like admin and click Login. It should work.
o Attack Request: Now, enter a basic SQLi probe into the username field: test' UNION
SELECT 1,2,3--
o Verify the Block: When you click Login, you will receive a 403 Forbidden error from the
server. The WAF has blocked your request. You can see the block message in Apache's
error log (sudo tail /var/log/apache2/error.log).
