# ⏳ Очікування (Wait) у Selenium
Цей розділ пояснює, як керувати очікуваннями в Selenium для роботи з елементами, які з’являються із затримкою (наприклад, після завантаження сторінки або AJAX-запиту).

---

#### 📌 Типи очікувань

| Тип очікування | Опис |
|---------------|------|
| `Implicit Wait` | Задається один раз для драйвера. Автоматично чекає заданий час перед киданням `NoSuchElementException`. |
| `Explicit Wait` | Очікування конкретної умови (наприклад, поки елемент стане видимим або клікабельним). |
| `Fluent Wait`   | Те саме, що Explicit, але з можливістю налаштувати інтервал опитування та ігноровані винятки. |

---

#### 🛠 Implicit Wait

```java
// Очікування до 10 секунд для всіх пошуків елементів
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
```

---

#### 🛠 Explicit Wait

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

// Очікування, поки елемент стане видимим
WebElement element = wait.until(
    ExpectedConditions.visibilityOfElementLocated(By.id("username"))
);

// Очікування, поки кнопка стане клікабельною
WebElement button = wait.until(
    ExpectedConditions.elementToBeClickable(By.id("submit"))
);
```
#### 📌 Найпоширеніші ExpectedConditions
| Метод | Опис |
|-------|------|
| `visibilityOfElementLocated(locator)` | Елемент видимий |
| `presenceOfElementLocated(locator)` | Елемент є у DOM |
| `elementToBeClickable(locator)` | Елемент клікабельний |
| `invisibilityOfElementLocated(locator)` | Елемент зник/невидимий |
| `textToBe(locator, "text")` | Текст дорівнює значенню |
| `textToBePresentInElementLocated(locator, "text")` | Текст містить значення |
| `attributeToBe(locator, "attr", "value")` | Атрибут має значення |
| `titleIs("title")` / `titleContains("part")` | Очікування по title сторінки |
| `urlToBe("url")` / `urlContains("part")` | Очікування по URL |
| `alertIsPresent()` | Очікування появи alert |

---

#### 🛠 Fluent Wait

```java
Wait<WebDriver> wait = new FluentWait<>(driver)
        .withTimeout(Duration.ofSeconds(30))       // максимум 30 секунд
        .pollingEvery(Duration.ofSeconds(5))       // перевірка кожні 5 секунд
        .ignoring(NoSuchElementException.class);   // ігнорувати помилку

WebElement element = wait.until(
    drv -> drv.findElement(By.id("username"))
);
```

---

#### 🧠 Порада  
* Використовуй `Explicit Wait` замість `Implicit` для більшої гнучкості.
* Не змішуй `Implicit` і `Explicit` — це може призводити до непередбачуваних затримок.
* Для складних сценаріїв з AJAX краще застосовувати `Fluent Wait`.

