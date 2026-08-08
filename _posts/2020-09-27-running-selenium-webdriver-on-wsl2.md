---
layout: post
title: "Running Selenium Webdriver on WSL2"
categories:
  - Programming
  - Linux
  - Testing
image: assets/images/ubuntu_selenium.png
description: "Running Selenium WebDriver with Firefox on WSL2 using VcXsrv and geckodriver"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2020/09/27/running-selenium-webdriver-on-wsl2/](https://blog.henrypoon.com/blog/2020/09/27/running-selenium-webdriver-on-wsl2/)

This is a newer version of my earlier post on [running Selenium on WSL1]({% post_url 2017-06-18-running-selenium-webdriver-on-bash-for-windows %}), updated for WSL2. The instructions follow the same high-level approach but include some additional gotchas specific to WSL2.

You will need:

- [WSL2 setup](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) with Firefox installed (I used Ubuntu 20.04)
- [VcXsrv](https://sourceforge.net/projects/vcxsrv/)
- [geckodriver](https://github.com/mozilla/geckodriver/releases)

## How it works

VcXsrv starts up an X server on the Windows host machine. WSL connects to this server to pass on the details of what programs need to be displayed - in this case, the browser window. Geckodriver acts as a middle layer that allows Selenium to interact with Firefox.

## VcXsrv setup

This sets up the X server so that Windows can display graphical data coming from the Ubuntu instance.

1. Download and install VcXsrv
2. Start it up with the command line parameter `-ac`. This flag removes access control restrictions for connecting clients (safe as long as the server is not exposed on the open Internet and the only client connecting is the Ubuntu instance)
3. Allow connections to VcXsrv on Windows Firewall

The `-ac` flag and allowing the program through Windows Firewall are critical. Without these, Ubuntu produces cryptic error messages like "Broadway display type not supported". Once access controls are properly configured, everything works.

## Bash setup

Install Firefox:

```bash
sudo apt install firefox
```

Export the DISPLAY variable in `.bashrc` (or `.zshrc` or whatever terminal configuration file you use):

```bash
export DISPLAY=$(ip route | awk '{print $3; exit}'):0
```

This configures the DISPLAY variable to use the IP address listed in `resolv.conf`. That IP address is the address of the X server that will be used for displaying the browser window.

Start up VcXsrv as described above and then try to open Firefox. The Firefox window should open on your Windows desktop.

## Geckodriver setup

Geckodriver acts as the API interface that allows Selenium to interact with Firefox. Selenium looks for this executable when controlling the web browser.

1. Download geckodriver (make sure to get the **Linux** version, not the Windows one)
2. Place it in `/usr/bin` (or alternatively some other folder in your PATH)

## Selenium sample on Python

I tend to use Python with Selenium, though the principles are similar for other languages. Here is sample code for starting up the browser and opening a website:

```python
import time

from selenium import webdriver
from selenium.webdriver import DesiredCapabilities

def execute_with_retry(method, max_attempts):
    e = None
    for i in range(0, max_attempts):
        try:
            return method()
        except Exception as e:
            print(e)
            time.sleep(1)
    if e is not None:
        raise e

capabilities = DesiredCapabilities.FIREFOX
capabilities["marionette"] = True
firefox_bin = "/usr/bin/firefox"
browser = execute_with_retry(lambda: webdriver.Firefox(
    firefox_binary=firefox_bin, capabilities=capabilities), 10)

browser.get("https://www.google.com")

time.sleep(10)

browser.close()
```

This will open Firefox and navigate to Google, then close after 10 seconds. Any standard Selenium code can be used once the setup is complete.
