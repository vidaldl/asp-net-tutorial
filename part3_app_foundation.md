# 🧱 Part 3: Building the To-Do App Foundation

Let's build the basic pieces of our To-Do app: the **Model**, **Controller**, and **View**. These will work together to display a simple list of tasks using MVC.

---

## 3.1 Create the Model – `/Models/TodoItem.cs`

This file defines the data structure for our tasks.

```csharp
// File: /Models/TodoItem.cs

namespace TodoMvcApp.Models
{
    public class TodoItem
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Description { get; set; }
        public bool IsDone { get; set; }
    }
}
```

### 💡 Why This Matters

This class represents a single task. We'll use it throughout the app for forms, displays, and updates.

---

## 3.2 Create the Controller – `/Controllers/TodoController.cs`

Controllers respond to browser requests.

```csharp
// File: /Controllers/TodoController.cs

using Microsoft.AspNetCore.Mvc;
using TodoMvcApp.Models;
using System.Collections.Generic;
using System.Linq;

namespace TodoMvcApp.Controllers
{
    public class TodoController : Controller
    {
        // Simulated in-memory database
        private static List<TodoItem> _items = new List<TodoItem>
        {
            new TodoItem { Id = 1, Title = "Buy groceries", Description = "Milk, eggs, bread", IsDone = false },
            new TodoItem { Id = 2, Title = "Finish homework", Description = "Math and Science", IsDone = true }
        };

        // GET: /Todo
        public IActionResult Index()
        {
            return View(_items);
        }
    }
}
```

### 🧠 What It Does

* Creates fake data in `_items`
* Returns the view and passes in the item list

---

## 3.3 Create the View – `/Views/Todo/Index.cshtml`

Views display HTML to the browser. Create a new folder and file:

```plaintext
Path: /Views/Todo/Index.cshtml
```

```html
@model List<TodoMvcApp.Models.TodoItem>

<h2>To-Do List</h2>

<table class="table">
    <thead>
        <tr>
            <th>Title</th>
            <th>Description</th>
            <th>Completed</th>
        </tr>
    </thead>
    <tbody>
    @foreach (var item in Model)
    {
        <tr>
            <td>@item.Title</td>
            <td>@item.Description</td>
            <td>@(item.IsDone ? "✅" : "❌")</td>
        </tr>
    }
    </tbody>
</table>
```

### 📘 Explanation

* `@model` declares the data type expected from the controller
* Razor `@foreach` loops through the items
* `@item.PropertyName` inserts data into the page

---

## ✅ Summary

* We created a **Model** for our data
* A **Controller** to handle a route and return data
* A **View** to render that data as HTML

➡️ Next up: [Part 4 – Full CRUD Implementation](./part4_crud_operations.md)
