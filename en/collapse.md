
<details>
  <summary><h1 id="get_start" >Getting started on Linux</h1></summary>


1. Download margin-x86_64-4.6.0.AppImage from [BTSE link](https://app.btse.com/download/margin-x86_64.AppImage)
1. Optionally, move and/or rename the newly created folder to where you want margin to reside. A common choice is `~/opt/margin`
1. Go into the *margin* folder and run the file. Before the first run, the icon will be a default icon and not the margin logo shown in the screenshot.
1. Optionally, if you want to copy the .desktop file used to run margin to a different place, e. g. your desktop, or `~/.local/share/applications/` to be seen by your desktop environment, you'll have to change the last line to read something like `Exec=/home/username/opt/margin/margin-x86_64-4.6.0.AppImage`

Adapt for the location you actually put margin in.
</details>

<details>
  <summary><h1 id="setup_linux_vps" >Setting up a Linux VPS to run Margin</h1></summary>

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

```bash
cd Downloads
```

Next, some packages need to be installed in order to run the Margin trading terminal:

```bash
sudo apt install -y xcb* libxcb* libxkbcommon*
```

Finally, run the terminal:

```bash
./margin-x86_64-4.6.0.AppImage
```
</details>

<details>
  <summary><h1 id="machine_sleep" >If my machine goes to sleep, will margin and its bots keep running?</h1></summary>

No, if your laptop goes to sleep the bots will stop working. Amphetamine, NoSleep, and Caffeine are popular apps to stop your machine from going into sleep mode. Otherwise, you can use a VPS. See our other help article: [Can I use a VPS?](#use_vps)
</details>


<details>
  <summary><h1 id="get_error_message" >On Linux I'm getting the error message: Could not load the Qt platform plugin "xcb" in "" even though it was found.</h1></summary>

This error is related to the XCB-Platform plugin of the underlying Qt library. It can be fixed by manually installing all xcb-related packages:

On Ubuntu 18.04, this is:
```bash
sudo apt install libx11-xcb-dev libx11-xcb1 libxcb-dri2-0 libxcb-dri2-0-dev libxcb-dri3-0 libxcb-dri3-dev libxcb-glx0 libxcb-glx0-dev libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-present-dev libxcb-present0 libxcb-randr0 libxcb-randr0-dev libxcb-render-util0 libxcb-render0 libxcb-render0-dev libxcb-res0 libxcb-shape0 libxcb-shape0-dev libxcb-shm0 libxcb-sync-dev libxcb-sync1 libxcb-util1 libxcb-xfixes0 libxcb-xfixes0-dev libxcb-xinerama0 libxcb-xkb1 libxcb-xtest0 libxcb-xv0 libxcb1 libxcb1-dev
```

On Ubuntu 20.04, this is:
```bash
sudo apt install libx11-xcb1 libxcb-dri2-0 libxcb-dri3-0 libxcb-glx0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-present0 libxcb-randr0 libxcb-render-util0 libxcb-render0 libxcb-res0 libxcb-shape0 libxcb-shm0 libxcb-sync1 libxcb-util1 libxcb-xfixes0 libxcb-xkb1 libxcb-xv0 libxcb1
```

If this does not suffice, you can export the following environment variable before starting Margin, which should provide additional help to find out which additional libraries/packages are missing.

QT_DEBUG_PLUGINS=1 ./margin-x86_64-4.6.0.AppImage
</details>


<details>
  <summary><h1 id="cannot_install_margin" >I cannot install margin on my Ubuntu VPS</h1></summary>

  Yes, some VPSs run very minimal versions of Ubuntu that do not contain needed libraries for Margin. If running Margin on Ubuntu produces this

./run-margin.sh: line 30: 2043 Aborted (core dumped) LD_LIBRARY_PATH=$DIR/lib:$LD_LIBRARY_PATH QT_PLUGIN_PATH=$DIR/plugins
./bin/margin.bin

Then please do the following:

```bash
sudo apt install libxcb-xkb-dev libxkbcommon-*
```

Then you should be good to go! Note, if you set up a fresh full version of Ubuntu, these libraries are included and this step is not needed.
</details>


<details>
  <summary><h1 id="os_support" >What operating systems do you support?</h1></summary>

Margin supports Windows, macOS and Linux in the following flavors:

Windows 10 x64
macOS (every version from 10.14 onwards)
Ubuntu 20.04+
</details>

<details>
  <summary><h1 id="use_vps" >Can I use a VPS?</h1></summary>

Yes you can and we recommend it! You can use Microsoft Remote Desktop to connect to your VPS or VPN instance (there are even iOS and Android apps) and check in on how margin is trading for you from your PC, phone or tablet. And what’s more, you won’t need to leave your laptop running 24/7.

A few things to remember.
1. Do not run two instances of Margin in parallel connecting to BTSE with the same API key pair.
1. Make sure to set your VPS instance to the same time as the PC/laptop on which you were running Margin. Otherwise, your API keys might not work.
1. Make sure your API keys do not have withdrawals activated.

If you have any questions, don’t hesitate to get in touch with Margin's customer support.

Note that data usage (if connecting to your VPS instance using a phone or tablet) is pretty high so take care depending on the data plan you have for the VPS.
</details>

<details>
  <summary><h1 id="machine_specs" >What are the minimum machine specs I need?</h1></summary>

We recommend at least 4GB RAM, a Core 2 Duo processor and a HD display for Windows, macOS and Linux systems. It is possible to run Margin on lower spec machines (2GB RAM with a 720p display) but this will restrict the number of pairs/bots that can reasonably be run.
</details>

<details>
  <summary><h1 id="use_bots_with_futures_trading" >Can I use bots with futures trading?</h1></summary>

No, at this time we only support manual trading for the futures market.
</details>

<details>
  <summary><h1 id="margin_in_docker" >How to run margin in Docker?</h1></summary>

Please [follow this link](https://gist.github.com/warp1337/3ebe461af606046f382e50b584705e1c) to run Margin in Docker.
</details>

<details>
  <summary><h1 id="ema_bot_work" >How does the EMA crossover bot work?</h1></summary>

The EMA crossover bot can be started in one of three modes: buy, sell or any. In the 'buy' mode it will wait until a buy situation arises before triggering its first spot order. In 'any' mode it is ready to either buy or sell, whichever situation occurs first.

What triggers a buy?
A buy event is triggered when the short term EMA line crosses the long term EMA line from below.

What triggers a sell?
A sell event is triggered when the short term EMA line crosses the long term EMA line from above.

![image](https://user-images.githubusercontent.com/30857981/176336927-51ce162c-fedb-4a3e-adb0-b11e4857220c.png)

Important details

Please note that in default mode the EMA bot waits for a candle to fully form before calculating the current value of the two EMA lines. The actual value taken for each candle can be configured in the GUI, but the default is to take the closing value. This means that even though a crossover event may have occurred in a particular candle the bot will react one candle later. Reacting within a currently forming candle had the undesired effect of potentially multiple crossover events occurring. It is possible for the bot to react to a crossover event immediately, but we then advise that offsets are used (see Crossover fine tuning below).

It is also important to note that once the bot triggers a buy or sell event it places a spot order. This means that the resulting trade can be displaced from the crossover event due to having to overcome the spread and in cases where there is a shallow order book this can result in many partial order fills.

Crossover fine tuning

It is possible to add a buy or sell offset which provides more confidence that a crossover situation has occurred. These are visualised in the chart as separate lines ensuring you have a visual confirmation of their affect.
</details>

<details>
  <summary><h1 id="bollinger_band_bot_work" >How does the Bollinger Band bot work?</h1></summary>

Margin's Bollinger Band bot is inspired by the John Bollinger's (https://www.investopedia.com/terms/b/bollingerbands.asp ) technical indicator.

The ‘Start with’ combo box (see figure) allows you to start the bot in three modes: buy, sell or any. Starting in any mode will activate both the buy and sell thresholds and is great if you are not sure which way the market will initially move.

Rather than placing limit orders like the static ping pong and mArgin maker bots, the Bollinger Band bot places spot orders. Once the bot triggers a spot order it will place it, which means you need to be prepared that the actual trade might not be at the price the order was triggered at.

How does an order get triggered? There are two bands, a sell band (solid red line) and a buy band (solid blue line), that can be configured. These are set relative to the Bollinger Bands. For an order to trigger, the opposite order book has to intersect the buy/sell band. For example, in the buy case, the top of sell order book has to touch the ‘Current buy threshold’. Note that in volatile markets, this means that it can commonly occur that the order book rapidly retreats after triggering a spot order. This results in the spot order having to overcome the spread to get filled. On certain pairs, this can be some percentage points off the trigger price.

In order to protect against unwanted losses, it is possible to set a Min effective gain parameter. This can be set on both sides. In the figure, the Minimum effective gain displaces the current buy threshold by more than 4% to ensure that the desired Minimum effective gain is achieved.

![image](https://user-images.githubusercontent.com/30857981/176337131-20d2aae7-6f6f-4411-92e0-6985fd3c525d.png)

In the figure above, a minimum effective gain ensures that the bot does not buy back too soon in a market that had trended upwards. Also, note that the two sell trades (small yellow triangles) went through above the Bollinger Band sell threshold because of the Min effective gain setting.

Stop-loss is also available on both sides. On the buy-side, a stop loss can be set up relative to the last buy the bot performed. This is visualized in the chart and the percentage can be manipulated by dragging the annotation up or down. Note that if a stop loss is triggered, the bot will stop trading.
</details>

<details>
  <summary><h1 id="margin_maker_bot_work" >How does the mArgin maker bot work?</h1></summary>

The mArgin maker bot is a dynamic bot that places limit orders.

There are several parameters you can set, some of which can be set directly in the chart. The ‘time window’ is set by dragging the long vertical blue line (see image below - it’s the thin blue line in the middle of the chart running from top to bottom) to determine what time period is desired. The vertical height of the time window is given by the lowest and highest priced trades that occurred during that time.

Inside this window, the relative buy and sell margins can be set (dashed red horizontal lines). As the lowest and highest trade price will change over time, the vertical height of the window changes accordingly, which in turn means the buy and sell margin prices will change. As the market contracts, the prices become closer to each other. This also means that the initial Eff. gain* shown in the center of the time window will also change.

![image](https://user-images.githubusercontent.com/30857981/176337251-b2f52180-be03-4eb7-899a-d84714dfc1b5.png)

The Min. effective gain [%] is a very important parameter. For the mArgin maker, it applies to both buy/sell and sell/buy cycles. It is always active, with the default value being 0.0%. If you want to ensure that the bot makes a gain after trading fees have been subtracted, a positive value must be given. Note that this means a bot order can get stuck at a particular price in order not to violate the Min. effective gain.

The other parameters are quite self-explanatory, especially if you hover over their tooltips.

Stop-loss can be enabled and then adapted in the chart. If a stop-loss event occurs, the bot will accept the user-specified loss by triggering a spot sell order, and then the bot stops.
</details>

<details>
  <summary><h1 id="ping_pong_bot_work" >How does the static ping pong bot work?</h1></summary>

The static ping pong bot places limit orders.

This is the simplest bot in Margin. Click on the strategy button (chess knight with +) to create a new bot. Initially, it will default to an effective gain of 0.1% around the spread. Click and drag the buy and sell price lines to set the prices you want. The bot waits until its order is fully filled before switching actions and then places a limit order on the opposite side. In the example below, the bot has just placed a limit buy order and is waiting for the order to become active. If this order gets filled, a limit sell order for the same amount will be placed on the opposite side. Here, we’ve specified an effective gain of just over 3%.

![image](https://user-images.githubusercontent.com/30857981/176337356-d1e8d273-8067-401e-a25a-790f26a86f7c.png)

The bot will continue to trade until you explicitly stop it.
</details>

<details>
  <summary><h1 id="invalid_range" >I see an invalid range and can’t place an order</h1></summary>

This occurs because you do not have enough funds to place even the minimum allowed order. For example, for a BTC/USD market, if you see an invalid range in Margin, it means in the ‘buy’ case that you do not have enough USD and in the ‘sell’ case enough BTC to place the minimum order possible.

Note that some bots require you to have a little more than the minimum in order to overcome trading fees and continue trading. That means it is possible to have enough funds to place a manual trade but not start a bot in some cases.
</details>
