# snapshot_digitalocean_psedodownload
In trying to download a snapshot of my digital ocean server to host myself, I found out a) digital ocean does not support this and b) lots of people wanted this feature also. After figuring it out, I decided to compile the various tutorials I found so that others could do this also. If you have any feedback on other ways to do this, leave me a comment!

For information on inital set up of a Ruby on Rails app on a CentOS server see <a href = "https://www.digitalocean.com/community/tutorials/initial-server-setup-with-centos-7"> server setup </a> and <a href = "https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-centos-7"> rails set-up </a>.

I found a tutorial by <a href= "http://www.aboutdebian.com/tar-backup.htm"> KEITH PARKANSKY </a> on writing a little script using tar. I ran through this a few times while we were figuring what configs the server needed to run our Ruby on Rails web app for work,  which can be found <a href = "https://github.com/c-hamilton/hour_report.git"> here </a>. 

First we made a little shell script
```
$ cd /
$ mkdir backups
$ cd backups
$ vi fullserver.sh   (or nano or vim or whatever rocks your socks) 
``` In this file copy and paste this line:  ```
tar -cvpf /backups/fullbackup.tar --directory=/ --exclude=proc --exclude=sys --exclude=dev/pts --exclude=backups .
```
If you are curious about the details of what this line does, definitely checkout the link above. 

Make the file an executable by running from the parent folder of backups/
- ```chmod 750 /backups/fullserver.sh```
- ```./backups/fullserver.sh```

Once the snap shot was saved within the user of the digital ocean server that you have ssh keys configured for, you can copy it over to the desired machine. In my case, I just put it on the desktop using 
```scp -r user@digital.ocean.server.ip:/path/to/backups /home/your_user_name/Desktop/```

After this, I had the entire tar file on my desktop (yikes its big!) and was able to work with the IT guys to get it set up on our LAN. 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
##Below I compiled the various tutorials I used on digital ocean:
It was a pain to hunt down these sources each time I wanted to set up a new CentOS server with Rails
- 0. Make a new droplet on Digital Ocean. Use the $50 off coupon provided to students in the [GitHub Student Developer](https://education.github.com/pack)
- 1. Initial Server Set-up to create a non-root sudo user of the server
- a. ```ssh root@SERVER_IP_ADDRESS```
- b. ```adduser demo```
- c. ```passwd demo```
- d. ```gpasswd -a demo wheel``` <-- this adds sudo priveledges to your non root user. Since we were not using our server for more than set-up, I skipped this.
- 2. Install git because we all need git
a. ```sudo yum install git```
- 3. Install rbenv and Ruby Dependencies
a. ```sudo yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel```
b. ```git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
exec $SHELL```
c. ```echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile
exec $SHELL```
- 4. Make sure to logout and re-login here or the server will not recognize your rbenv commanbd!
- 5. Install Ruby and set the shells default version
a. ``` rbenv install -v 2.3.1 ```
b. ```rbenv global 2.3.1```
c. Running the right Ruby? ```ruby -v```
d. If you want to disable the gem log you can do so by running: ```echo "gem: --no-document" > ~/.gemrc```
e. ```gem install bundler````
- 6. Install rails 
a. ```gem install rails -v 4.2.2``` #This was the stable relese when we began but you can now use 5.0!
b. ```rbenv rehash```
7. Install Node.js because it is required by key Rails features like the Asset Pipeline
a. ```sudo yum -y install epel-release```
b. ```sudo yum install nodejs```
8. Clone your app using rails install
9. 

