# 🚾 Part 8: Debugging and Error Handling

Every developer hits snags — that’s part of the job. In this section, you'll learn how to **debug**, catch **common issues**, and handle **runtime errors** gracefully in your ASP.NET Core MVC app.

---

## 8.1 Developer Exception Page

ASP.NET Core automatically shows a detailed error page **during development**.

### ✅ Enable the Developer Exception Page

#### 📄 File: `/Program.cs`

Make sure the following block exists **after** `var app = builder.Build();`:

```csharp
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```

> ⚠️ This ensures you see full stack traces when something goes wrong during development.

---

## 8.2 Handling 404 and Other Status Codes

When a page isn’t found (404) or crashes (500), you can customize the response.

### 📄 Add Error View

#### 📄 File: `/Views/Shared/Error.cshtml`

Create this file if it doesn't exist:

```html
@model Microsoft.AspNetCore.Diagnostics.ExceptionHandlerFeature

<h1>Oops! Something went wrong.</h1>
<p>An error occurred while processing your request.</p>
<p><strong>Error:</strong> @Model?.Error?.Message</p>
<a asp-action="Index" asp-controller="Todo">Back to Home</a>
```

### 🛠️ Set Up Error Middleware

#### 📄 File: `/Program.cs`

Add this block **below the development block**, to handle errors in production:

```csharp
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}
```

### 🔧 Add Error Action in Controller

#### 📄 File: `/Controllers/HomeController.cs`

Add this method to handle the error route:

```csharp
using Microsoft.AspNetCore.Diagnostics;

public class HomeController : Controller
{
    public IActionResult Error()
    {
        var exceptionFeature = HttpContext.Features.Get<IExceptionHandlerFeature>();
        return View(exceptionFeature);
    }
}
```

> ⚠️ If you don't already have a `HomeController`, create one using the file path `/Controllers/HomeController.cs`.

---

## 8.3 Debugging in Visual Studio Code

### 🪛 Add Breakpoints

1. Open a `.cs` file (e.g., `/Controllers/TodoController.cs`)
2. Click to the left of a line number to set a red dot (breakpoint)

### ▶️ Start Debugging

1. Press `F5` or open the Run & Debug panel (sidebar)
2. Select “.NET Core Launch (web)” when prompted
3. Trigger the action in your app (e.g., click “Add Task”) to hit the breakpoint

### 🔍 Use Watch and Locals

* **Watch**: Add expressions to track manually
* **Locals**: See variables in current method context

---

## 🥮 Common Issues & Fixes

| Issue                  | Likely Cause                           | Fix                                    |
| ---------------------- | -------------------------------------- | -------------------------------------- |
| 404 Not Found          | Wrong route or missing view            | Check controller action and file path  |
| Model not binding      | Property names don’t match form fields | Use `asp-for` and ensure correct names |
| Validation not showing | Missing validation scripts             | Add `@section Scripts` to your view    |
| Breakpoint not hit     | App not in debug mode                  | Start with `F5` or VS Code debugger    |

---

## ✅ Summary

* Enable `UseDeveloperExceptionPage()` in development via `Program.cs`
* Add custom error handling using middleware and a shared view
* Use breakpoints and debugger in VS Code to trace and solve bugs faster

➡️ Next up: [Part 9 – Wrapping Up and Next Steps](./part9_wrapping_up.md)
