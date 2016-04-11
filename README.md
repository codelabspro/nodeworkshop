nodeworkshop
------------

- Partially inspired by https://github.com/kentcdodds/ng-workshop


- Install node using nvm as follows :

https://www.digitalocean.com/community/tutorials/how-to-install-node-js-with-nvm-node-version-manager-on-a-vps#installation

Installing Node.js on a VPS
The install process couldn't be easier. Once you're logged into your VPS, run this command:

curl https://raw.githubusercontent.com/creationix/nvm/v0.11.1/install.sh | bash
You'll see some output fly by, and then nvm will be installed. You will see a line that says:

=> Close and reopen your terminal to start using NVM

It's not actually necessary to log out, we just need to make sure that the changes nvm made to your path are actually reflected, so just do:

source ~/.profile
Alternatively, run the command suggested in the output of the script. Now type:

nvm ls-remote
Should you see the error, -bash: nvm: command not found it may be because git is not installed.

Go ahead and install git and rerun the script:

apt-get install git
And you will be shown a list of all the available versions of node.js. You can always find out the latest stable release by heading to the node.js website, where it's printed in the center of the page.

To install version 0.10.13 (the latest as of this writing) type:

nvm install 0.10.13
If you type:

node --version
You will now see that node v0.10.13 is installed and active. If you had an older node app that only works with node v0.8.16, and wanted to downgrade, then you would input:

nvm install v0.8.16
to install and switch to v0.8.16.

When you're done and want to switch back to v0.10.13, you can do so with nvm's use command:

nvm use v0.10.13
Nvm is great and makes switching between node versions easy and convenient. However, there's one caveat. If you type:

which node you will see something interesting. Nvm installs node.js inside your user's home directory. This is fine for development, but if you want to actually host node applications, you don't want to install the latest new version of node via nvm and discover that you've inadvertently caused your production node app (which can be incompatible with the latest node.js) to stop working. It's best to install one copy of node globally so that other users can access it, and use nvm to switch between your development versions.

To do this, run the following command (entering your user's password at the prompt):

n=$(which node);n=${n%/bin/node}; chmod -R 755 $n/bin/*; sudo cp -r $n/{bin,lib,share} /usr/local


The above command is a bit complicated, but all it's doing is copying whatever version of node you have active via nvm into the /usr/local/ directory (where user installed global files should live on a linux VPS) and setting the permissions so that all users can access them.

If you ever want to change the version of node that's installed system wide, just do another nvm use vXX.XX.XX to switch your user's node to the version you want, and then re-run the above command to copy it to the system directory.
To check that it works, become the root user and do another which command to make sure that node is now installed to /usr/local/bin:

sudo -s
which node
You should see:

/usr/local/bin/node
Congrats! Node.js is now installed and ready for use. Enjoy!





