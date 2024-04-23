# Developer Cheat Sheet

Some commands &amp; shortcuts I use in daily life. Also contains some interesting prompts as well for Generative AI tools.

## Contents

- [Git Commands](#git-commands)
- [Conda virtual environments](#conda-virtual-environments)
- [PEP8 Checking in code](#pep8-checking-in-code)
- [Docker Commands](#docker-commands)
- [Azure Commands](#azure-commands)
- [Kubernetes Commands](#kubernetes-commands)
- [Linux Commands](#linux-commands)
- [Prefect Commands](#prefect-commands)
- [Other Tips](#other-tips)


## Git Commands
First Time Cloning an Azure/Git repository:
- For Windows: Install Git Credentials Manager
- For Mac:  
  - `brew tap microsoft/git`
  - `brew install --cask git-credential-manager-core`
and Log-in from browser
  
### Git Commands for version control
- `git clone https://github.com/<repo-name>.git` - To clone a repository
- `git checkout origin/master` - To set branch to master/main
- `git status` - To check the git status of the directory
- `git pull origin develop` - To pull all contents from `develop` branch
- `git log` - To get a history of the latest changes made in the repository
- `git checkout -b <new branch name>` - To create a new branch before starting to make changes. Branch names can begin with `feature/12345_new_model`/`patch/12345_add_item`/`bugfix/12345_fix_issue`
-- make code changes--
- `git status`
- `git add <filenames>` - Add modified files from the output of the previous `git status` command
- `git commit -m "comments"` - A meaningful message for the commit
- `git push origin -u <new branch name>:<remote branch name>` - Just `git push origin` is enough if you're pushing directly to master.
- `git push origin HEAD:<branch name>` - To directly push the changes to a branch.

Other git commands:
- `git fetch` - If some new branches are missing in local
- `git diff` 
- `git stash` - To delete all existing changes & start fresh 
- `git reset --merge`
- `git checkout -f origin/master`
- `git pull origin bug/12345-existing_error`
- `git config --global http.sslVerify true` - Step 1: in case of SSL certificate error
- `git config --global http.sslbackend schannel` - Step 2: in case of SSL certificate error


## Conda virtual environments
### To create a new virtual environment with conda

- `conda create -y -n "<env name>" python=3.9 pip=21.1` - To create virtual environment using Python 3.9 & a compatible pip version 
- `conda activate <env name>` - To activate the virtual environment
- `conda env list` - To list all available environments
- `conda env create -f conda.yml`
- `conda deactivate` - To deactivate a conda environment

To update an existing conda environment:
- `conda env update --file "./Dependencies/conda.yml" --prune`

If the organization is not allowed to create a conda env:

- `conda config --set ssl_verify no`
- `python -m pip install PACKAGENAME --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=files.pythonhosted.org` - This bypasses Firewall
- `pip freeze | grep PACKAGENAME` - To get the version of a specific package
- `pip freeze > requirements.txt` - To save all the package requirements in a virtual environment
- `pip show PACKAGENAME` - To get more details of a specific package

Pytesting:
- `python -m pytest --rootdir=./Tests --junitxml=./Tests/junit/unit-test.xml -vv -rP` - To test all tests from the folder
- `pytest -v tests/my-directory/test_demo.py::test_specific_function` - To test a specific function

Command to get all python packages used in a project:
- `pip install pipreqs`
- `pipreqs "<location where you want requirements to be saved>"`

To install from within a repository (if it has setup.py)
- `pip install - e .` (This installs the repo in 'editable' mode.

## PEP8 Checking in code
### Checking intendation of python script
First install Flake8 package (`pip install Flake8`)
- `flake8 <code path> --max-line-length=120`
or
- `python -m flake8 <code path> --max-line-length=120`


## Docker Commands
### Docker Commands for running a docker file

First open 'Docker CLI' for SSO authentication
- `docker login <host-name> -u <user name> -p <password>` - Enable logging in with SSO if connected to VPN/Remote Connect.
- `docker pull <image-name>` - A working sample command to pull a repository.
- `docker images` - List the available docker images.
- `docker build . -f dockerfile -t <image name>` - Build a docker image using the available dockerfile in the repository
- `docker build -t <image-name> -f dockerfile .` - This can also be used. Check & understand the difference before using it.
- `docker build -t  <another-image-name> -f dockerfile .`
- `docker tag <tag name> <ACR hostname/folder:latest` - To tag the image manually
- `docker push <host name/folder:latest>` - To push to container registries/remote locations.
- `docker run -it -e PYTHONUNBUFFERED=1 --publish 8080:8080 <image name>` - Run & publish the docker image
- `docker run -p 5000:5000 -v //home//project-location//://home//project-location// -d <image-name>`
- `docker run -p 4200:4200 -d <image-name>`
- `docker-compose -f db-docker-compose.yaml up` - If it's only to run a MSSQL database locally
- `
- `systemctl show --property ActiveState docker|cut -d"=" -f2` - To list active docker images


## Azure Commands
### Commands used to connect to Microsoft Azure Portal 
[Full list](https://github.com/ferhaty/azure-cli-cheatsheet)
For command-line:
- `az login` - Login with web
- `az login -u myemail@address.com` - Login in CLI
- `az account list` - List accounts
- `az account list-locations` - List all locations
- `az account get-access-token --output json --resource https://vault.azure.net`
- `az resource list` - List all my resource groups
- `azure --version` - Get what version of the CLI you have
- `az vm list` - List your VMs
- `azure help` - Get help
- `az account show -o jsonc` - Check if logged in or not
- `az account set --subscription <subscription-id>` - To set the currently active subscription for your Azure account
- `az aks get-credentials --resource-group <resource-group-name> --name <name-of-AKS-cluster> --admin` - To configure kubectl with the credentials and context required to connect to an Azure Kubernetes Service (AKS) cluster

## Kubernetes Commands
### Commands for interacting with Kubernetes clusters
[Full list](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- `kubectl get pods -n <name of the cluster>` - Used to retrieve information about resources in the cluster.
- `kubectl get pods -A -o wide > file-name.txt` - Used to get complete information about available pods and the tasks undertaken by them (stores it in a text file).
- `kubectl get nodes` - Used to get all available nodes.
- `kubectl describe pod -n <name of the cluster> <name of the pod>` - Gives detailed information from the yaml file used to configure the pod.
- `kubectl get hpa <name assigned to the HPA> --watch` - Gives real-time load info and pod count by HorizontalPodAutoscaler. [1](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/) [2](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- `kubectl logs <name of the pod> -n <name of the cluster>` - To get the logs of a pod
- `kubectl top pod <name of the pod> -n <name of the cluster>` - To retrieve usage statistics of a pod
- `kubectl apply -f manifest-file-name.yaml` - Apply changes made in the yaml file and recreate the pods based on it.
- `kubectl port-forward <resource-you-want-to-forward-a-port-to> 4200:4200 -n <name-space>` - For port-forwarding.
- `kubectl get secret` - List the secrets available
- `kubectl describe secret` - To get all details of the namespace including the token.
- `kubectl config get-contexts` - Used to display information about the available contexts in your Kubernetes configuration
- `kubectl get hpa -n <name-space>` - Used to retrieve information about Horizontal Pod Autoscalers (HPA) in a namespace
- `kubectl -n <name-space> patch hpa <name-of-the-hpa> --patch '{"spec":{"maxReplicas":2}}'` - To configure maximum replicas of a HPA.
- `kubectl patch secret <secret-name> -n <name-space> -p '<value>'` - To update regcred secrets inside a cluster.




## Linux Commands
### Commands used in Linux OS
- `sudo lsof -i -P -n | grep LISTEN`
- `kill -9 <container id>`

Curl Commands:
- `curl -i -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://127.0.0.1:8000/<page-url>/`

For Azure Portal:
Steps: 
1. Enable SSH
2. Install NVIDIA Drivers

- `ssh -L 1234:localhost:8888 avinash@<IP-Address>` - Port forwarding

Enabling SSH: 
- `ls .ssh`
- `ssh-copy-id -i ~/.ssh/id_rsa avinash@<IP-Address>`
- `ssh avinash@172.190.120.45`

Inside VM:
- `tmux kill-session -t 1`
- `tmux a -t 1`
- `tmux ls`
- `tmux`
- `sudo shutdown`
- `df -h`
- `htop`
- `ps`
- `ssh-copy-id -i ~/.ssh/mykey user@host`
Also refer [Tmux cheat-sheet](https://tmuxcheatsheet.com/) & [SSH Basics](https://www.ssh.com/academy/ssh/copy-id)

  
## Prefect Commands
### Prefect is an orchestration tool
[Prefect](https://www.prefect.io)
[Documentation](https://docs.prefect.io/2.11.3/)
- `prefect version`
- `prefect server start`
- `prefect deployment build prefect_tryouts.py:hello_world -n demo-deployment`
- `prefect deployment apply hello_world-deployment.yaml`
- `prefect agent start -q <work_queue_name>`
- `prefect cloud login`

## Other Tips
### Some ways to reduce efforts while developing code

To reduce the size of PDFs in PDF X-Change Editor:

Organize -> Resize -> Percentage -> [Reduce to a size which fit the requirement].
(Keep 'Context Scale Options' all check)

To beautify JSONs:     `Ctrl + Alt + L` (`Option + cmd + L` on Mac)

To select a URL fully: `Ctrl + W`

Extend Selection:

- In Mac: `Option + Up` or `Option + Down`

- In Windows: `Ctrl + W`

Get IP address of the Mac:
- `curl ifconfig.me`

To convert a string to base64 in Mac:
- `echo 'string' | base64 # To encode
- 'c3RyaW5nCg==' | base64 -D # To decode

---

These commands are written in such a way that helps **me** understand them. I might add more, or delete some, based on whatever is relevant to me. 

**Note:** I'll keep on updating these commands as I use them. 
