# pypilot-debian
Scripts for making pypilot a debian package.
The selected packaging tool is **dh_make** and the packaging approach is **debianization of upstream project**

### Build prerequisites 
```
sudo apt-get install devscripts python-virtualenv equivs python-dev git-buildpackage dh-virtualenv \
dh-make dh-python python3-all wget unzip git

```

### Get the source code
Before building the package we must get the genuine pypilot source code (aka upstream) and compress it with debian naming scheme

```
cd pypilot-0.0.0-0/

wget https://github.com/pypilot/pypilot/archive/master.zip
unzip master.zip

cd pypilot-master/ 
    git clone --depth 1 https://github.com/pypilot/pypilot_data
cd ../

mv pypilot-master ../pypilot-0.0.0-0.orig
cp -r ../pypilot-0.0.0-0.orig/* ./

rm -rf master.zip pypilot-0.0.0-0.orig
```

###### Build and sign source package
```
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
```

Content of the debian package files: 
 - changelog - Contains a log of the changes made to the Debian package.
 - compat - Specifies the compatibility level for debhelper tool
 - control - Describes the source and binary package giving information about them
 - install - Copies package specific configurations
 - postinst - A script to execute after package installation has happened
 - rules - A makefile for the package
 