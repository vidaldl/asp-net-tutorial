# 🔀 Part 6: Routing and Navigation

In this part, we’ll look at how ASP.NET Core handles **routing** (matching URLs to actions) and how to create intuitive **navigation** between views.

---

## 6.1 How Routing Works in ASP.NET Core

Routing connects **URLs** to specific **Controller actions**. ASP.NET Core uses **convention-based routing** by default.

### 🧠 Default Route Template

In `/Program.cs`:

```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

### 🔎 What it means

```plaintext
URL pattern → /{controller}/{action}/{optional id}
```

* `/Todo/Index` → `TodoController.Index()`
* `/Todo/Edit/1` → `TodoController.Edit(1)`

If no route is given, it defaults to `HomeController.Index()`.

> ✅ Routes are case-insensitive and flexible. You can use attribute routing too, but we’ll stick to conventional routing for now.

### 🔗 Add Custom Route (optional)

You can add your own routes:

```csharp
app.MapControllerRoute(
    name: "tasks",
    pattern: "tasks/{action}/{id?}",
    defaults: new { controller = "Todo" });
```

This maps `/tasks/create` to `TodoController.Create()`.

---

## 6.2 Add Navigation Links

### 📄 Update Layout – `/Views/Shared/_Layout.cshtml`

Add a nav bar at the top:

```html
<nav class="navbar navbar-expand navbar-light bg-light mb-4">
    <div class="container-fluid">
        <a class="navbar-brand" asp-controller="Todo" asp-action="Index">To-Do App</a>
        <div class="navbar-nav">
            <a class="nav-link" asp-controller="Todo" asp-action="Index">Home</a>
            <a class="nav-link" asp-controller="Todo" asp-action="Create">Add Task</a>
        </div>
    </div>
</nav>
```

### 📄 Add Return Links to Views

To improve navigation, add return links at the bottom of your views, e.g.:

```html
<a asp-action="Index" class="btn btn-secondary mt-3">Back to List</a>
```

Use this in:

* `/Views/Todo/Create.cshtml`
* `/Views/Todo/Edit.cshtml`
* `/Views/Todo/Delete.cshtml`
* `/Views/Todo/Details.cshtml`

> 🧠 Use `asp-action` and `asp-controller` tag helpers. These automatically generate correct URLs.

---

## 🧪 Quick Routing Test

Try visiting these URLs:

* `/Todo/Index` – See all tasks
* `/Todo/Create` – Add a new task
* `/Todo/Edit/1` – Edit task with ID 1
* `/Todo/Delete/1` – Delete task with ID 1

Make sure your controller actions match these routes!

---

## ✅ Summary

* Routing maps URLs to controller actions using a pattern
* Navigation is built using tag helpers like `asp-action`
* Your app now feels more connected and user-friendly

➡️ Next up: [Part 7 – Layouts and Styling](./part7_layouts_and_styling.md)
