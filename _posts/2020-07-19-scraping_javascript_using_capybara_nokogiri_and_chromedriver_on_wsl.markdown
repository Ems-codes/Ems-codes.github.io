---
layout: post
title:      "**Scraping Javascript Using Capybara, Nokogiri and ChromeDriver on WSL**"
date:       2020-07-19 18:14:26 +0000
permalink:  scraping_javascript_using_capybara_nokogiri_and_chromedriver_on_wsl
---

Hi everyone, I just wrapped up my CLI webscraper project and wanted to share how I was able to scrape a Javascript heavy site using Capybara and Nokogiri. 

I want to start off by saying - doing a Javascript scrape is way more trouble than its worth, especially in the context of this project - however I'd started down a path and felt committed to see it through. I had tons of trouble getting Capybara to work because I was using a Windows Subsystem for Linux and so it literally took me days to even get chromedriver up and running. Here is a detailed step by step guide that might help someone in the same position! 

**There are two major problems you will come across when scraping Javascript with WSL**

1) Scraping a Javascript site using Nokogiri alone is impossible because all the data is dynamic and hidden, therefore you have to use something like Watir or Capybara to interact with the Javascript on the site to reveal the html underneath

2) The Ubuntu WSL has a lot of trouble working with Chromedriver (chromedriver is basically the tool that Capybara uses to open up a site and interact with it) and so one of the biggest challenges 

**Heres how to get chromedriver working on your terminal:**

1) Download a chromedriver: https://sites.google.com/a/chromium.org/chromedriver/ 

- Make sure to check your verison of chrome using [Chrome → Help → About Google Chrome] 

2) # Enter your title here

The content of your blog post goes here.
