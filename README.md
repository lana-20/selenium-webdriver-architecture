# Selenium WebDriver Architecture

- What is a WebDriver?
- Architecture of WebDriver
- Selenium 3 vs Selenium 4
- Setup Selenium with Python Project
- Write a Test Case

## What is a WebDriver?

Selenium contains multiple components - IDE, WebDriver, RC, Grid.
The most popular component is Selenium WebDriver. I use it to automate web apps. Selenium on its own only supports web apps.
WebDriver is a package/module in respect to Python. In Java, I'd call it an interface. Module contains functions, classes, classes contain different types of methods.
WebDriver module contains a number of classes. Eg, for each browser there's a class availabe:
- Chrome Browser -> Chrome()
- Firefox Browser -> Firefox()
- Edge Browser -> Edge()

There are other browsers available with their respective classes in WedDriver module.

I have to import WebDriver module to obtain access to all these classes or class methods, in order to automate test cases.

WebDriver is an API (Application Programming Interface).
In a web app, there are multiple layers/tiers.
![image](https://user-images.githubusercontent.com/70295997/205237418-dda18f95-596b-4475-8054-1757249d8bca.png)

Suppose I want to open amazon.com. I send the amazon.com URL in the browser and get some info back. From some web or app server I'm getting back this data, I'm seeing all the elements (searchbox, dropdowns, etc.). When I send a Request, I get a Response back. the component called Business Logic (API) receives these Requests and Responses, processes a Request, sends back a Response. It's known as Business Login in a sense that it contains an n-number of programs. Based upon the Request I send, accordingly, a particular logic gets executed. API forwards this same Request to the Backend Database Layer. API receives a Response back from the DB and, again, forwards the Response back to the Presentation Layer in a user-undertandable format. Business Logic contains a lot of programs developed by devs in programming languages. Business Logic is divided into  multiple Classes or APIs. All Business Logic can be called as APIs.
![image](https://user-images.githubusercontent.com/70295997/205237523-f14a4f88-988a-4cc3-ad35-0a11b43318dd.png)

API acts as a mediator between Presentation Layer and Backend Layer. Every app internally has many APIs. 

When I conduct testing in the UI/Presentattion Layer area, I call it GUI Testing. Normally, I do this with browsers using Selenium. It's __Browser-level GUI Testing__.

Whenever I conduct testing directly in the Business Logic Layer, I call it __API Testing__. I test APIs directly by passing some input to the API, getting a Response back, and, again, directly verify/validate the Response. For API Testing I use Postman, RestAssured, Carate, etc. There are many tools available in the marketplace.

In the Backend Layer, I conduct __Database/Backend Testing__.

When I run End-to-End (e2e) Tesintg on the app, I conduct (1) UI, (2) API, and (3) Database/Backend testing.

Performance Testing or Security Testing is there on every level/tier of the app. These are Non-Fuctional types of testing.

As for the Functional testing, I conduct 3 different types of testing on 3 main layers/tiers - GUI, API, DB.

Each layer is different, as well as the tools applcalbe to it. By using a single tool, I can't do everything. There are tools available to support all sorts of testing.
- Selenium - is specifically and only for GUI testing
- Postman, RestAssured, SoapUI - are for API testing
- TOAD or another client - is for DB testing

The main importance of API is that, first, it gets a Request from the User, sends the same Request to the Database Layer which processes the data. Then API gets the Response and presents the same Response to the Presentation Layer. And that is the Response variable I see in the UI. Based on this understanding, why is WebDriver an API? For that I need to understand the architecture of Selenium WebDriver and how WebDriver works internally. Accordingly, I'll be able to understand why WebDriver is an API.
![image](https://user-images.githubusercontent.com/70295997/205237705-214914ef-4bc9-441f-8d5f-d9cf405b9444.png)

Automation scripts can't directly talk to the Browser level, on which AUT runs. All web apps would run on a browser, because this is a GUI-level test. To run test cases, I write some automation code, different statements in Python (or Java, etc.). When I execute my automation script, whatever actions I've written in the code are performed on the Applicatin in the browser. Suppose there's a Login box and I want to enter username and password in text boxes. When I run my automation script, it seems similar to a Python program -> actions get performed on the Browser level.

Who performs these actions, how does my Automation Code talk to the Browser? Since automation scripts can't directly talk to the Browser, internally I need another layer. That layer is WebDriver [API]. WebDriver contains many classes and methods, to which I refer to inside of the program (automation code). My Automation Code, first, talks to the WebDriver. And the WebDriver methods, in their turn, directly execute the statements in the AUT.

Since WebDriver can't directly talk to the Browser, Browser Drivers are required. Wuthout Browser Drivers, even WebDriver API can't directly talk to the Application [Under Test].

Whatever statements I write in my Automation code are taken by the WebDriver. WebDriver takes these statements and comprehends them. Accordingly, WebDriver executes the statements in my Application [Under Test]. WebDriver acts as an API between my Automation and the Browser. That's the reason I can call it as __WebDriver API__. WebDriver API contains many classes I can use and methods I can call. That way, I'm able to interact with the Browser. And the actions, derived from my Automation Scripts, are performed on the Application [Under Test]. Here, WebDriver is an API.

How does WebDriver internally talk to the Browser?
For that, I need to understand the Architecture of the WebDriver.

## Architecture of WebDriver

There are differences [on architectural levels] between Selenium versions 3 and 4 Architecture Types. Selenium 4 has some new changes and features.
![image](https://user-images.githubusercontent.com/70295997/205237817-7bc058b3-da6c-48b8-a90c-bb8b6bf91138.png)

In Selenium 3 Architecture, there is a Selenium Client Library. WebDriver provides a certain number of jar files, class files, etc., called a Client Library. When I write the [Automation Code] program, I use different Classes and call different types of Methods, which belong to WebDriver [API module]. All these classes and methods come under Selenium Client Library.
Selenium supports Python, Java, Ruby, C#, and other languages, hence Selenium Classes and Methods are implemented in multiple languages. When I program in Python to customize test cases, I use that particular Selenium Library. This library is a simple program, like some automation code I've sritten in Python. I can call it a Python Client Library.

How does my Python code interact with the Browser?
My Automation Code internally calls WebDriver Methods. And these Methods directly communicate with the Browser. But this still is not a direct connection. Internally, under the hood, a lot of things happen, which I can't observe externally, physically. There are protocols and drivers between the WebDriver [API module] Layer and Browser/AUT Layer. Only with these Protocols and Drivers can the Automation Code (Client Library) Layer and the Browser [AUT] Layer talk to each other. My (Client Library) program can't directly talk to the Browser(s).

First, I need browser-specific Drivers. For each browser, there is a driver. And that driver is availalbe in the form of an exexutable file. Eg, if I want to work in Chrome, I need chromedriver.exe file. In order to work with this browser, I need to download the browser-specific drivers to my local machine. Without these Drivers, I can't directly communicate with the Browsers.

These Drivers are not implemented or maintained by Selenium, but by their own respective software companies. Eg, Microsoft implements the Edge driver, Google - Chrome driver, Mozilla - Firefox, etc. These Drivers are available for use, I just need to get them.

My Automation Code talks directly to the Driver, it invokes the Driver through JSON protocol. JSON protocol is a common language for different Selenium Client Library languages. It allows my commands to process and call the browser-specific Drivers. Communication between mu Client Library and browser-specific Driver happens via JSON Wire Protocol.

Browser-specific Drivers talk to Browsers using W3C (World Wide Web Consortium) Protocol. W3C Protocol contains a number of standards which a wep app should follow. Browsers and Drivers follow the W3C collection of standards/guidelines/rules/regulations.

Because the W3C Protocol is used between Drivers and Browsers, and JSON Wire Protocol - between Client Library and Drivers, there are some stability and performance related issues. Sometimes test case execution may fail without a reason. Because of these issues, protocola got changed in Selenium 4. 

## Selenium 3 vs Selenium 4

Selenium 4 replaced JSON Wire Protocol with W3C Standard Protocol. Drivers started communicating with Client Library over W3C. Now, all the Layers (Client Library, Drivers and Browsers) use the same (single) W3C protocol.
![image](https://user-images.githubusercontent.com/70295997/205237900-86f700b7-d86b-492d-ac7b-3600d1a726fc.png)

Through this architectural change, Selenium solved the instability issues and also made the communication faster. Aside from that, internally there are no more changes. Although, in addtion, to solving the stability performance issue, Selenium 4 introduced some new features.
![image](https://user-images.githubusercontent.com/70295997/205237971-70d2109e-a073-4d88-80b6-e89d1db464b2.png)

First, download and configure the Selenium Client Library. Then download the Drivers from Selenium > Downloads > Browsers. And then install 3+ Browsers to conduct cross-browser testing (by runnung the same test cases on multiple browsers).

## Setup and Configure WebDriver in PyCharm

No need to download/install anything, except Python and PyCharm. These are the pre-requisites to setup and condigure WebDriver in PyCharm directly.

Driver Downloads -> https://www.selenium.dev/downloads/. The official Selenium website provides available language bindings.
Selenium Clients and WebDriver Language Bindings: Python, Java, C#, Ruby, JavaScript, etc. I use Python (stable version 4.7.0).

There are various ways to install and configure Selenium WebDriver. Pre-requisites for Selenium are Python and PyCharm. Also, before installing Selenium, I need to have browser-specific drivers. When I work with 3 different browsers, I need to download those 3 respective drivers to my local machine.

1) Download browser-specific Drivers from the official Selenium website or the following links:
- Chrome: https://chromedriver.chromium.org/downloads (latest ChromeDriver version is 109)
- Edge: https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/ (latest EdgeDriver version is 107)
- Firefox: https://github.com/mozilla/geckodriver/releases (latest GeckoDriver version is0.32)
- Safari: https://webkit.org/blog/6900/webdriver-support-in-safari-10/ and https://developer.apple.com/documentation/webkit/about_webdriver_for_safari

Eg, I can go to the ChromeDriver link and download a version compatible my current Chrome Browser (version 108 as of 12/02/222). However, ChromeDriver version 109 is already released. Drivers get developed first, Browsers come later.


2) Setup WebDriver Movule
3) ...


## Write a Test Case

