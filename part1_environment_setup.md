# 📦 Part 1: Environment Setup (VS Code)

This section sets up everything you need to develop and run a simple ASP.NET Core MVC app using **Visual Studio Code** and the **.NET CLI**. We'll also explore the project structure created by ASP.NET.

---

## ✅ Prerequisites

* A computer running **Windows**, **macOS**, or **Linux**
* Basic command line familiarity

---

## 1.1 Install .NET SDK

### 🔗 Step 1: Download and Install

1. Visit the official .NET SDK download page: [https://dotnet.microsoft.com/download](https://dotnet.microsoft.com/download)
2. Download the latest **LTS version** (e.g., .NET 8)
3. Install it by running the installer for your OS

### 🧪 Step 2: Verify Installation

Open a terminal and run:

```bash
dotnet --version
```

You should see output like:

```
8.0.100
```

This confirms the .NET CLI is working.

---

## 1.2 Install Visual Studio Code

### 🔗 Step 1: Download and Install VS Code

* Visit [https://code.visualstudio.com/](https://code.visualstudio.com/) and download the installer
* Install it just like any other app

### 🧩 Step 2: Install Extensions

Open VS Code and install these extensions:

* **C#** (by Microsoft – adds IntelliSense, debugging, etc.)
* **Razor** (for better Razor view support)
* Optional: ".NET Install Tool for Extension Authors"

---

## 1.3 Create and Run a New MVC App

### 🧱 Step 1: Scaffold the Project

In a terminal, run:

```bash
dotnet new mvc -n TodoMvcApp
cd TodoMvcApp
```

This creates the following structure:

```plaintext
📁 TodoMvcApp/
├── Controllers/
├── Models/
├── Views/
├── wwwroot/           # Static files (CSS, JS, images)
├── Program.cs         # App entry point
├── appsettings.json   # Configuration file
```

### 📂 Step 2: Open the Project in VS Code

```bash
code .
```

> 💡 Tip: If `code` isn't recognized, open VS Code manually and use `File → Open Folder...`

### ▶️ Step 3: Run the App

From the terminal inside VS Code:

```bash
dotnet run
```

Visit the URL shown in the output:

```
https://localhost:5001
```

You should see the default ASP.NET Core MVC homepage.

---

## ✅ What You’ve Done

* Installed the .NET SDK and VS Code
* Created your first ASP.NET Core MVC project
* Learned the default folder structure
* Ran the app locally

➡️ Next up: [Part 2 – Understanding MVC in ASP.NET Core](./part2_understanding_mvc.md)
