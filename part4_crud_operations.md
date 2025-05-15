# ✍️ Part 4: Full CRUD Implementation

Now that we’ve built the basic MVC structure, it’s time to add **full CRUD functionality**: Create, Read, Update, and Delete.

We’ll also introduce **model binding** and **validation** to make sure users submit valid data.

---

## 4.1 Create – Add a New Task

### 🧭 Controller: `/Controllers/TodoController.cs`

Add to your existing `TodoController` class:

```csharp
// GET: /Todo/Create
public IActionResult Create()
{
    return View();
}

// POST: /Todo/Create
[HttpPost]
[ValidateAntiForgeryToken]
public IActionResult Create(TodoItem item)
{
    if (ModelState.IsValid)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
        return RedirectToAction("Index");
    }
    return View(item);
}
```

### 📄 View: `/Views/Todo/Create.cshtml`

```html
@model TodoMvcApp.Models.TodoItem

<h2>Create New Task</h2>

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

## 🔄 4.1.1 Model Binding & Validation

### ✏️ Model: `/Models/TodoItem.cs`

Update your model with validation attributes:

```csharp
using System.ComponentModel.DataAnnotations;

public class TodoItem
{
    public int Id { get; set; }

    [Required(ErrorMessage = "Title is required")]
    [StringLength(100)]
    public string Title { get; set; }

    public string Description { get; set; }
    public bool IsDone { get; set; }
}
```

### 💡 Razor Validation Scripts

In `_Layout.cshtml`, make sure you have:

```html
@section Scripts {
    <partial name="_ValidationScriptsPartial" />
}
```

This ensures client-side validation works.

---

## 4.2 Read – List and View Tasks

Already done in Part 3 using:

* `/Controllers/TodoController.cs` → `Index()` method
* `/Views/Todo/Index.cshtml`

For detailed task view:

### ➕ Add to Controller

```csharp
public IActionResult Details(int id)
{
    var item = _items.FirstOrDefault(t => t.Id == id);
    if (item == null) return NotFound();
    return View(item);
}
```

### 📄 Create View: `/Views/Todo/Details.cshtml`

```html
@model TodoMvcApp.Models.TodoItem

<h2>Task Details</h2>
<p><strong>Title:</strong> @Model.Title</p>
<p><strong>Description:</strong> @Model.Description</p>
<p><strong>Completed:</strong> @(Model.IsDone ? "Yes" : "No")</p>
<a asp-action="Index">Back to List</a>
```

---

## 4.3 Update – Edit a Task

### 🧭 Controller

```csharp
// GET: /Todo/Edit/1
public IActionResult Edit(int id)
{
    var item = _items.FirstOrDefault(t => t.Id == id);
    if (item == null) return NotFound();
    return View(item);
}

// POST: /Todo/Edit/1
[HttpPost]
[ValidateAntiForgeryToken]
public IActionResult Edit(int id, TodoItem updatedItem)
{
    if (!ModelState.IsValid) return View(updatedItem);

    var item = _items.FirstOrDefault(t => t.Id == id);
    if (item == null) return NotFound();

    item.Title = updatedItem.Title;
    item.Description = updatedItem.Description;
    item.IsDone = updatedItem.IsDone;

    return RedirectToAction("Index");
}
```

### 📄 View: `/Views/Todo/Edit.cshtml`

```html
@model TodoMvcApp.Models.TodoItem

<h2>Edit Task</h2>

<form asp-action="Edit" method="post">
    <input type="hidden" asp-for="Id" />
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
    <button type="submit" class="btn btn-success mt-3">Update</button>
</form>
```

---

## 4.4 Delete – Remove a Task

### 🧭 Controller

```csharp
// GET: /Todo/Delete/1
public IActionResult Delete(int id)
{
    var item = _items.FirstOrDefault(t => t.Id == id);
    if (item == null) return NotFound();
    return View(item);
}

// POST: /Todo/Delete/1
[HttpPost, ActionName("Delete")]
[ValidateAntiForgeryToken]
public IActionResult DeleteConfirmed(int id)
{
    var item = _items.FirstOrDefault(t => t.Id == id);
    if (item != null)
    {
        _items.Remove(item);
    }
    return RedirectToAction("Index");
}
```

### 📄 View: `/Views/Todo/Delete.cshtml`

```html
@model TodoMvcApp.Models.TodoItem

<h2>Are you sure you want to delete this task?</h2>

<div>
    <strong>@Model.Title</strong>
    <p>@Model.Description</p>
</div>

<form asp-action="Delete" method="post">
    <input type="hidden" asp-for="Id" />
    <button type="submit" class="btn btn-danger">Yes, Delete</button>
    <a asp-action="Index" class="btn btn-secondary">Cancel</a>
</form>
```

---

## ✅ Summary

* ✅ **Create**: Form and model validation
* ✅ **Read**: List and detail view
* ✅ **Update**: Edit and update form
* ✅ **Delete**: Confirmation and remove logic

➡️ Next up: [Part 5 – Intermediate Concepts: Data Passing and ViewModels](./part5_data_passing.md)
