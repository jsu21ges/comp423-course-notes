# Setting up a dev container for Go

* Primary author: [Justin Su](https://github.com/jsu21ges)
* Reviewer: [Jeffrey Zhu](https://github.com/JeffJeffisawesome)

## Introduction

Welcome! In this tutorial, you'll learn how to build a containerized environment from which you can code up and run your first program in Go. Yippee!

!!! note "Side Note"

    Go is a **Functional Language**. The programming languages that you already familiar with are likely *Object Oriented Languages*. These include ```python```, ```c/c++```, ```java```, and many other languages. The key difference between Functional Languages and Object Oriented Languages is that all the data in a Function Language is ***immutable***. An immutable value is a primitive value that cannot change. Freaky, right?

## Prerequisites

For this tutorial, make sure to:

 - **Have a Github account**: You can sign up [here](https://github.com/)
 - **Have git installed**. You can install it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
 - Download and install **Visual Studio Code** (VS Code) from [here](https://code.visualstudio.com/).
 - **Install Docker:** get it [here](https://www.docker.com/products/docker-desktop).

With that out of the way, we can get into the good stuff.

## Project Setup (part 1): Create a git repository

### Create the repository
1. Open up your terminal in your local machine.
2. Create a new directory for your project:
```
mkdir go-project
cd go-project
```
3. Initialize a new git repository:
```
git init
```
4. Create a README.md file:
``` bash
echo "# My First Go Project" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Linking to Github
1. Log in to your Github account and navigate to the [Create a New Repository](https://github.com/new) page and fill in the details as follows:
     - **Repository Name:** ```go-project```
     - **Description:** "My first go project!"
     - **Visibility:** Public
2. Do not initialize the repository with a README, .gitignore, or license. 
3. Click **Create Repository**
4. Link your local repository to GitHub. You can do this in terminal with:
```
git remote add origin https://github.com/<your-username>/go-project.git
```
Replace `<your-username>` with your GitHub username
5. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`.
6. Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```

Congrats! You've set up the repository for your first Go Project!

## Project Setup (part 2): Setting Up the Development Environment

Now that you have the repository set up, we can get started on the Devoloper Container.

### Add Development Container Configuration

1. In VSCode, open the ```go-project``` directory. You can do this via: File > Open Folder
2. Install the **Dev Containers** extension for VS Code.
3. Create a ```.devcontainer``` directory in the root of your project with the following file inside of this "hidden" configuration directory:
```
.devcontainer/devcontainer.json
```

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- `name`: A descriptive name for your dev container.
- `image`: The Docker image to use, in this case, the latest version of a Go environment. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!
- `customizations`: Adds useful configurations to VS Code, like installing the Python extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

```
{
  "name": "COMP423 Course Notes",
  "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["golang.go"]
    }
  }
}
```

### Reopen the Project in a VSCode Dev Container

!!! warning "ATTENTION"
    Make sure Docker is running before proceeding to the next step. Or else...

Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running `go version` to see your dev container is running a recent version of Go without much effort!

## Making your first Go Program!

With all of that out of the way, we can finally get to the good stuff!

1. In your terminal, create a directory for your first Go source code.
```
mkdir hello
cd hello
```
2. Then in the terminal, create your first Go file:
```
$ go mod init example/hello
go: creating new go.mod: module example/hello
```
3. In VS Code, create a file hello.go in which to write your code.
4. Paste the following code into your hello.go file and save the file.
```
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```
 This is your Go code. In this code, you: 
    - Declare a `main` package (a package is a way to group functions, and it's made up of all the files in the same directory).
    - Import the popular [fmt package](https://pkg.go.dev/fmt/), which contains functions for formatting text, including printing to the console. This package is one of the [standard library](https://pkg.go.dev/std) packages you got when you installed Go.
    - Implement a main function to print a message to the console. A `main` function executes by default when you run the main package.
5. Run your code to see the greeting.
```
$ go run hello.go
Hello COMP423
```
Alternatively you could also run:
```
$ go build hello.go
$ ./hello
```
This will give you the same result!

!!! note "Side Note"
    Think of `build` as similar to `gcc` for `C` code. It's job is to convert human readable code into a machine executable file to be run by the computer. From there, you can run the executable directly with `./<executable file name>`.

Now you might be thinking, what's the difference between `run` and `build`? It's all for the sake of convenience: ```go run hello.go``` takes ```go build hello.go``` and ```./hello``` and combines them into a single command. Thanks google.

## Conclusion

Congratulations! You've successfully created and ran your first Go program!