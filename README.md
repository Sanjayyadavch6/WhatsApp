import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class WhatsAppWebAutomation {
  public static void main(String[] args) {
    // Set the path to the ChromeDriver executable
    System.setProperty("webdriver.chrome.driver", "D:\\\\Selenium Drivers\\\\Chrome Driver\\\\chromedriver.exe");

    // Create a new instance of the ChromeDriver
    WebDriver driver = new ChromeDriver();

    // Navigate to the WhatsApp Web website
    driver.get("https://web.whatsapp.com/");

    // Wait for the QR code to load
    WebDriverWait wait = new WebDriverWait(driver, 10);
    wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//div[@title='Scan me!']")));

    // Use your phone to scan the QR code displayed in the browser

    // Wait for the chat list to load
    wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//span[@title='Contact Name']")));

    // Find the desired chat and click on it
    WebElement chat = driver.findElement(By.xpath("//span[@title='Contact Name']"));
    chat.click();

    // Wait for the input field to load
    wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//div[@contenteditable='true']")));

    // Find the input field and send a message
    WebElement inputField = driver.findElement(By.xpath("//div[@contenteditable='true']"));
    Actions actions = new Actions(driver);
    actions.moveToElement(inputField);
    actions.click();
    actions.sendKeys("Hello, this is a test message");
    actions.build().perform();

    // Find the send button and click on it
    WebElement sendButton = driver.findElement(By.xpath("//span[@data-icon='send']"));
    sendButton.click();

    // Verify that the message was sent
    wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath("//span[text()='Hello, this is a test message']")));
    WebElement sentMessage = driver.findElement(By.xpath("//span[text()='Hello, this is a test message']"));
    if (sentMessage.isDisplayed()) {
      System.out.println("Message sent successfully");
    } else {
      System.out.println("Message failed to send");
    }

    // Close the browser
    driver.quit();
  }
}

