# 🧠 Part 2: Understanding MVC in ASP.NET Core

Before building features, we need to understand the **Model-View-Controller (MVC)** pattern and how it works in ASP.NET Core.

---

## 2.1 What is MVC?

### 🎯 MVC Breakdown

The MVC pattern splits your app into 3 clear roles:

* **Model**: Holds and manages data — e.g., `TodoItem.cs`
* **View**: The UI template — e.g., `Index.cshtml`
* **Controller**: Handles user requests, interacts with the model, and returns a view — e.g., `TodoController.cs`

### 🔁 MVC Flow in ASP.NET Core

```plaintext
Browser Request → Controller → Model → View → HTML Response
```

Imagine you visit `/Todo/Index`:

1. The **Controller** handles the route `/Todo/Index`
2. It uses the **Model** to get or process data
3. It returns a **View**, passing the model data to it
4. The **View** generates an HTML page using Razor
5. The user sees a web page built from the data

---

## 2.2 ASP.NET Core Project Structure Explained

When you run `dotnet new mvc`, you get this structure:

```plaintext
📁 TodoMvcApp/
├── Controllers/        # C# files for request handling
├── Models/             # Your app's data classes
├── Views/              # Razor (.cshtml) view files
├── wwwroot/            # Static files (CSS, JS, images)
├── Program.cs          # App entry point and configuration
├── appsettings.json    # Global settings like connection strings
```

### 📄 Key File Roles

* `/Program.cs`

  * Starts the app and configures services (including routing)

* `/Controllers/TodoController.cs`

  * Responds to URLs like `/Todo/Index`

* `/Models/TodoItem.cs`

  * Stores data about to-do items

* `/Views/Todo/Index.cshtml`

  * Displays the to-do list to the user

> 📌 Convention over Configuration: ASP.NET Core uses naming patterns, so `TodoController` and its `Index` method automatically map to `/Todo/Index` and use `/Views/Todo/Index.cshtml`.

---

## ✅ Summary

* MVC is a clean way to separate concerns in your app.
* ASP.NET Core automatically connects URLs, controllers, and views using conventions.
* The default structure makes it easy to follow and scale your project.

➡️ Next up: [Part 3 – Building the To-Do App Foundation](./part3_app_foundation.md)
