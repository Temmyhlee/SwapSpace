# SwapSpace

This is a documentation of somethings we run at swapspacesystems especially devops.

Below are the various steps to setup Vagrant for your Windows Machine.


* Run CMD as Adminnistrator on you system.

C:\windows\system32> cd [space] .. (The goal here is to do this as many times until you get to c:\) or just run "cd C:/" (without quotes)

In your C drive make a directory say VMs with this command "mkdir vms". 
C:\ > cd vms
C:\vms> mkdir firstclass
C:\vms> cd firstclass
C:\vms\firstclass> vagrant init hashicorp/precise32 or vagrant init ubuntu/trusty64
{After this}
C:\vms\firstclass> vagrant up
{open the newly created vagrant script (VagrantFile) in your text editor}
…go to line 29, uncomment it, change the last two digits of the IP address from :10 to any two digits
ranging from 01 to 99
- Then copy the IP address
- Open x-shell
- Click new file on the top left corner to create a new folder
- Paste the IP address in the host space bar
- Click connect
- Username  vagrant
- Click ok
- Password  vagrant
When console comes up, you will see a prompt that begins with vagrant@.... To change to root,
Type "sudo -s" {sudo (space) (hypen) s}
==> "apt-get update"
apt-get install nginx
Questions will pop up  click Y on your keyboard
#service [space] nginx [space] restart
 Ater this…
> apt-get [space] update
> add-apt-repository ppa:ondrej/php (if this doesn’t work)
 Do
#apt-get [space] install [space] python-software-properties [space] build essential
  (if it shows error, try #apt-get update to redirect)
  Do
#apt-get-repository
  Then do;
#apt-get [space] install python
{after all this is complete}
 Do
#apt-get [space] install [space] php7.0 [space] php7.0-mysql [space] php7.0-fpm [space] php7.0-cli
[space] php7.0-common [space] php7.0-mcrypt [space] php7.0-mbstring [space] php7.0-curl
{if it works, do…}
#apt-get [space] update
{after this, do}
Service [space] php7.0-fpm restart
(after php is successfully installed, our goal is to expose nginx to php and php to nginx)
…In our Guest environment (Xshell)
Type…
Cd ~
Cd [space] /etc
/ls
  after the dropdown
Type…
Cd [space] nginx
 {a dropdown occurs}
***Note: Look out for the following step and proceed as follows;
root@vagrant-ubuntu-trusty-64:/etc/nginx #cd [space] sites-available  type {cd sites-available}
root@vagrant-ubuntu-trusty-64:/etc/nginx/sites-available # ls  type{ls}
root@vagrant-ubuntu-trusty-64:/etc/nginx/ nano [space] default  type{nano default}
***Note: in the dropdown that occurs now, your mouse won’t work, so use your arrows keys to
navigate through.
Use arrow key to come down to the second server
Change the root/user/…. To root/vagrant/www
Change the index index.html index.htm  index.php index.html index.htm
Scroll down and navigate gently to the second location(#location ~\ php$ { )
Here we need to uncomment the #location ~\php$
Then remove the second # directly beneath it
Then jump down to where we have fast cgi_pass, 127…….:9000 and uncomment it
Uncomment #fast cgi_index index.php
Uncomment # include fast cgi-params
Then uncomment the hash before the closing curly brace  #}
After all this, do CTRL + X, then click Y on your keyboard
root@vagrant … nano default
root@vagrant … cd [space] .. {cd [space] dot dot}
root@vagrant... Cd php
,, ,, ,, ,, ,, ,, ls {-el -ess}
,, ,, ,, ,, ,, ,, ,, cd [space] 7.0
,, ,, ,, ,, ,, ,, ,, ls
,, ,, ,, ,, ,, ,, ,, cd fpm
,, ,, ,, ,, ,, ,, ,, ls
,, ,, ,, ,, ,, ,, cd pool.d
,, ,, ,, ,, ,, ,, ls
,, ,, ,,, ,, ,, ,, www.conf
,, ,, ,, ,, ,, ,, ,, nano [space] www.conf
 Scroll down to [listen = /run/php/ php7.0-fpm.sock]
 Type…
Listen = 127.0.0.1:9000;
 Do CTRL + X, then click Y on your keyboard
 scroll down
after…
root@vagrant-ubuntu-trusty64:... Nano www.conf
 type…
cd ~
nginx restart
***Restarting nginx nginx***
(some dropdowns will occur)
Go to your CDM environment
 Type…
mkdir www
 after doing this, go back to Xshell
 type…
cd [space] /vagrant
ls
vagrant file www
cd www
www [space] nano [space] index.php
 …after this (it will bring up an empty screen)
Inside this, create a php file, by typing…
<?php
echo phpinfo();
?>
 …after this, do CTRL + X, then click Y on your keyboard
Copy the IP address that was created, paste it in your browser address bar, type /index.php and click
Enter
 …restarting
root@vagrant-ubuntu-trusty-64:/vagrant/www#  this shows
 …type
cd ~
apt-get [space] install [space] mysql-server
after entering the password you created earlier
do… apt-get [space] update
 …after this, do
apt-get install phpmyadmin php7.0 mbstring
phpenmod mbstring
ln [space] -s/usr/share/phpmyadmin [space]/vagrant/www {ln = “el en”}
 …then type,
service nginx restart
***restarting nginx nginx***
root@vagrant-ubuntu-trusty-64: ~ serice [space] php7.0-fpm [space] restart {type ~ service php7.0-
fpm restart}
root@vagrant-ubuntu-trusty-64: #cd [space] /etc
 …type
Cd [space] 7.0
ls {-el -ess}
cd[space] fpm
ls
cd [space] php
cd [space] php.ini
ls
cd [space] php.ini
cd [space] ~
cd [space] .. {cd dot dot}
cd [space] ~
cd [space]/etc/php/7.0/fpm
ls
 …you should see this, conf.d php-fpm.conf php.ini pool.d
nano [space]php.ini
cd [space] ~
~ #
~ # cd [space] php
***Go back to your CMD environment and vagrant halt***
***CONGRATULATIONS***
