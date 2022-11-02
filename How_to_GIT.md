```
 ██████╗ ██╗████████╗██╗  ██╗██╗   ██╗██████╗ 
██╔════╝ ██║╚══██╔══╝██║  ██║██║   ██║██╔══██╗
██║  ███╗██║   ██║   ███████║██║   ██║██████╔╝
██║   ██║██║   ██║   ██╔══██║██║   ██║██╔══██╗
╚██████╔╝██║   ██║   ██║  ██║╚██████╔╝██████╔╝
 ╚═════╝ ╚═╝   ╚═╝   ╚═╝  ╚═╝ ╚═════╝ ╚═════╝ 

Files that you add to a repository via a browser are limited to 25 MB per file. You can add larger files, up to 100 MB each, but you need to use CLI for this. Follow these steps:

╦┌┐┌┌─┐┌┬┐┌─┐┬  ┬  ┌─┐┌┬┐┬┌─┐┌┐┌
║│││└─┐ │ ├─┤│  │  ├─┤ │ ││ ││││
╩┘└┘└─┘ ┴ ┴ ┴┴─┘┴─┘┴ ┴ ┴ ┴└─┘┘└┘

To install github CLI

$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key C99B11DEB97541F0
$ sudo apt-add-repository https://cli.github.com/packages
$ sudo apt update
$ sudo apt install gh

╦ ╦┌─┐┬ ┬  ╔╦╗┌─┐  ╦ ╦┌─┐┌─┐
╠═╣│ ││││   ║ │ │  ║ ║└─┐├┤ 
╩ ╩└─┘└┴┘   ╩ └─┘  ╚═╝└─┘└─┘

To login
$ gh auth login

To clone repo
$ mkdir ~/repos
$ cd ~/repos
$ gh repo clone https://github.com/PATH/TO/REPO

To upload files to repo:
Place the file on your local repor and then execute the following commands
$ cd ~/repos/YOUR-LOCAL-REPO
$ git add .
$ git commit -m "COMMENT FOR COMMIT"
$ git push origin NAME-OF-BRANCH

╔╗ ┬┌─┐┌─┐┌─┐┬─┐  ╔═╗┬┬  ┌─┐┌─┐
╠╩╗││ ┬│ ┬├┤ ├┬┘  ╠╣ ││  ├┤ └─┐
╚═╝┴└─┘└─┘└─┘┴└─  ╚  ┴┴─┘└─┘└─┘

For files bigger than 100 MB, you need to install Git LFS

Installation steps:
- Install GitLFS (link: https://git-lfs.github.com/)
$ git lfs install
$ git add .gitattributes

To Push:
$ git lfs track “.fileextension”
$ git commit -m "commit msg"
$ git push origin

If you get an error that you still can not upload files larger than 100MB:
$ git lfs migrate import --include="*.fileextension"

To Pull:
$ git lfs pull (to pull actual file instead of a pointer to the large file)
Source: https://sabicalija.github.io/git-lfs-intro/

```