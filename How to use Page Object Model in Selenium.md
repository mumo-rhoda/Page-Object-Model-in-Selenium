## Code Optimization in Selenium WebDriver using Page Object Model
One of the best ways to optimize code in Selenium and make sure your code is efficient and  runs as quickly as possible using as little memory is to use the Page Object Model. This will help to organize your code and make it more readable and maintainable. 

There are many ways to use the Page Object Model in Selenium, but one of the most common is to create a Page Object for each page in your application. This allows you to group all the elements and functionality for a particular page in one place, making your code more readable and maintainable.

In this tutorial we are going to practically learn how to achieve improved test automation results in Selenium using the Page Object Model.
### What is the Page Object Model?
The Page Object Model is a design pattern that helps make your code more maintainable and easier to read. It's commonly used in Selenium tests, but can be applied to any automated testing tool.

Some advantages of using the Page Object Model include:

- You can reuse page objects in multiple tests.
- Your tests are less susceptible to changes in the UI.
- Your code is more maintainable and easier to read.

## Prerequisites
A general knowledge of Selenium WebDriver, Java, Maven and Intellij IDE.
Test website access [saucelabs](https://www.saucedemo.com/)
For a comprehensive undertanding on how to setup selenium WebDriver and install Intellij explore this [page](https://www.guru99.com/intellij-selenium-webdriver.html).

### Step by Step implementing Page Object Model using Selenium Webdriver
To implement the Page Object Model using Selenium Webdriver, you'll need to take the following steps:

1. Create a New Maven Project as shown below:
![New-project](/pictures/newproject1.png) 
*A new maven project and latest JDK version.*
2. Make sure your dependecies are well set as shown below: All dependeices can be found in [ Maven-repository](https://mvnrepository.com/)
 ![Pom-Depedencies](/pictures/pomdependencies.png)
*Selenium dependency, webDriver Manager dependency.*
3. Come up with clear structure and configure the static properties as shown below;
![New-project](/pictures/config.properties%20and%20structure.png) 
4. Setting up Base class. All classes extend the base class. This is how your base class should be structured;

'''package BaseClass;

import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.time.Duration;
import java.util.Properties;

public class BaseClass {

    public static Properties prop;
    public static WebDriver driver;

    // load configuration properties url, username, password and browser
    public void loadConfig(){
        try {
            prop = new Properties();
            System.out.println("super constructor invoked");
            FileInputStream ip = new FileInputStream("Configurations/Config.properties");
            prop.load(ip);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
    //launching our test website
    public static void launchWeb() {

        if (prop.getProperty("browser").equalsIgnoreCase("edge")) {

            WebDriverManager.edgedriver().cachePath("drivers").setup();
            driver=new EdgeDriver();
        } else if (prop.getProperty("browser").equalsIgnoreCase("Firefox")) {
           WebDriverManager.firefoxdriver().cachePath("drivers").setup();
            driver = new FirefoxDriver();
        }
        //Maximize the screen
        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(20));
        driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(10));
        //Launching the URL
        driver.get(prop.getProperty("url"));

    }
}
'''

5. Create a Page Object class for each page in your application and use Page Factory to find all the Object Elements and initialize them;
![PageObjects-Page Factory](/pictures/LoginPageObjectClass.png) 
![CheckoutPageObject, methods](/pictures/CheckoutPageObjectClass.png)

6. In the test script,  Call the methods on the Page Object instances to interact with the page elements.create an instance of the Page Object class for each page as shown below;

![HomeTestcase](/pictures/HomeTest.png)
![CheckoutTest, cases](/pictures/CheckoutTest.png)
7. Come up with TestNg.xml file.
    TestNG.xml file is a configuration file that helps in organizing our tests. It allows testers to create and handle multiple test classes, define test suites and tests. Then run your test cases.
    ![TestNg file](/pictures/Testngf.png)

## Conclusion.
The Page Object Model is a great way to create tests that are easy to maintain and will allow you to scale your testing efforts faster, as you can reuse the object as required for any test automation flow.
