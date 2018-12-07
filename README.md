# 0xbtc-discord-price-bot
bot to monitor/post price etc to the 0xbtc discord server

##### Installation:

1. Clone this repository
2. Install python 3.6 (NOT 3.5 or 3.7)
   - For debian 9 users: Debian 9 repositories only go up to python 3.5, so to
     install the latest 3.6.x python version:
     - `sudo apt install build-essential checkinstall libreadline-gplv2-dev 
        libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev 
        libc6-dev libbz2-dev libffi-dev`
     - `wget https://www.python.org/ftp/python/3.6.7/Python-3.6.7.tgz`
     - `tar xf Python-3.6.7.tgz`
     - `cd Python-3.6.7/`
     - `./configure --enable-optimizations --with-ensurepip=install`
     - `make -j2` (or `make -j8` if you have a cpu with lots of threads)
     - `sudo make altinstall`
3. run `pip3 install -r requirements.txt`
   - For for Windows Users: This command failed for me with error:
   `error: command 'C:\\Program Files (x86)\\Microsoft Visual Studio 14.0\\VC\\BIN\\link.exe' failed with exit status 1158`
   - The fix: Copy rc.exe and rcdll.dll from `C:\Program Files (x86)\Windows Kits\8.1\bin\x86` to `C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin`
4. copy `template_secret_info.py` to `secret_info.py` and fill in your bot's authentication settings
5. edit `configuration.py` (you can run the bot with `--show_channels` to get channel IDs)
6. (Optional) edit `exchanges` list at the end of `main.py`
7. (Optional) run `python3 /path/to/price-bot/ --self_test`
8. run `python3 /path/to/price-bot/`

##### Requires:
 - python3
 - websocket
 - discord
 - web3.py
 - BeautifulSoup (only if !holders command is enabled)
 - matplotlib (only if !holders command is enabled)

##### Bugs:
 - bot creates the 'databases' folder in a location relative to the current
   directory, rather than the location of the bot code
 - occasionally APIs return NaN as a data point.. which is a valid float. Need
   to explicitly check for this.

##### Todo:
 - exchange module
   - switch over all apis to use \_get_json_from_url in exchange base class
   - remove `if __name__ == "__main__":` checks from exchanges or figure out
     a way to keep and still test them individually
     `cd 0xbtc-discord-price-bot; python -m exchanges.mercatox`
 - make configuration text-based so it does not need python imports etc
 - add keyboard shortcuts / letters (ie press 'c' to show all channels)
 - update from async to rewrite branch of discord.py [link](https://github.com/TheTrain2000/async2rewrite)
   `pip install -U git+https://github.com/Rapptz/discord.py@rewrite#egg=discord.py[voice]`
 - generalize command categories (currently only trading and global)
 - new commands
   - !binance (to show current listing price in usd)
   - !orderbooks mercatox
 - Need a new 'Pairing' class to handle pairings in a more generic way. This
   will allow easier integration of BTC pairings (ie mercatox)
 - volume_eth and volume_usd are not strictly defined - sometimes it means total
   volume across all pairs (converted to eth), sometimes it means volume in eth
   only and volume_btc means volume in btc only.
 - 24h high/low/average
 - ascii chart?
 - enable hotbit?
 - new exchanges
   - tokenjar [link](https://tokenjar.io/0xbtc)
   - tokenstore [link](https://token.store/trade/0xBTC)
   - payfair [link](https://payfair.io/?coin=0XBTC&tradeType=sell&currency=USD)
   - instex [link](https://app.instex.io/0xBTC-WETH)
   - cryptobridge (not yet)
   - ddex.io
   - Rootrex
