---
layout: post
title: "Running Selenium Webdriver on Bash for Windows"
categories:
  - Programming
  - Linux
  - Testing
image: assets/images/selenium.png
description: "Running Selenium WebDriver with Firefox on WSL (Bash for Windows) using Xming and geckodriver"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2017/06/18/running-selenium-webdriver-on-bash-for-windows/](https://blog.henrypoon.com/blog/2017/06/18/running-selenium-webdriver-on-bash-for-windows/)

**NOTE:** This article is for WSL1. For WSL2, see my updated post: [Running Selenium Webdriver on WSL2]({% post_url 2020-09-27-running-selenium-webdriver-on-wsl2 %})

Bash for Windows had been working great for me until I needed to run Selenium WebDriver on it. I quickly learned that it would not work right out of the box, and the setup for it is quite convoluted.

You will need:

- [Bash for Windows](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
- [Xming](https://sourceforge.net/projects/xming/) - This allows the browser window to appear on the screen
- [geckodriver](https://github.com/mozilla/geckodriver/releases) - Selenium needs this to run Firefox

## Bash setup

Install Firefox:

```bash
sudo apt-get install firefox
```

Export the DISPLAY variable in `~/.bashrc`. Just add this to `~/.bashrc`:

```bash
export DISPLAY=:0
```

## Xming setup

Download Xming from the link above and run it.

## Download geckodriver

Download geckodriver from the link above and place it in the `/usr/bin/` folder in Bash for Windows.

## Running Selenium

Here is a piece of sample Python code I used to set up the web browser. It will set up the browser, open Google, sit there for 10 seconds, and then quit. Make sure to have Xming running, otherwise the browser will not start.

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
