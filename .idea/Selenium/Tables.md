# 📊 Робота з таблицями у Selenium  

#### ❓ Що таке HTML-таблиця  
HTML-таблиця складається з:
- `<table>` – контейнер таблиці
- `<thead>` – заголовок (опційно)
- `<tbody>` – тіло таблиці (рядки з даними)
- `<tr>` – рядок
- `<th>` – комірка заголовка
- `<td>` – звичайна комірка

Приклад:
```html
<table id="users">
  <thead>
    <tr><th>Name</th><th>Email</th></tr>
  </thead>
  <tbody>
    <tr><td>Alice</td><td>alice@mail.com</td></tr>
    <tr><td>Bob</td><td>bob@mail.com</td></tr>
  </tbody>
</table>
```
---
#### 📌 Основні кроки роботи  
1. Знайти елемент `<table>`.
2. Отримати рядки (`<tr>`).
3. Для кожного рядка отримати комірки (`<td>` або `<th>`).
4. Зберегти дані у Java-структуру (наприклад, `List<List<String>>` або `Map`).
---
#### 📘 Приклади використання
##### 🔹 Отримати всі дані таблиці
```java
WebElement table = driver.findElement(By.id("users"));
List<WebElement> rows = table.findElements(By.tagName("tr"));

for (WebElement row : rows) {
    List<WebElement> cells = row.findElements(By.tagName("td"));
    for (WebElement cell : cells) {
        System.out.print(cell.getText() + " | ");
    }
    System.out.println(); // ➡️ Виведе всі дані рядок за рядком.
}
```
---
##### 🔹 Перетворення таблиці у List<List<String>>
```java
WebElement table = driver.findElement(By.id("users"));
List<List<String>> tableData = new ArrayList<>();

for (WebElement row : table.findElements(By.cssSelector("tbody tr"))) {
    List<String> rowData = new ArrayList<>();
    for (WebElement cell : row.findElements(By.tagName("td"))) {
        rowData.add(cell.getText());
    }
    tableData.add(rowData);
}

// Приклад доступу
System.out.println("Ім'я у 2-му рядку: " + tableData.get(1).get(0));
```
---
##### 🔹 Отримати заголовки таблиці 
```java
WebElement table = driver.findElement(By.id("users"));
List<WebElement> headers = table.findElements(By.cssSelector("thead th"));

for (WebElement header : headers) {
    System.out.println("Header: " + header.getText());
}
```
---
##### 🔹 Пошук значення за умовою
Наприклад, знайти email користувача "Bob":
```java
WebElement table = driver.findElement(By.id("users"));
List<WebElement> rows = table.findElements(By.cssSelector("tbody tr"));

for (WebElement row : rows) {
    List<WebElement> cells = row.findElements(By.tagName("td"));
    if (!cells.isEmpty() && cells.get(0).getText().equals("Bob")) {
        System.out.println("Email Bob: " + cells.get(1).getText());
        break;
    }
}
```
#### 🔹 Зберегти таблицю у список мап (ключ – заголовок)
Зручно, коли потрібно працювати з рядками як з об’єктами:
```java
WebElement table = driver.findElement(By.id("users"));
List<WebElement> headers = table.findElements(By.cssSelector("thead th"));
List<Map<String, String>> tableAsMap = new ArrayList<>();

for (WebElement row : table.findElements(By.cssSelector("tbody tr"))) {
    Map<String, String> rowMap = new LinkedHashMap<>();
    List<WebElement> cells = row.findElements(By.tagName("td"));
    for (int i = 0; i < cells.size(); i++) {
        String key = headers.get(i).getText();
        String value = cells.get(i).getText();
        rowMap.put(key, value);
    }
    tableAsMap.add(rowMap);
}

// Приклад доступу
System.out.println("Email Alice: " + tableAsMap.get(0).get("Email"));
```
---
#### 🧠 Поради  
- Використовуй tbody tr у локаторах, щоб уникнути потрапляння в заголовки.
- Якщо таблиця динамічна (AJAX), застосовуй Explicit Wait:
```java
new WebDriverWait(driver, Duration.ofSeconds(10))
        .until(ExpectedConditions.presenceOfElementLocated(By.cssSelector("table#users tbody tr")));
```
- Для великих таблиць можна комбінувати пагінацію або прокручування (scroll) з парсингом.