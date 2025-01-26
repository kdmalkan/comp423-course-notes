# Setting up a dev container for Go - tutorial 

* Primary author: [Krisha Malkan](https://github.com/kdmalkan/comp423-course-notes)

* Reviewer: [Kiara Smith](https://github.com/kiaras4)

``` py
This codeblock is to show you what a codeblock looks like.
```

**Welcome!** This tutorial will help you create a "Hello, World!" using the language Go.

## Prerequisites:

- **GitHub account**
If you do not have an account, make an account to be able to do the rest of the tutorial.

- **Git installed**

- **Visual Studio Code (VS Code)**
Install VS Code is not already installed on your computer.

- **Docker installed**
Install Docker if not already installed on your computer.

- **Dev Containers extension for  VS Code**

## Part 1: Getting Started

First, we will need to create a directory and initialize our repisitory on GitHub.

1. Open your terminal or command prompt.


2. Create a new directory for your hello comp423 program.

    ```
    mkdir <name-of-directory>
    cd <name-of-directory>
    ```

3. Initalize your new Git repository.

    ```
    git init
    ```
    
4. Create a README file:

    ```
    echo "# Hello Comp423 in Rust" > README.md
    git add .
    git commit -m "Initial commit with README"
    ```

Now that we have our local repository setup, let's create our GitHuB repository:

1. Log into your GitHub account and head straight to the Create a New Repository page here.
2. Fill in the following details:

    Repository Name: hello-comp423-rust

    Description: "Hello COMP423 in Rust"

    Visibility: Public
3. Do not initialize the repository with a README, .gitignore, or license
4. Click Create Repository

We can now onnect out local and remote repositories.

1. Add GitHub repository as a remote:

```
git remote add origin https://github.com/<your-username>/hello-world-rust.git
```

Change ``<your-username>`` with the username you have set up in GitHub.

2. Ensure your default branch name is ``main`` by using ``git branch`` in your terminal. If it's not ``main``, rename it using ``git branch -M main``.

3. Push local commits to your GitHub repository

```
git push --set-upstream origin main
```

4. Using ``git log`` in your terminally will show you the commit ID and message. This should match the ID of the most recent commit on your GitHub after you reload it.

## Part 2: Development(Dev) Container Set Up and Configuration

### Set-up

1. Open the directory you created in VS Code.
    - Can be done like so: File > Open folder

2. Create a .devcontainer directory at the root of the project with a file name "devcontainer.json" Path should look like this:

    ```
    .devcontainer/devcontainer.json
    ```

### Configuration

The devcontainer.json file you just created defines the configuration needed for your development environment. We will be adding the following specification:

1. **name:** descriptive name for the dev container

2. **image:** This specifies the Docker image to use. We will use one of Microsoft's base images of the latest version of a Rust environment.

3. **customizations:** Adds important & useful configurations to VS Code, such as installing the Rust extension. Searching for VSCode extensions on the marketplace will bring up the string identifier of each extension in its sidebar. Adding extensions this way is important as it ensures other developers on your project will have those extensions installed in their own dev containers automatically. 

    ```
    {
        "name": "Go Hello World",
        "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
        "customizations": {
            "vscode": {
                "settings": {},
                "extensions": [
                    "ms-vscode.go",
                    "davidanson.vscode-markdownlint"],
            }
        }
    }
    ```

### Post-Configuration - Reopen Project in a VS Code Dev Container

Here we will reopen the project in the container. You can do this by doing ``Ctrl+Shift+P`` (or ``Cmd+Shift+P`` on Mac), then type "Dev Containers: Reopen in Container," selecting the option once it comes up. The image will be downloaded and any requirements installed. It may take a few minutes.

Once the setup is complete, close the current terminal tab by pressing the trash can button. Open a new terminal in VS Code and run ``go version`` to ensure the dev container is running a recent version of Go. 




## Part 3: The Hello Comp423 Program!

We will now be writing a Hello Comp423 program using Go.

1. Run these command lines

    ```
    cargo new hello_comp423 --vcs none
    cd hello_comp423
    ```

    These lines of code will create a hello_comp423 directory for your first Go source code. 

 2. Enable dependency tracking for your code.

 Now we will need to enable dependency tracking for your code by creating a go.mod file. When your code imports packages contained in other modules, you manage those dependencies through your code's own module. 
 Run the following: 

```
    go mod init example/hello_comp423_students
    ```

3. In your text editor, create a file hello.go in which to write your code.

4. Paste the folllowing code into the hello.go file

```
    package main

    import "fmt"

    func main() {
        fmt.Println("Hello Comp423")
}
    ```

In this code we first declared a main package. Then we import the  fmt package, which contains functions for formatting text, including printing to the console. Then we implement a main function which will print Hello Comp423 to the console.

5. Run your code

```
    go run .
    ```

#### Congratulations! You ran your first program using Rust!
