# snapshot_digitalocean_psedodownload
In trying to download a snapshot of my digital ocean server to host myself, I found out a) digital ocean does not support this and b) lots of people wanted this feature also. After figuring it out, I decided to compile the various tutorials I found so that others could do this also. If you have any feedback on other ways to do this, leave me a comment!

//Will write about how I set up my server here -- set up server to run a ruby on rails app

I found a tutorial by <a href= "http://www.aboutdebian.com/tar-backup.htm"> KEITH PARKANSKY </a> on writing a little script using tar. I ran through this a few times while we were figuring what configs the server needed to run our Ruby on Rails which can be found <a href = "https://github.com/c-hamilton/hour_report.git"> here </a>. 



Once the snap shot was saved within the user of the digital ocean server that you have ssh keys configured for, you can copy it over to the desired machine. In my case, I just put it on the desktop using <b>scp -r user@digital.ocean.server.ip:/path/to/backups /home/your_user_name/Desktop/ </b>

After this, I had the entire tar file on my desktop (yikes its big!) and was able to work with the IT guys to get it set up on our LAN. 
