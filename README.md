# C# Project Workshop with GitHub Copilot

Welcome to this interactive workshop where we will use GitHub Copilot to create a C# project with CRUD operations. This project will allow us to add, update, and delete users.

## Getting Started

### Launch Codespace
Start by launching your Codespace environment.

### Familiarize Yourself with the Project Directory
Take a moment to explore the project directory. (Surprise! It's empty)

### Install Copilot Extension
Navigate to the extensions tab on the left hand side of the codespace. Search 'copilot' and install the GitHub Copilot extension. Note that this will also install the chat feature. 

<img src="./images/copilot_extension.png" alt="GitHub Copilot Extension" width="250"/>



### Open Copilot Chat
Open up the chat feature and say hello to Copilot!

### Explore Built-in Commands
GitHub Copilot chat includes built-in commands (hotkeys) for common tasks. You can explore these using the `/` command in chat.

## Creating a New Workspace

### Create a New Workspace
Start typing `new` in the chat and choose the `new workspace` option. Ask Copilot to `scaffold a new C# project`. Copilot will create a new workspace and present you with a convenient button to create the workspace for you. Click this button, name the workspace `my-csharp-project` (see second image below) and wait for the Codespace to reload. (see image below)

<img src="./images/new_workspace.png" alt="GitHub Copilot New Workspace Command" width="250"/>


<img src="./images/workspace_name3.png" alt="GitHub Copilot New Workspace Command" width="600"/>



### Explore the New Project
Once the Codespace has reloaded, familiarize yourself with the contents of the new project and its directories.

## Building the Application
We will use Copilot in the IDE to create a `User` class with `ID`, `Name`, and `Email` properties, along with their respective `get` and `set` methods.


### Create a User Class

We will use Copilot in the IDE to create a `User` class with `ID`, `Name`, and `Email` properties, along with their respective `get` and `set` methods.

Navigate to the `/src/classes` directory and create a new file called `User.cs`. At the top, we will write a comment to prompt GitHub Copilot:

```csharp
// setup a class called User with 3 properties: Id, Name, and Email
// The properties are defined using the get and set accessors.
// Use the appropriate namespace for the project (my_csharp_project.Classes).
// The set accessor assigns a new value to the property, and the get accessor returns the property value.
```

The contents returned should be something along the lines of:

```csharp
using System;

namespace my_csharp_project.Classes
{ 
    public class User
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Email { get; set; }
    }
}
```

Alternatively, you may begin typing into the file the solution above, and see what suggestions Copilot returns along the way. 

### Create a User Service
We will ask **Copilot chat** to create the `UserService`. This service will handle the CRUD operations for our `User` objects.

Navigate to the `/src/classes` directory and create a new file called `UserService.cs`. We will use GitHub Copilot chat to generate the contents of this service file. 
In the chat interface, prompt copilot to 

```csharp 
// We are creating a simple C# console application that performs basic CRUD operations on a list of users. Create a UserService class in the my_csharp_project.Classes namespace that manages a list of User objects. The User class has properties Id, Name, and Email. The UserService class should have methods to add a user, get a user by id, update a user's details, and delete a user by id.
```


The response should contain code similar to the following solution below: 

```csharp
using System.Collections.Generic;
using System.Linq;
namespace my_csharp_project.Classes{ 
public class UserService
{
    private List<User> users = new List<User>();

    public void AddUser(User user)
    {
        users.Add(user);
    }

    public User GetUser(int id)
    {
        return users.FirstOrDefault(u => u.Id == id);
    }

    public void UpdateUser(User user)
    {
        var existingUser = GetUser(user.Id);
        if (existingUser != null)
        {
            existingUser.Name = user.Name;
            existingUser.Email = user.Email;
        }
    }

    public void DeleteUser(int id)
    {
        var user = GetUser(id);
        if (user != null)
        {
            users.Remove(user);
        }
    }
}
}
```
Use the built-in `insert` button (see below) in the chat response interface to insert at the cursor in your `UserService.cs` file. 

<img src="./images/copilot_insert.png" alt="GitHub Copilot Insert" width="250"/>

### Create the Entry Point
Navigate to the `Program.cs` file (in the root directory) and use Copilot chat to create the entry point for our project.

```csharp 
// This file contains the Main method where you create an instance of UserService and perform operations like adding, getting, updating, and deleting users. 
// create a main program that uses the UserService class to add, get, update, and delete a User. The User class has properties Id, Name, and Email. The UserService class has methods to add a user, get a user by id, update a user's details, and delete a user by id. Demonstrate these operations in the Main method.
```
The response should contain code similar to the following solution below: 

```csharp 
using System;
using my_csharp_project.Classes;

public class Program
{
    static void Main(string[] args)
    {
        UserService userService = new UserService();

        // Add a user
        userService.AddUser(new User { Id = 1, Name = "John Doe", Email = "john.doe@example.com" });

        // Get a user
        User user = userService.GetUser(1);
        Console.WriteLine($"Got user: {user.Name}");

        // Update a user
        user.Name = "Jane Doe";
        userService.UpdateUser(user);

        // Delete a user
        userService.DeleteUser(1);
    }
}
```
Use the built-in `insert` button (see below) in the chat response interface to insert at the cursor in your `UserService.cs` file. 

<img src="./images/copilot_insert.png" alt="GitHub Copilot Insert" width="250"/>

### Add additional users
Use Copilot to add additional users in the `Program.cs` file. 

### Review the Code
Another use case for GitHub Copilot chat is code review. For an extra set of eyes, you may highlight the contents of each of the three files and ask Copilot to review them for syntax errors or any other issues.

Alternatively, you may use the built-in `/workspace` command and ask Copilot chat to check the contents of specific files for errors (see image below):

<img src="./images/workspace_check.png" alt="GitHub Copilot Insert" width="250"/>


### Generate the .csproj File
Navigate to your `.csproj` file in the `/src` directory, highlight any contents, and ask Copilot to generate the contents for the `.csproj` file. Ask Copilot to use .NET version 7 and to include the appropriate `ItemGroup` elements.

```csharp 
// Create a .NET project file that targets .NET 7.0, outputs an executable, and includes Program.cs and all C# files in the Classes directory
```

The response should contain code similar to the following solution below: 

```csharp
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net7.0</TargetFramework>
        <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
    </PropertyGroup>

    <ItemGroup>
        <Compile Include="Program.cs" />
        <Compile Include="Classes/*.cs" />
    </ItemGroup>

</Project>
```

## Running the Application

### Build the Project
Now we're ready to build the project. Navigate to the `/src` directory via the terminal and run `dotnet build`. If you run into any errors, copy and paste the contents of the error into Copilot chat and use it as an aide to guide you towards a fix. 

### Run the Application
Use `dotnet run` to run the application.

## Testing and Debugging

### Generate Tests
Use Copilot to generate tests for your application. Test files are located in the `/tests` directory.

### Debugging
If you run into errors, you can use Copilot chat to assist you. Consider using the built-in `/fix` command.

---

Enjoy the workshop and happy coding!

# Challenge Exercises

## Intermediate

- Create a method to assign roles to a user
- Create a method to search for users by name
- Modify the GetUser method to support pagination
- Create a method to log events in the application
- Create an API controller for the User class
- Create unit tests for the UpdateUser method
- Create unit tests for the getUser method
- Create unit tests for the addUser method

## Advanced 
- Modify the AddUser method to store user data in a database 
