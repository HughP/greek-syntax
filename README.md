# The Greek Syntax Jupyter Notebook Environment

Greek Syntax is a Jupyter Notebook environment for querying the Greek New Testament using XQuery, XPath, or Python.  It supports queries on syntax trees as well as the base text.

See the [Greek Syntax tutorial](http://jonathanrobie.biblicalhumanities.org/assets/greeksyntax-tutorial.html) for an overview of its capabilities.

The data for these queries comes from these GitHub repos:

- https://github.com/biblicalhumanities/Nestle1904
- https://github.com/biblicalhumanities/greek-new-testament
- https://github.com/biblicalhumanities/levinsohn
- https://github.com/translatable-exegetical-tools/Abbott-Smith

# Getting Started

There are two ways to install this package.  You can either install it directly on your computer or use a Docker image (which is easier, but apparently does not work on some operating systems).

## Installing with Docker

If it works on your computer, the easiest way to install is to use the Docker image.  First, install Docker:

- [Install Docker](https://docs.docker.com/install/)

- If you are running on Windows, you must [switch to Linux containers](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers) in Docker before running the container.

- Run this command from the command line:

  ```
  $ docker run -v ${PWD}:/home/jovyan/work -p 8888:8888 biblicalhumanities/greek-syntax
  ```
  
  **Windows Users**: On Windows Systemsyou can either use the above command with PowerShell or use `%cd` instead of `${PWD}` in the above command.
  
  The `-v` option tells Docker to make your host machine's local directory available to the Docker container so you can mount and save notebooks.
  
  The `-p` option maps a container's port to a port on your local machine.  In this case, we map the container's port `8888` to the local machine's port `8888`. If you get an error message saying that port 8888 is already in use on your computer, try `-p 8880:8888`, which maps to port 8880 instead. If that's already in use, try 8881, 8882, etc.

- When it runs, you will see a message with a URL to put in a web browser:

  ```
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=431d559093f580607f51cc1ed0dd3d86db0abc743c2d049e
  ```

  Follow the instructions - copy the URL into the address bar of a web browser. If you changed the port to 8080, change `localhost:8888` to `localhost:8880` in the URL before you open it.

-  You should see a directory tree that looks like this:

   <img src='./img/Directories.png' />

   Click on the `work` directory and you will see a list of files.  Open the Greek Syntax Tutorial, which will teach you how to use the Greek Syntax package in a Jupyter Notebook.

   <img src='./img/GreekSyntaxTutorial.png' width="50%"/>

## Installing Greek Syntax, Jupyter, and BaseX Directly

You can also use Greek Syntax directly on your computer without Docker.  You need the Greek Syntax package, Jupyter, and BaseX.  There is a script that installs the data into BaseX.

- Clone this repository using `git`:

  ```
  $ repos: git clone https://github.com/biblicalhumanities/greek-syntax
  ```

  Then go to the `greek-syntax/python` directory and install the package as follows:

  ```
  $ python: python setup.py install
  ```
  
- Install Jupyter using [these instructions](https://jupyter.org/install).

- Install BaseX using [from here](http://basex.org/download/).

- Download data from repositories and load it into the database using the `data/load_data.sh` script:

  ```
  $ data: ./load_data.sh 
  ```
  
- Go to the `notebooks` directory and start Jupyter:

  ```
  $ notebooks: jupyter notebook
  ```
  
  You will see a message like this:
  
  ```
      Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8890/?token=00cdcc7b167d94d2ceac84fe38d0fcfff17a76ae921c12ad
  ```
  
  Do what it says - copy the URL into a web browser.
  

-  You should see a directory tree that looks like this:

   <img src='./img/NotebooksDirectory.png' />

   Click on the `work` directory and you will see a list of files.  Open the Greek Syntax Tutorial, which will teach you how to use the Greek Syntax package in a Jupyter Notebook.

   <img src='./img/GreekSyntaxTutorial.png' width="50%"/>

# Implementation

Greek Syntax is implemented as a Docker container based on [`jupyter/minimal-notebook`](https://github.com/jupyter/docker-stacks/tree/master/minimal-notebook). It uses the marvelous [BaseX](basex.org) database for all XML processing and querying.

# Building a Docker image

To build a Docker image, use this script:

`build.sh`

# Directory Structure

- *docker* - Files we use to build the Docker container.
- *python* - Source code for the Python module that we install in the Docker container.
- *data* - Where data from corpora is to be placed.

```
.
├── data
│   ├── build
│   ├── github
│   ├── load_data.sh
│   └── README.md
├── docker
│   ├── assets
│   ├── build.sh
│   ├── Dockerfile
│   └── VERSION
├── img
├── LICENSE
├── notebooks
│   ├── AskingQuestions.ipynb
│   ├── greeksyntax-tutorial.ipynb
│   ├── Greek\ Syntax\ Tutorial.ipynb
│   ├── Reflexive\ Pronouns.ipynb
│   ├── SplitConstituents.ipynb
│   └── Verbless\ Clauses.ipynb
├── python
└── README.md

```
