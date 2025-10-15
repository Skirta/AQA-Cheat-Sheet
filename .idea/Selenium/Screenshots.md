# 📸 Screenshots

#### 📌 Що таке Screenshot у Selenium
Скріншот (знімок екрану) — це збереження зображення поточного стану сторінки або елемента, яке допомагає:
* відлагоджувати тести
* зберігати докази помилок
* створювати репорти з візуальними доказами (наприклад, у Allure)
---
_**Зробити скріншот всієї сторінки**_

Використання TakesScreenshot:
```java
import org.openqa.selenium.*;
import org.openqa.selenium.io.FileHandler;
import java.io.File;
import java.io.IOException;

WebDriver driver = new ChromeDriver();
driver.get("https://example.com
");

// Створюємо об’єкт TakesScreenshot
TakesScreenshot ts = (TakesScreenshot) driver;

// Отримуємо зображення у вигляді файлу
File source = ts.getScreenshotAs(OutputType.FILE);

// Вказуємо шлях для збереження
File destination = new File("C:\\screenshots\\fullpage.png");

// Копіюємо файл
FileHandler.copy(source, destination);

System.out.println("Screenshot saved successfully!");
```
🧠 Пояснення:

OutputType.FILE — повертає скріншот як файл.  
Можна також отримати у Base64 або byte[], наприклад:
```java
String base64 = ts.getScreenshotAs(OutputType.BASE64);
```
---
**_Зробити скріншот конкретного елемента_**

```java
WebElement logo = driver.findElement(By.id("site-logo"));
File source = logo.getScreenshotAs(OutputType.FILE);
FileHandler.copy(source, new File("C:\\screenshots\\logo.png"));
```
🧠 Підходить, якщо треба зробити знімок конкретної кнопки, зображення, таблиці тощо.

---
**_Використання у тестах (TestNG)_**

Приклад із TestNG (тільки при фейлі):
```java
@AfterMethod
public void takeScreenshotOnFailure(ITestResult result) {
if (ITestResult.FAILURE == result.getStatus()) {
try {
TakesScreenshot ts = (TakesScreenshot) driver;
File source = ts.getScreenshotAs(OutputType.FILE);
FileHandler.copy(source, new File("C:\\screenshots\\" + result.getName() + ".png"));
} catch (Exception e) {
e.printStackTrace();
}
}
}
```
---
**_Screenshot у форматі Base64 (для репортів Allure)_**

```java
String screenshotBase64 = ((TakesScreenshot) driver).getScreenshotAs(OutputType.BASE64);
// Можна передати у Allure або лог
System.out.println("data:image/png;base64," + screenshotBase64);
```
---

#### 🧠 Поради
| 🧩 Ситуація                           | ✅ Рішення                                         |
| ------------------------------------- | ------------------------------------------------- |
| Потрібно зробити скріншот сторінки    | `((TakesScreenshot) driver).getScreenshotAs(...)` |
| Потрібно зберегти елемент             | `element.getScreenshotAs(...)`                    |
| Потрібно додати в Allure              | `OutputType.BASE64`                               |
| Тести запускаються на Selenium Grid   | Використати `Augmenter`                           |
| Треба зробити автоматично при помилці | Реалізувати у `@AfterMethod` або `@AfterEach`     |

---

#### 💡 Коротко

* TakesScreenshot — головний інтерфейс для створення скріншотів.
* Використовуй OutputType.FILE для збереження на диск.
* Використовуй OutputType.BASE64 для репортів або логів.
* Можна робити скріншоти всього екрану або окремого елемента.
* Для RemoteWebDriver потрібен Augmenter.