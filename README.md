# STEP BY STEP
## 1. Set Up
### - Installing Java 11
### - Installing IntelliJ
### - Installing Chrome Browser
### - Installing Chrome Driver
### - Creating a New Project
- We want to create a Maven project.
>  In here, they're going to ask you for a GroupId and an ArtifactId.
Next it will ask you the location of where you want to store the project.
Now there are a couple of things we want to add into here — the first thing we want to add is the properties.

`<properties>
    <maven.compiler.target>1.12</maven.compiler.target>
    <maven.compiler.source>1.12</maven.compiler.source>
</properties>`

***note**: en Intellij 2023 version properties are added by default.*
- The next thing we want to do is to add dependencies because we're using Selenium WebDriver.
- Okay, let's paste this under the properties and we notice that we get a little error.
That's because this needs to be in dependency section.
- Create new resources directory 
---------------

### 2. WebDriver
- Okay, so we're going to create a new class.
	-  Under this source directory, we have a “main” directory and a “test” directory. We're going to create one under the test and we have this Java folder. We'll just right click on the Java folder, select “new" and select *“Package”.*
	- We're going to create a package here called “base”. Inside of the base package we'll create a new Java class, and this one we'll call "BaseTests".

- Now inside of here, the very first thing I want to do is create a WebDriver object.
	- Let's go ahead and say `private WebDriver driver`. We'll go ahead and import the WebDriver.

- Next I want to create a method — we'll just call this **setUp**.
	Inside of here, Selenium WebDriver is going to need to know where is that executable file that you have, because I need it in order to run. We do this using a **System.setProperty()** and we give this the name of the property. And this property that Selenium will look for is called webdriver.chrome.driver, and it must be specified exactly like this because this is what Selenium will look for. This is like a key.

	Next we do a comma, and the next argument here needs to be the location of that chromedriver file.

	Remember we placed it in this “resources” directory so we can simply say, look in the “resources” directory and the file is called **chromedriver**.

```java
public void setUp(){
    System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
}
````
> **Windows Users**
If you are on Windows, you need to also add an “.exe” here [ chromedriver.exe ], but only if you're on Windows. If not, your file is just called chromedriver

- After we've set up the property, now let's go ahead and instantiate this WebDriver object.
	You can specify what type of driver you like to use. Now we have downloaded the chromedriver, so that's the one we want to use, but there are other options as well for the different browsers.

	The WebDriver that we're using is an interface, so we're using it as a type, but we must instantiate it using one of the  [implementing classes](http://https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/WebDriver.html "implementing classes")  There are multiple ones:

	- ChromeDriver, which we'll use
	- EdgeDriver for the Edge browser
	- FirefoxDriver
	- InternetExplorerDriver
	- OperaDriver
	- SafariDriver
	- RemoteWebDriver

Let's go ahead and instantiate our driver as a **ChromeDriver**, so, we say:
````java
driver = new ChromeDriver();
````
- Let's look at the application that we want to launch.
````java
driver.get("https://the-internet.herokuapp.com/");
````

- Now just to make sure that the browser does launch and that it actually loads to this application, let's write one more command to print something out.
````java
System.out.println(driver.getTitle());
````

- In order to run this, we'll need a main method just because we haven't set up our project to do any test runs just yet.
````java
public static void main(String args[]){
     BaseTests test = new BaseTests();
     test.setUp();
}
````
> **Note**
There are some other outputs here that are in red. If this is your first time using ChromeDriver, this may seem alarming to you because it's in red and red usually means a type of error. But rest assured, this is not an error, this is just information being printed out and we can ignore it.

- We might want to close the browser as well because we have it left hanging open.
````java
driver.quit();
````
- Maybe you want to do things like change your window size before you start doing your testing.
````java
//1 - Maximize the window
driver.manage().window().maximize();
````
- Another option is fullscreen mode.
````java
//2 - Fullscreen mode
driver.manage().window().fullscreen();
````

- What if you have a specific size you want the browser to be in?
````java
//3 - Specific width (show Chrome iPhoneX emulator)
Dimension size = new Dimension(375, 812);
driver.manage().window().setSize(size);
````
### BaseTests.java
````java
package base;

import org.openqa.selenium.Dimension;

import org.openqa.selenium.WebDriver;

import org.openqa.selenium.chrome.ChromeDriver;

public class BaseTests {

    private WebDriver driver;

    public void setUp(){
        System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://the-internet.herokuapp.com/");

        //1 - Maximize the window
        driver.manage().window().maximize();

        //2 - Fullscreen mode
        driver.manage().window().fullscreen();

        //3 - Specific width (show Chrome iPhoneX emulator)
        Dimension size = new Dimension(375, 812);
        driver.manage().window().setSize(size);
        System.out.println(driver.getTitle());
        driver.quit();
    }

    public static void main(String args[]){
        BaseTests test = new BaseTests();
        test.setUp();
    }
}
````







