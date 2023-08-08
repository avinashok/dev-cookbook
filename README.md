# Developer Cheat Sheet

Some commands &amp; shortcuts I use in daily life. Also contains some interesting prompts as well for Generative AI tools.

## Contents

- [Docker Commands](#Docker Commands)
- [Conda virtual environments](#Conda virtual environments)
- [Package Management](#package-management)
- [Version Control (Git)](#version-control-git)
- [Network and Connectivity](#network-and-connectivity)
- [Miscellaneous](#miscellaneous)

## Docker Commands

### Docker Commands for running a docker file

- `docker login` - Enable logging in with SSO if connected to VPN/Remote Connect.
- `docker pull eyctpeu-smartreviewer-nonprod-docker.jfrog.io/module_base:3.8` - A working sample command to pull a repository.
- `docker images` - List the available docker images.
- `docker build . -f package_module.dockerfile -t crossdocumentcomparison_v1` - Build a docker image using the available dockerfile in the repository
- `docker run -it -e PYTHONUNBUFFERED=1 --publish 8080:8080 crossdocumentcomparison_v1` - Run & publish the docker image
- `docker-compose -f db-docker-compose.yaml up` - 



## File Operations

### Creating and Manipulating Files

- `touch [filename]` - Create an empty file.
- `cp [source] [destination]` - Copy files or directories.
- `mv [source] [destination]` - Move or rename files or directories.
- ...

## Package Management

### Package Installation and Management

- `npm install [package]` - Install a Node.js package.
- `pip install [package]` - Install a Python package.
- `brew install [package]` - Install a package using Homebrew.
- ...

## Version Control (Git)

### Basic Git Commands

- `git clone [repository]` - Clone a remote repository.
- `git init` - Initialize a new Git repository.
- `git add [file]` - Stage changes for commit.
- `git commit -m "message"` - Commit staged changes.
- ...

## Network and Connectivity

### Network Related Commands

- `ping [hostname]` - Send ICMP echo requests to a host.
- `curl [url]` - Fetch content from a URL using HTTP/HTTPS.
- `ssh [user]@[hostname]` - Connect to a remote host using SSH.
- ...

## Miscellaneous

### Other Useful Commands

- `echo [text]` - Display a message on the terminal.
- `grep [pattern] [file]` - Search for a pattern in a file.
- `chmod [permissions] [file]` - Change file permissions.
- ...

---

Feel free to contribute by adding your own frequently used commands or improving the documentation. If you have questions or suggestions, please open an issue or submit a pull request.

**Disclaimer:** Please use these commands with caution, as some actions can have irreversible effects on your system or data.


# Appendix





 

 

First Time Cloning an Azure/Git repository:

For Windows-> Install Git Credentials Manager
For Mac->
brew tap microsoft/git

brew install --cask git-credential-manager-core

 

And Log in from browser

 

git clone https

 

GIT Commands:

git checkout origin/master
git status
git pull origin develop
git log
git checkout -b <new branch name>
-- make changes--
git status
git add <filenames>
git commit -m "comments"
git push origin -u <new branch name>:<remote branch name>
 

Other commands:

git diff
git stash
git reset --merge
git fetch
git checkout -f origin/master
 

git pull origin bug/2457988-cross_document_error
 

PEP8 Enforcing:

`flake8 <code path> --max-line-length=120`

or

python -m flake8 <code path> --max-line-length=120

pip freeze | grep pandas

 

Conda Environment using Yaml file:

 

conda create -y -n "<env name>" python=3.8 pip=21.1

conda activate <env name>

conda env create -f conda.yml

 

To update an existing conda environment:

conda env update --file "./Dependencies/conda.yml" --prune

 

If organization is not allowing to create a conda env:

conda config --set ssl_verify no

python -m pip install PACKAGENAME --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=files.pythonhosted.org

 

Command for testing:

python -m pytest --rootdir=./Tests --junitxml=./Tests/junit/unit-test.xml -vv -rP

pytest -v tests/my-directory/test_demo.py::test_specific_function

 

To reduce size of PDFs in PDF X-Change Editor:

Organize -> Resize -> Percentage -> [Reduce to a size which fit requirement].
(Keep 'Context Scale Options' all check)

 

 

 

To beautify JSONs:     Ctrl + Alt + L (Option + cmd + L on Mac)

To select a url fully: Ctrl + W

 

Extend Selection:

In Mac: Option + Up or Option + Down

In Windows: Ctrl + W

 

 

 

Azure Commands (from https://github.com/ferhaty/azure-cli-cheatsheet):

 

Login with web: az login
 Login in CLI: az login -u myemail@address.com
 List accounts: az account list
List all locations: az account list-locations
az account get-access-token --output json --resource https://vault.azure.net
List all my resource groups: az resource list
Get what version of the CLI you have: azure --version
Get help: azure help
List your VMs: az vm list
Check if logged in or not: az account show -o jsonc
 

 
 conda create -y -n "pipeline-env" python=3.9 pip=21.1
 conda env list
 conda activate pipeline-env
 conda deactivate


 
