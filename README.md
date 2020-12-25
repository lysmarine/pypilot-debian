#rtimulib2
# Download pypilot
Download
```
wget https://github.com/seandepagnier/RTIMULib2/archive/master.zip
unzip master.zip
cp -r RTIMULib2-master/* rtimulib2/
rm master.zip
```

Build
```
cd rtimulib2
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
`

```

# pypilot-debian
Scripts for making pypilot a debian package.
The selected packaging tool is **dh_make** and the packaging approach is **native debian package**

### Build prerequisites 
```
sudo apt-get install devscripts python-virtualenv equivs python-dev git-buildpackage dh-virtualenv \
dh-make dh-python python3-all wget unzip git

```

### Get the source code
Before building the package we must get the genuine pypilot source code (aka upstream) and compress it with debian naming scheme

```
# Download pypilot 
wget https://github.com/pypilot/pypilot/archive/master.zip
unzip master.zip
rm master.zip

# Download pypilot_data
wget https://github.com/pypilot/pypilot_data/archive/master.zip
unzip master.zip
rm master.zip

# Create the source package 
cp -r pypilot-master/* ./pypilot
cp -r pypilot_data-master/* ./pypilot

```

###### Build and sign source package
```
cd pypilot
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
 