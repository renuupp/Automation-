# Automation-
package TestCases;

import java.util.concurrent.TimeUnit;
import org.junit.Assert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.PageFactory;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

public class Account_Fields {
     private Account acct = null;
     static WebDriver driver = null;
     static WebElement click;
     static WebElement submit; 
     private WebElement Account, Website, TopAccount;
     Select Type, SubType;
     
     @FindBy(xpath = "//a[contains(text(), 'U-FUEL INC')]")
 	 WebElement ele;
     
    @BeforeClass
    public void beforeClass() {
    	 
    	 System.setProperty("webdriver.chrome.driver", "C:/Program Files (x86)/Google/Chrome/Application/chromedriver.exe");
	  	 driver = new ChromeDriver();
	  	 driver.get("www.scottrade.com/");	    
	   	 acct = PageFactory.initElements(driver, Account.class); // Initialize the Account class  
	  	 driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	   	 pg.HomePageLogon();
    }
     
    @Test
    public void testCase() {
    	try {
    		// invoking account tab.
    		acct.selectAcctTab();        	
        	//Account = driver.findElement(By.xpath("//a[contains(text(), 'opening an account')]"));
        	Account = driver.findElement(By.xpath("//*[@id='bodyCell']/div[3]/div[1]/div/div[2]/table/tbody/tr[2]/th/a"));
        	Account.click();
        	acct.clickEdit();
        	// Invoking Type and SubType Dropdown menu
        	Type = new Select(driver.findElement(By.id("acc")));
        	//Type = driver.findElement(By.xpath("//*[@id ='acc6']"));
        	Type.selectByIndex(1); // 1 (3PL) is for selecting first field in Type drop down menu 
        	SubType = new Select(driver.findElement(By.id("00NZ0000001"))); 
        	//SubType = driver.findElement(By.xpath(".//*[@id='00NZ0000001RmPM']"));
        	SubType.selectByIndex(2);
        	Website = driver.findElement(By.xpath(".//*[@id='acc12']"));
        	//Website = driver.findElement(By.id("acc12"));
        	Website.sendKeys("https://www.google.com");
        	TopAccount = driver.findElement(By.id("00NZ0000001RO")); 
        	TopAccount.click(); 
        	acct.clickSave(); 
        	Assert.assertTrue(acct.getAccountTab().isDisplayed());
  		} catch (Exception e) {
  			e.printStackTrace();
  		}    	
	}
    
    @AfterClass
  	public void afterClass() {
	  driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
	  //pg.HomePageLogout();
