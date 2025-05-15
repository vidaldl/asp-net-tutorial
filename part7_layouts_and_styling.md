# Part 7: Layouts and Styling

In this part, we’ll clean up the UI using ASP.NET Core’s **layout system** and add some basic styling with **Bootstrap** to make the app more user-friendly.

---

## 7.1 Layout Pages – Shared HTML for All Views

ASP.NET Core MVC uses a shared layout file to provide a consistent structure across all views.

### 📄 File: `/Views/Shared/_Layout.cshtml`

Open or edit the existing file and find this placeholder:

```html
@RenderBody()
```

This is where the content of each page (like `Index.cshtml`, `Create.cshtml`) will be injected.

### 🛠️ Customize the Layout

Update `_Layout.cshtml` to include a basic Bootstrap layout:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo App - @ViewData["Title"]</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light mb-4">
        <div class="container-fluid">
            <a class="navbar-brand" asp-controller="Todo" asp-action="Index">To-Do App</a>
            <div class="navbar-nav">
                <a class="nav-link" asp-controller="Todo" asp-action="Index">Home</a>
                <a class="nav-link" asp-controller="Todo" asp-action="Create">Add Task</a>
            </div>
        </div>
    </nav>

    <main class="container">
        @RenderBody()
    </main>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    @RenderSection("Scripts", required: false)
</body>
</html>
```

> 🧠 `@RenderBody()` is required. `@RenderSection()` is optional and used for page-specific scripts.

---

## 7.2 Use Layout in All Views

Every Razor view should declare the layout or inherit it via `_ViewStart.cshtml`:

### 📄 File: `/Views/_ViewStart.cshtml`

This file is already present and should contain:

```csharp
@{
    Layout = "_Layout";
}
```

This ensures that all views use the shared layout.

> ✅ You usually don’t need to manually set `Layout =` in every individual view.

---

## 7.3 Style Your Views

You can now style your HTML using Bootstrap classes:

* Add `table` to `<table>` elements
* Add `form-control` to inputs
* Add `btn`, `btn-primary`, `btn-success`, etc. to buttons

Example button:

```html
<button class="btn btn-success">Save Task</button>
```

Example table header:

```html
<table class="table table-striped">
```

> 🧠 Bootstrap helps you avoid raw HTML styling — it's responsive and mobile-friendly by default.

---

## ✅ Summary

* All views now share a layout with `_Layout.cshtml`
* Bootstrap provides instant styling with little effort
* Navigation is consistent across pages

➡️ Next up: [Part 8 – Debugging and Error Handling](./part8_debugging_and_error_handling.md)
