# 🗂️ Робота з кількома вкладками (Browser Tabs) у Selenium

---

Selenium дозволяє відкривати нові вкладки/вікна, перемикатися між ними та закривати непотрібні.  
Це корисно, коли тест відкриває нову сторінку у **новій вкладці**, але треба повернутись до початкової.

---

#### 📌 Основні методи

| Метод | Опис |
|------|------|
| `driver.getWindowHandle()` | Повертає унікальний ідентифікатор (handle) поточної вкладки/вікна (`String`). |
| `driver.getWindowHandles()` | Повертає `Set<String>` з усіма відкритими вкладками/вікнами. |
| `driver.switchTo().window(handle)` | Перемикає драйвер на вкладку з вказаним `handle`. |
| `driver.switchTo().newWindow(WindowType.TAB)` | (Selenium 4) Відкриває нову вкладку та автоматично на неї перемикається. |
| `driver.switchTo().newWindow(WindowType.WINDOW)` | (Selenium 4) Відкриває нове вікно браузера. |
| `driver.close()` | Закриває поточну вкладку (але не закриває весь браузер). |
| `driver.quit()` | Закриває всі вкладки/вікна і завершує роботу драйвера. |

---

#### 📘 Приклади використання

🔹 Отримати хендли всіх вкладок
```java
// Поточний хендл
String mainHandle = driver.getWindowHandle();

// Всі відкриті вкладки
Set<String> allHandles = driver.getWindowHandles();
for (String handle : allHandles) {
    System.out.println("Handle: " + handle);
}
```
---
🔹 Перемикання на нову вкладку
```java
String mainHandle = driver.getWindowHandle();
Set<String> handles = driver.getWindowHandles();

for (String handle : handles) {
    if (!handle.equals(mainHandle)) {
        driver.switchTo().window(handle); // Перехід на нову вкладку
        break;
    }
}
```
---
🔹Відкрити нову вкладку (Selenium 4)
```java
driver.switchTo().newWindow(WindowType.TAB);
driver.get("https://example.com");
```
---
🔹Повернення до головної вкладки
```java
driver.switchTo().window(mainHandle);
```
---
🔹 Закриття поточної вкладки та перехід до іншої
```java
driver.close(); // Закриває активну вкладку
driver.switchTo().window(mainHandle); // Перемикаємось на потрібну
```
---

#### 🧠 Поради
- Порядок хендлів не гарантується – завжди перевіряй через if (!handle.equals(mainHandle)).
- Після закриття вкладки обов’язково викликай switchTo().window(...), інакше драйвер залишиться без активного вікна.
- Для зручності можна зберігати хендли у List<String> і перемикатися за індексом, наприклад:
```java
- List<String> tabs = new ArrayList<>(driver.getWindowHandles());
driver.switchTo().window(tabs.get(1)); // Перехід на другу вкладку
```