# 🧠 Part 5: Intermediate Concepts – Data Passing and ViewModels

Now that your To-Do app supports full CRUD, let’s explore **how data flows more deeply** between controllers and views. This part introduces:

* Temporary data passing (ViewData, ViewBag, TempData)
* ViewModels (for better design and flexibility)

---

## 5.1 Passing Data Between Controller and View

There are three main ways to pass data **besides the model**:

### 🪣 ViewData

* A `Dictionary<string, object>`
* Useful for one-way, one-time communication

```csharp
ViewData["Message"] = "This message comes from the controller!";
```

In your view:

```html
<p>@ViewData["Message"]</p>
```

### 📦 ViewBag

* A dynamic wrapper around ViewData
* Syntactic sugar (easier to write)

```csharp
ViewBag.Note = "Hello from ViewBag!";
```

In your view:

```html
<p>@ViewBag.Note</p>
```

### 🔁 TempData

* Persists across **one redirect**
* Ideal for status messages like "Item created"

```csharp
TempData["Success"] = "Task added successfully!";
return RedirectToAction("Index");
```

Then in `/Views/Todo/Index.cshtml`:

```html
@if (TempData["Success"] != null)
{
    <div class="alert alert-success">@TempData["Success"]</div>
}
```

> ✅ **Best practice**: Use ViewModel for structured data, ViewBag/TempData for lightweight info like alerts.

---

## 5.2 Using ViewModels for Clean Architecture

### 🧱 What Is a ViewModel?

A **ViewModel** is a custom class made just for the **View** — it may include 1+ models or additional metadata needed for rendering.

### 📄 Create a ViewModel – `/Models/TodoFormViewModel.cs`

```csharp
// File: /Models/TodoFormViewModel.cs
using System.ComponentModel.DataAnnotations;

namespace TodoMvcApp.Models
{
    public class TodoFormViewModel
    {
        [Required]
        [StringLength(100)]
        public string Title { get; set; }

        public string Description { get; set; }

        public bool IsDone { get; set; }

        // Optional custom field just for the view
        public string PageTitle { get; set; }
    }
}
```

### 🛠️ Update the Controller – `/Controllers/TodoController.cs`

Modify the `Create()` action:

```csharp
// GET: /Todo/Create
public IActionResult Create()
{
    var vm = new TodoFormViewModel
    {
        PageTitle = "Create New Task"
    };
    return View(vm);
}

// POST: /Todo/Create
[HttpPost]
[ValidateAntiForgeryToken]
public IActionResult Create(TodoFormViewModel form)
{
    if (ModelState.IsValid)
    {
        var item = new TodoItem
        {
            Id = _items.Count + 1,
            Title = form.Title,
            Description = form.Description,
            IsDone = form.IsDone
        };
        _items.Add(item);
        TempData["Success"] = "Task created using a ViewModel!";
        return RedirectToAction("Index");
    }
    form.PageTitle = "Create New Task";
    return View(form);
}
```

### 🧩 Update View – `/Views/Todo/Create.cshtml`

```html
@model TodoMvcApp.Models.TodoFormViewModel

<h2>@Model.PageTitle</h2>

<form asp-action="Create" method="post">
    <div class="form-group">
        <label asp-for="Title"></label>
        <input asp-for="Title" class="form-control" />
        <span asp-validation-for="Title" class="text-danger"></span>
    </div>
    <div class="form-group">
        <label asp-for="Description"></label>
        <textarea asp-for="Description" class="form-control"></textarea>
    </div>
    <div class="form-check">
        <input asp-for="IsDone" class="form-check-input" />
        <label asp-for="IsDone" class="form-check-label"></label>
    </div>
    <button type="submit" class="btn btn-primary mt-3">Save</button>
</form>
```

---

## ✅ Summary

* **ViewBag, ViewData, and TempData** are tools for short-term data passing
* **ViewModels** give you clean separation of concerns between View and Model
* Your `Create.cshtml` view is now smarter and better organized

➡️ Next up: [Part 6 – Routing and Navigation](./part6_routing_and_navigation.md)
