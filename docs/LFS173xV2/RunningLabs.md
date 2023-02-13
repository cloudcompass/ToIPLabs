# General Instructions for Running Labs<!-- omit in toc -->

This page contains general instructions for running labs for the [Linux
Foundation's edX LFS173x Becoming an Aries
Developer](https://www.edx.org/course/becoming-a-hyperledger-aries-developer)
online course. We'll provide a link to this page in most labs to give you some
context in completing the labs.

- [Labs Content](#labs-content)
- [Running Options: Play with Docker and Locally with Docker](#running-options-play-with-docker-and-locally-with-docker)
  - [Running on Play with Docker](#running-on-play-with-docker)
    - [Play WIth Docker Prerequisites](#play-with-docker-prerequisites)
    - [Basic Usage](#basic-usage)
    - [Ports](#ports)
    - [Editing Files](#editing-files)
  - [Running on Docker Locally](#running-on-docker-locally)
    - [Local Docker Prerequisites](#local-docker-prerequisites)
    - [Local Docker Basic Usage](#local-docker-basic-usage)
    - [LocalHost Ports](#localhost-ports)
  - [Running on Bare Metal](#running-on-bare-metal)

## Labs Content

In the interest of reducing the duplication of documentation and documents, the labs in this course use tutorials and examples in the open source repositories that we discuss. This greatly increases the chance that participants will always be seeing the latest information, with a slight risk that the connection between the labs and the content will get out of sync. We do our best to keep the content in sync.

We really appreciate the contributions of all those that have helped in building the examples referenced in this course. Do take a look at the GitHub IDs of the contributors and when you get a chance, thank them!

## Running Options: Play with Docker and Locally with Docker

In many of the labs we will let you know that you have the option of running the lab on your own machine using Docker or directly in your browser using a web service called "Play with Docker," that is operated by Docker, Inc. The following gives you a background on both options:

### Running on Play with Docker

[Play with Docker](https://labs.play-with-docker.com/) is a tool from [Docker, Inc.](https://docker.com/) that allows you to access a Linux command line on which you can run docker scripts in your browser. The environment is temporary (lasting up to 4 hours) and should not be used for development, but it is a great playground for playing with open source software examples without having to add anything to your own system.

#### Play With Docker Prerequisites

To use Play with Docker, you must have a modern browser and a free account on [Docker Hub](https://hub.docker.com/).

#### Basic Usage

To get to a command line for running a lab, do the following:

- Go to [https://labs.play-with-docker.com](https://labs.play-with-docker.com/) (called Play with Docker)
- Click `Start` and the `+ Add New Instance` to start a terminal window

Once running a terminal window, follow the specific examples for the lab. The Linux instance you are using has everything you need to run the labs preinstalled, such as `git` and `docker`, plus an editor if you want to update files as you experiment.

If instructed to open an additional terminal, hit the `+ Add New Instance` again.

#### Ports

Play with Docker automatically exposes publicly-accessible ports from running docker containers by providing links to the ports in the header section of the page, above the terminal. When instructed to click (for example) `http://localhost:8080` in a tutorial, click the `8080` link in the header of the Play with Docker page.

#### Editing Files

If you need to edit files when using Play with Docker, you can use `vi` from the terminal command line, or there is a browser based file explorer and GUI editor. To get to that, click the `Editor` button in the header section and a window will popup. Enlarge the window and use the file explorer to find the file you want to edit. Double click on the file and you will be in the editor.

Remember that all your files are deleted when your Play with Docker session closes, so if you do want to preserve your files, make sure you grab them before you exit.

### Running on Docker Locally

To run the examples locally, open up a `bash` terminal session on your local machine. On Mac and Linux, the default `terminal` apps use bash (or a bash-compatible shell). On Windows, we recommend using `git-bash` that is installed with git on Windows. The labs will not work using Windows `cmd` or `powershell` command lines.

#### Local Docker Prerequisites

When you run the labs locally, you need the following prerequisites installed on your system:

- A terminal command line interface running `bash` shell.
- Docker, including Docker Compose—Community Edition is fine.
  - If you do not already have Docker installed, open [this link](https://docs.docker.com/install/#supported-platforms) and then click the link for the installation instructions for your platform.
- Git
  - [This link](https://www.linode.com/docs/development/version-control/how-to-install-git-on-linux-mac-and-windows/) provides installation instructions for Mac, Linux (including if you are running Linux using VirtualBox) and native Windows (without VirtualBox).

#### Local Docker Basic Usage

To get to a command line for running a lab, open the (bash) terminal app on your system. If instructed in labs, open up additional terminal sessions/tabs.

Once running a terminal window, follow the specific examples for the lab.

#### LocalHost Ports

The tutorials generally assume that you are running docker on your local system and the ports exposed by the various docker containers are available on `localhost` (for example, `http://localhost:8080`).

### Running on Bare Metal

All of the labs that you can run locally use Docker. You can run the labs directly on your own system without Docker, but we don’t provide instructions for doing that, and we highly recommend you not try that until you have run through them with Docker. Because of differences across systems, it’s difficult to provide universal instructions, and we’ve seen many developers spend far too much time trying to get everything installed and working versus learning from the example.
