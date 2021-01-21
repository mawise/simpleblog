# SimpleBlog is now Haven

The version here has been deprecated, continued development at https://github.com/havenweb/haven

# Haven

[Haven](https://havenweb.org) is a simple blog application (formerly called SimpleBlog) built with Ruby on Rails, some motivating philosophies:

* Privacy-first.  This is for sharing with friends and family, not commercial endevors.  If you want a blog for your company, you probably want to use Wordpress instead
* Easy to use.
* Low-bandwidth friendly.  Images get downscaled to reduce page load times.  No javascript frameworks.  No ads or trackers.
* Customizable.  If you want to add custom CSS, you can do that
* No spam. There is no self-signup for users so there is no place for unauthorized users to impact your life

# Deployment
## AWS
* Register an account with AWS, the included scripts deploy to an AWS EC2 instance
* Buy a domain with AWS route 53, this is the domain that will point to the blog
* Clone this project onto your computer (tested with Mac OS Mojave and Ubuntu 18.04)
* Go to the `deploymentscripts` folder
* Execute `ruby deploy-aws.rb <domain> "<email>"`
  * Put your email address in quotes, this email is used for registering your HTTPS certificate
* Wait.  Deployment can 20 minutes
* The script will show you your login information, enjoy your blog
* Note: if anything goes wrong, you can run `ruby cleanup-aws.rb <domain>` to tear down everything the script created
* If you get this error: `cannot load such file -- aws-sdk-ec2 (LoadError)`, then type `gem install aws-sdk` and try again
## Raspberry Pi (Only tested with Pi Zero W)
Note, this requires a little bit more technical knowledge.  You know know how to flash an SD card and how to use the tools `ssh` and `scp`.  You should also be able to configure your own DNS and port forwarding. We're doing this fully headless, not plugging in a display or mouse/keybord to the Raspberry Pi.
* Configure your DNS to point to your home IP address.
  * If you're using AWS Route53 for your DNS, this script might be useful: https://github.com/mawise/r53dyndns
* Flash a micro SD card with Raspbian-Lite (Feb 2020)
  * http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2020-02-14/
* Enable SSH and Wifi: https://raspberrytips.com/raspberry-pi-wifi-setup/
* Insert the card into the Pi, and turn it on
* Make sure you can SSH to the Pi, then copy `deploymentscripts/deploy-pi.sh` from this repository to the Pi's home directory
  * Note, the script assumes your default home directory of `/home/pi` and that you're using the default `pi` user.
* Configure your home router to forward port 80 (http) and 443 (https) to the Raspberry Pi.
  * You might also want/need to configure a static IP address for the Raspberry Pi.
* SSH to the Pi and run: `bash deploy-pi.sh DOMAIN "YOUREMAIL"`
* Wait.  On the Raspberry Pi Zero W, installation can take over three hours.
* The script will give you your initial login information, enjoy your new blog!
* Note, there are no backups setup.  You may want to backup the database (PostgreSQL) and uploaded images (`/home/pi/simpleblog/storage`).



