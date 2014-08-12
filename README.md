lnpm.sh
=======
An npm for local storage use and managment

This script solves the problem of having node_modules installed in every directory in which you have a node project. It allows node modules to be read from a centralized directory on the file system and when a particular package does not exist it will download the package to the centralized directory for continued use. No more downloading packages every time you start a new node project and no longer do node packages have to be spread out all over your hard drive. Every version of a package in use conveniently stored in one place.

BEFORE USING lnpm.sh YOU MUST CHANGE THE nd VARIABLE LINE 6 OF THE SCRIPT TO POINT TO THE FULL PATH OF THE DIRECTORY YOU WILL USE TO STORE THE NODE PACKAGES

After that is done, the easiest way to get started is to copy and existing node_modules directory from one of your existing projects to where you want your centralized location. Then run lnpm configure. This will change all the directory names to <packagename>---<version>. This makes the packages usable with lnpm and your ready to go. You could simply create an empty directory and assign it to nd, but this way will save you some downloading which is one of the main reasons to use this script. You can easily add other packages to the nd directory at anytime and run lnpm configure again to setup the new directories.

lnpm.sh install <package name>
Searches the local directory for the package and if it exist it will do the following as needed:
If no package.json exists, it will run npm.init to interactively create it.
If no dependencies object exists, it will add it to the package.json.
If no reference to the package exists in the dependencies object, it will be added.
If the package does not exist in the local directory, it will be download and assimilated into the local directory and the previous steps will then be carried out.
Note that if there is more that one version of a package in the local directory, you will be prompted for the one to install.

lnpm.sh install <package_name> -dev
Performs all the tasks of regular install but also will perform the same steps to add as a dev dependency
If both dependencies and devDependencies have a reference to the package in package.json it will exit with a package is already installed notification.

lnpm.sh configure
Makes an existing node_modules directory compatible with lnpm.sh by renaming the directories to include versions

lnpm.sh update <package_name>
Without a package name this will add the latest version of all packages not already stored in the local folder. If a package name is provided only that package will be affected.

lnpm.sh revert
Reverts the lmpm modules directory directories to standard node names. Since lnpm allows the centralized storage of multiple package versions by adding the version to the directory name, directories that are part of a multi-version package will remain unaltered. You will need to choose a version and rename the directory manually

lnpm.sh deploy
Need to implement for copying modules used by project to the project directory, changing directory names back to just the package name and modifying package.json to have the modified path. So the application can be deployed off the local system.