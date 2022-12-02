# Selenium WebDriver Architecture

- What is a WebDriver?
- Architecture of WebDriver
- Selenium 3 vs Selenium 4
- Setup Selenium with Python Project
- Write a Test Case

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

Automation scripts can't directly talk to the Browser level, on which AUT runs. All web apps would run on a browser, because this is a GUI-level test. To run test cases, I write some automation code, different stataments in Python (or Java, etc.). When I execute my automation script, whatever actions I've written in the code are performed on the Applicatin in the browser. Suppose there's a Login box and I want to enter username and password in text boxes. Who performs these actions, how does my Automation Code talk to the Browser? Since automation scripts can't directly talk to the Browser, internally I need another layer. That layer is WebRiver [API].



![image](https://user-images.githubusercontent.com/70295997/205237817-7bc058b3-da6c-48b8-a90c-bb8b6bf91138.png)
![image](https://user-images.githubusercontent.com/70295997/205237900-86f700b7-d86b-492d-ac7b-3600d1a726fc.png)
![image](https://user-images.githubusercontent.com/70295997/205237971-70d2109e-a073-4d88-80b6-e89d1db464b2.png)

