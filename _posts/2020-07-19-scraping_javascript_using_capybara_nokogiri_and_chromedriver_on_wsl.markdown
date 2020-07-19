---
layout: post
title:      "**Scraping Javascript Using Capybara, Nokogiri and ChromeDriver on WSL**"
date:       2020-07-19 14:14:27 -0400
permalink:  scraping_javascript_using_capybara_nokogiri_and_chromedriver_on_wsl
---

Hi everyone, I just wrapped up my CLI webscraper project and wanted to share how I was able to scrape a Javascript heavy site using Capybara and Nokogiri. 

I want to start off by saying - doing a Javascript scrape is way more trouble than its worth, especially in the context of this project - however I'd started down a path and felt committed to see it through. I had tons of trouble getting Capybara to work because I was using a Windows Subsystem for Linux and so it literally took me days to even get chromedriver up and running. Here is a detailed step by step guide that might help someone in the same position! 

**There are two major problems you will come across when scraping Javascript with WSL**

1) Scraping a Javascript site using Nokogiri alone is impossible because all the data is dynamic and hidden, therefore you have to use something like Watir or Capybara to interact with the Javascript on the site to reveal the html underneath

2) The Ubuntu WSL has a lot of trouble working with Chromedriver (chromedriver is basically the tool that Capybara uses to open up a site and interact with it) and so one of the biggest challenges for me was getting chromedriver to work.

**Heres how to get chromedriver working on your terminal:**

1) Download a chromedriver: https://sites.google.com/a/chromium.org/chromedriver/ 

- Make sure to check your version of chrome using [Chrome → Help → About Google Chrome] 
- I downloaded the chromedriver_win32.zip file and extracted the exe file to my desktop 

2) Open up the chromedriver on Windows Command Line

- I CD'd into the file path (for me this was C:\Users\Emily\OneDriver\Desktop and the typed chromedriver to actually run the chromedriver. A message that says "Chromedriver was started succesfully" lets me know its working

3) Now, switch to the WSL terminal and incorporate the following code to connect with the chromedriver. You will notice after running this code that a chrome window will pop up by itself and is ready to be operated by Capybara!

   Capybara.register_driver :windows_chrome do |app|
        
				capabilities = Selenium::WebDriver::Remote::Capabilities.chrome()
        puts 'Current driver (windows_chrome) requires chromedriver to be launched from windows      (C:\Users\Emily\OneDrive\Desktop\chromedriver)'
        Capybara::Selenium::Driver.new(app,browser: :chrome, url: 'http://localhost:9515',
                                           desired_capabilities: capabilities)
      end

      Capybara.default_driver = :windows_chrome
      Capybara.javascript_driver = :windows_chrome
      Capybara.default_max_wait_time = 15 # Seconds
      Selenium::WebDriver.logger.level = :debug
      Webdrivers.logger.level = :DEBUG

4) Now you can use Capybara to click on links, close popups and access the HTML on the page. 

- This is a very good intro guide on capybara http://tutorials.jumpstartlab.com/topics/scraping-with-capybara.html
- This is the documentation https://github.com/teamcapybara/capybara

5) Once I loaded up the site I needed through Capybara, I used the .html command to save the current instance of the html into a variable which I could then load and scrape with Nokogiri

- The code looks something like this
(using a Capybara command to save the html) html = browser.html
(loading the html into Nokogiri for scraping) doc = Nokogiri::HTML(html)

From there it is possible to just scrape the html of the site that you loaded. If you want to scrape a different part of the site, you can use capybara again to click different buttons, re-load the html and then use Nokogiri to scrape. 

Hope this helps anyone who is trying to scrape Javascript! 

Emily
