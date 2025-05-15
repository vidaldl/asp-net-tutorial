# 📝 ASP.NET Core MVC To-Do App Tutorial

Welcome to the official repository for the **ASP.NET Core MVC To-Do App Tutorial**. This project is designed to help you learn the **Model-View-Controller (MVC)** design pattern in ASP.NET Core by building a fully functional web application — from scratch.

---

## 🎯 Project Goal

This tutorial teaches you how to:

* Set up a modern ASP.NET Core MVC development environment
* Understand how MVC works (Model, View, Controller)
* Build a cleanly structured To-Do app
* Implement full CRUD functionality
* Add layout, routing, and basic styling with Bootstrap
* Handle validation, form input, and errors
* Use ViewModels and debugging tools effectively

> This guide is beginner-friendly for developers with basic C# experience, but new to ASP.NET or web MVC frameworks.

---

## 📂 Folder Structure

```plaintext
TodoMvcApp/
├── Controllers/              # Handles request routing
│   ├── TodoController.cs
│   └── HomeController.cs
├── Models/                   # Represents application data
│   ├── TodoItem.cs
│   └── TodoFormViewModel.cs
├── Views/                    # Razor-based UI templates
│   ├── Shared/
│   │   └── _Layout.cshtml
│   │   └── Error.cshtml
│   ├── Todo/
│   │   ├── Index.cshtml
│   │   ├── Create.cshtml
│   │   ├── Edit.cshtml
│   │   ├── Delete.cshtml
│   │   └── Details.cshtml
├── wwwroot/                  # Static files (CSS, JS, etc.)
├── Program.cs                # App startup configuration
├── appsettings.json          # Configuration settings
```

---

## 📖 Tutorial Outline

Each section is a standalone Markdown file in this repository:

1. **Part 1** – [Environment Setup](./part1_environment_setup.md)
2. **Part 2** – [Understanding MVC](./part2_understanding_mvc.md)
3. **Part 3** – [Building the App Foundation](./part3_app_foundation.md)
4. **Part 4** – [Full CRUD Implementation](./part4_crud_operations.md)
5. **Part 5** – [ViewModels and Data Passing](./part5_data_passing.md)
6. **Part 6** – [Routing and Navigation](./part6_routing_and_navigation.md)
7. **Part 7** – [Layouts and Styling](./part7_layouts_and_styling.md)
8. **Part 8** – [Debugging and Error Handling](./part8_debugging_and_error_handling.md)
9. **Part 9** – [Wrapping Up and Next Steps](./part9_wrapping_up.md)

---

## 🚀 Get Started

To begin the tutorial, start with:

➡️ [**Part 1 – Environment Setup**](./part1_environment_setup_revised.md)

Make sure you have the .NET SDK installed and VS Code ready to go!

---

## 🚀 How to Run the App

```bash
# Make sure you have .NET SDK installed (version 8 or later)
dotnet --version

# Clone this repo and navigate to the project folder
git clone https://github.com/your-username/TodoMvcApp.git
cd TodoMvcApp

# Run the app
dotnet run
```

Then open your browser and go to `https://localhost:5001`

---

## 🙇‍♀️ Who This Is For

* C# developers new to ASP.NET Core
* Anyone learning how MVC web frameworks work
* Educators and bootcamp instructors

---

## 🛃️ Next Steps

Here’s how you can go deeper:

### 1. Add Real Database Support

* Integrate **Entity Framework Core**
* Replace in-memory `_items` with a real database like SQLite or SQL Server
* Learn migrations and `DbContext`

### 2. Implement User Authentication

* Use **ASP.NET Identity** to add login/logout functionality
* Restrict access to certain pages

### 3. Build New Features

* Add filtering and search to the task list
* Add due dates or priority levels to `TodoItem`
* Use **AJAX** or **SignalR** for real-time features

### 4. Learn Deployment

* Host your app on **Azure App Service**, **Render**, or **Netlify with API backends**
* Learn to configure environment settings securely

---

## 📣 Contributing

Found a typo? Want to suggest improvements? Pull requests are welcome!

---

## 📄 License

MIT License. Free to use, modify, and share.

---

Happy coding!

> "The best way to learn is by building."

---
