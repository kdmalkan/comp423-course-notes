# Setting up a dev container for Go - tutorial 

* Primary author: [Krisha Malkan](https://github.com/kdmalkan/comp423-course-notes)

* Reviewer: [Kiara Smith](https://github.com/kiaras4)


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

3. Initalize your Git repository.

    ```
    git init
    ```
    
4. Create a README file:

    ```
    echo "# Hello Comp423 in Go" > README.md
    git add .
    git commit -m "Initial commit with README"
    ```

Now that we have our local repository setup, let's create our GitHuB repository:

1. Log into your GitHub account and click on the Create a New Repository page.

2. Fill in the following details for your new repsitory:

    Repository Name: hello-comp423-go

    Description: "Hello COMP423 in Go"

    Visibility: Public

3. Do not initialize your repository with a README, .gitignore, or license

4. Click Create Repository

We can now connect our local and remote repositories.

1. Add GitHub repository as a remote repository:

    ```
    git remote add origin https://github.com/<your-username>/hello-comp423-go.git
    ```

    Change ``<your-username>`` with the username of your GitHub.

2. Ckeck to see if your default branch is ``main`` by using ``git branch`` in your terminal. If it's not ``main``, rename it using ``git branch -M main``.

3. Push local commits to your GitHub 

    ```
    git push --set-upstream origin main
    ```

    !!!question "What's --set-upstream?"

        ``--set-upstream`` allows us to makes the main branch track the remote branch. This allows future pushed and pulls to be done without needing to specify the branch name. So, when working on your local main branch, you can use ``git push origin``.

        * ``-u`` is the short flag of ``--set-upstream``

4. Using ``git log`` in your terminal will show you the commit ID. Check to see if this matches the ID of the most recent commit on your GitHub after you reload it.

## Part 2: Development(Dev) Container Set Up and Configuration

### Set-up

1. Open the directory you created in VS Code.
    - Can be done like so: File > Open folder

2. Create a directory named .devcontainer at the root of the project with a file inside of it named "devcontainer.json". The path should look like this:

    ```
    .devcontainer/devcontainer.json
    ```

### Configuration

The devcontainer.json file you just created defines the configuration needed for your development environment. We will need to add the following into the file.

1. **name:** This will give a descriptive name for your dev container

2. **image:** This specifies the Docker image to use. We will use one of Microsoft's base images of the latest version of a Go environment.

3. **customizations:** Adds important & useful configurations to VS Code, such as installing the Go extension. Searching for VSCode extensions on the marketplace will bring up the string identifier of each extension in its sidebar. 

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

Here we will reopen the project in the container. You can do this by doing ``Ctrl+Shift+P`` (or ``Cmd+Shift+P`` on Mac), then type "Dev Containers: Reopen in Container," and select it. The image will be downloaded and any requirements installed. It is normal for it to take a few minutes.

Once the setup is complete, you should close the current terminal tab by pressing the trash can button. Open a new terminal in VS Code and run ``go version`` to check if the dev container is running a recent version of Go. 

!!! success

    You should see a similar version in the output as seen below:

    ```
    go version go1.23.4 linux/amd64
    ```



## Part 3: The Hello Comp423 Program!

We will now be writing a Hello Comp423 program using Go.

1. Run these command lines

    ```
    mkdir hello_comp423
    cd hello_comp423
    ```

    These lines of code will create a hello_comp423 directory for your first Go source code. 

 2. Enable dependency tracking for your code.

    Now we will need to enable dependency tracking for your code by creating a go.mod file. When your code imports packages contained in other modules, you manage those dependencies through your code's own module. 

    Run the following: 

    ```
    go mod init example/hello_comp423_students
    ```

    !!! success

        You should see this output in your terminal:

        ``go: creating new go.mod: module example/hello_comp423_students``

3. In your text editor, create a file hello.go in which to write your code.

    !!!note
        The hello.go file should be placed in the hello_comp423 directory that was made in step 1 of this section.

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
6. Build subcommand as an Alternative
    Instead of usuing go run we can use go build. For this option, instead of manually making the hello.go file you would run: 

        ```
        go build main.go
        ```

    This command compiles the Go program and generates a binary executable file. Then on this file copy and paste the code that was provided in step 4. To run the file run the code:

        ```
        ./hello
        ```

    This option is similar to the gcc command. Both commands complie to generate a binary file. Then you run the binary manually. ```go build``` is different then ```go run``` because it creates a complied binary. 

#### Congratulations! You have created your first program using Go!

!!! info

    The first part of this tutorial was inspired by the "Starting a Static Website Project with MkDocs by Kris Jordan" page on the Comp423 website. 

    The documentation that was used to create the Hello Comp423 program was inspired by a website called "Go." The documentation can be found here: https://go.dev/doc/tutorial/getting-started