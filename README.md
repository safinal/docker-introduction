# Introduction to Docker

Imagine that you have developed your open-source application and pushed the project to GitHub. After a week when you check your email, you see that there are several emails about your last project from people who failed to run your project. When you check their issues you realize that each one of them has a different problem, one with the dependencies versions, the other with the configuration settings and so on. How can you solve this problem? By writing a long boring installation guide? This may help but will not solve the problem. Here is where **Docker** comes to the rescue.

## What is Docker?

Let's start with the official definition from the [Docker documentation](https://docs.docker.com/get-started/overview/):

> Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

This means that by using Docker, if an application works on your development machine, it can run in the same way on other machines. But how can this happen? By packaging the application with all its requirements and passing it to an isolated environment called **Container**. It allows multiple applications use different versions of some software along with each other in the same machine without messing with each other.

### Dockerizing an application

A Dockerized application is an application that `Dockerfile` has been added to it. `Dockerfile` is a plain text file which includes instructions that Docker uses to package up an application into an **image**. This image contains everything the application needs to run such as:

- A cut-down operating system
- A runtime environment (eg Python)
- Application Files
- Third-party libraries
- Environment variables

Therefore, if people get our project, they don't have to spend hours on installing dependencies and setting configurations! They just have to run a single command.

## Virtual Machines vs Containers

**Virtual Machine** is an abstraction of a machine (physical hardware) while **Container** is an isolated environment for running an application. The following table shows some of their differences:

|        Virtual Machines        |                Containers                |
| :----------------------------: | :--------------------------------------: |
| Each VM needs a full-blown OS. | All containers share the OS of the host. |
|         Slow to start          |              Start quickly               |
| Need more hardware resources.  |      Need less hardware resources.       |

### Virtual Environments

In some programming languages like Python, there is a similar concept called **virtual environment**. From the [Python documentation](https://docs.python.org/3/library/venv.html):

> A virtual environment is an isolated Python environment where a project’s dependencies are installed in a different directory from those installed in the system’s default Python path and other virtual environments.

Here is a nice picture describes the differences between the VM, VE and Docker Container architecture:

![VM, VE & Container Differences](https://miro.medium.com/max/700/1*qZQwwQguL61ut6Pz94hiPA.png)



## Architecture of Docker

Docker uses a client-server architecture. The client component talks to the Docker Engine (server component) through a RESTful API. Docker Engine takes care of building, running, and distributing Docker containers.

![Architecture of Docker](https://docs.docker.com/engine/images/architecture.svg)

## Installing Docker

You can download and install Docker on multiple platforms such as **macOS**, **Windows** and **Linux**. **Docker Engine** is available on Mac and Windows through **Docker Desktop** which is the combination of Docker Engine plus a bunch of other tools. There is a complete guide on the installation in the *Docker official documentation*, based on your operating system go to one of the following links:

- [Docker Desktop for Mac](https://docs.docker.com/desktop/mac/install/)
- [Docker Desktop for Windows](https://docs.docker.com/desktop/windows/install/)
- [Docker Engine for Linux](https://docs.docker.com/engine/install/)

After the installation, open the terminal and run this command:

```bash
$ docker version
```

You must see the **Client version** and the **Server version** in the terminal; otherwise, Docker is not installed correctly on your machine.

## A Simple Example

1. Create a directory named `hello-world`.

2. In the directory create a file named `app.js` and put the code below in it.

   ```javascript
   console.log("Hello World!")
   ```

3. Create the `Dockerfile` and put the code below in it.

   ```dockerfile
   FROM node:alpine
   COPY . /app
   WORKDIR /app
   CMD node app.js
   ```

4. Open the terminal in the directory and execute the following command:

   ```bash
   $ docker build -t hello-world .
   ```

5. Now, guess what is the output of this command: 

   ```bash
   $ docker run hello-world
   ```

   <details><summary>See the answer</summary>
   <p>

   ```
   Hello World!
   ```

   </p>
   </details>

