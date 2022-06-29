- [Getting started on Linux](#get_start)
- [Setting up a Linux VPS to run Margin](#setup_linux_vps)
- [If my machine goes to sleep, will margin and its bots keep running?](#machine_sleep)
- [On Linux I'm getting the error message: Could not load the Qt platform plugin "xcb" in "" even though it was found.](#get_error_message)
- [I cannot install margin on my Ubuntu VPS](#cannot_install_margin)
- [What operating systems do you support?](#os_support)
- [Can I use a VPS?](#use_vps)
- [What are the minimum machine specs I need?](#machine_specs)
- [Can I use bots with futures trading?](#use_bots_with_futures_trading)
- [How to run margin in Docker?](#margin_in_docker)
- [How does the EMA crossover bot work?](#ema_bot_work)
- [How does the Bollinger Band bot work?](#bollinger_band_bot_work)
- [How does the mArgin maker bot work?](#margin_maker_bot_work)
- [How does the static ping pong bot work?](#ping_pong_bot_work)
- [I see an invalid range and can’t place an order](#invalid_range)

----

<h4 id="get_start" >Getting started on Linux</h4>

1. Download margin-x86_64-4.6.0.AppImage from [BTSE link](https://app.btse.com/download/margin-x86_64.AppImage)
1. Optionally, move and/or rename the newly created folder to where you want margin to reside. A common choice is `~/opt/margin`
1. Go into the margin folder and run the file. Before the first run, the icon will be a default icon and not the margin logo shown in the screenshot. 
1. Optionally, if you want to copy the .desktop file used to run margin to a different place, e. g. your desktop, or `~/.local/share/applications/` to be seen by your desktop environment, you'll have to change the last line to read something like `Exec=/home/username/opt/margin/margin-x86_64-4.6.0.AppImage` 

Adapt for the location you actually put margin in.

----

<h4 id="setup_linux_vps" >Setting up a Linux VPS to run Margin</h4>

Running Margin on a cloud-based VPS such as Azure or DigitalOcean allows a trader to run their strategies uninterrupted. 

To get set up, a windowing manager such as MATE needs to be installed together with a RDP (Remote Desktop Protocol) server such as Xrdp. The following instructions were tested on a Ubuntu 20.04 LTS droplet running on DigitalOcean. This setup involves the creation of a user called `margin`. 

First, log into your Linux VPS and run the following commands:

```bash
sudo adduser margin 
sudo usermod -aG admin margin 
sudo usermod -aG sudo margin 
sudo apt update && sudo apt dist-upgrade -y 
sudo apt install -y --no-install-recommends ubuntu-mate-core ubuntu-mate-desktop 
sudo apt install -y mate-core mate-desktop-environment mate-notification-daemon xrdp 
sudo -u margin echo mate-session > /home/margin/.xsession 
sudo cp /home/margin/.xsession /etc/skel 
sudo systemctl enable xrdp 
sudo systemctl start xrdp sudo apt install -y firefox
```

Next, log in as the margin user through your favorite RDP client, open Firefox and navigate to [btse.com](http://btse.com/) , download the latest Linux margin AppImage file (for example margin-x86_64-4.6.0.AppImage) to your Downloads directory. 

Next, open a terminal: 

`cd Downloads`

Next, some packages need to be installed in order to run the Margin trading terminal: 

`sudo apt install -y xcb* libxcb* libxkbcommon*`

Finally, run the terminal: 

`./margin-x86_64-4.6.0.AppImage`

----

<h4 id="machine_sleep" >If my machine goes to sleep, will margin and its bots keep running?</h4>

----

<h4 id="get_error_message" >On Linux I'm getting the error message: Could not load the Qt platform plugin "xcb" in "" even though it was found.</h4>

----

<h4 id="cannot_install_margin" >I cannot install margin on my Ubuntu VPS</h4>

----

<h4 id="os_support" >What operating systems do you support?</h4>

----

<h4 id="use_vps" >Can I use a VPS?</h4>

----

<h4 id="machine_specs" >What are the minimum machine specs I need?</h4>

----

<h4 id="use_bots_with_futures_trading" >Can I use bots with futures trading?</h4>

----

<h4 id="margin_in_docker" >How to run margin in Docker?</h4>

----

<h4 id="ema_bot_work" >How does the EMA crossover bot work?</h4>

----

<h4 id="bollinger_band_bot_work" >How does the Bollinger Band bot work?</h4>

----

<h4 id="margin_maker_bot_work" >How does the mArgin maker bot work?</h4>

----

<h4 id="ping_pong_bot_work" >How does the static ping pong bot work?</h4>

----

<h4 id="invalid_range" >I see an invalid range and can’t place an order</h4>
