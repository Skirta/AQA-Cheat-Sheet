# ⚠️ Робота з JavaScript Alerts у Selenium

#### ❓ Що таке Alert
**Alert** – це нативне спливаюче вікно браузера (JavaScript).  
Є три основні типи:
- **Alert** – просте повідомлення з кнопкою **OK**.
- **Confirm** – запит із кнопками **OK** та **Cancel**.
- **Prompt** – вікно з полем для введення тексту та кнопками **OK** і **Cancel**.

👉 Щоб взаємодіяти з такими вікнами, Selenium використовує об’єкт `Alert`.

---

#### 📌 Основні методи

| Метод | Опис |
|------|------|
| `driver.switchTo().alert()` | Перемикає управління на активний alert і повертає об’єкт `Alert`. |
| `alert.accept()` | Натискає кнопку **OK** (підтвердження). |
| `alert.dismiss()` | Натискає кнопку **Cancel** (відхиляє). |
| `alert.getText()` | Отримує текст повідомлення. |
| `alert.sendKeys("text")` | Вводить текст у **Prompt** (не працює для простого Alert/Confirm). |

---

#### 📘 Приклади використання
 
##### 🔹 Прості дії з Alert
```java
// Перехід на Alert
Alert alert = driver.switchTo().alert();

// Отримати текст
System.out.println(alert.getText());

// Натиснути OK
alert.accept();
```
---
##### 🔹 Обробка Confirm (OK/Cancel)
```java
Alert confirm = driver.switchTo().alert();
System.out.println(confirm.getText());

// Натиснути Cancel
confirm.dismiss();
```
---
##### 🔹 Обробка Prompt (введення тексту)
```java
Alert prompt = driver.switchTo().alert();
prompt.sendKeys("Hello Selenium");
prompt.accept();
```
---
#### ⏳ Очікування появи Alert  
Щоб уникнути помилок, використовуй Explicit Wait:
```java
new WebDriverWait(driver, Duration.ofSeconds(10))
    .until(ExpectedConditions.alertIsPresent());

Alert alert = driver.switchTo().alert();
System.out.println(alert.getText());
alert.accept();
```