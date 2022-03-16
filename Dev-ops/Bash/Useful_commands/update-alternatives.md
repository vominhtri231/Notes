# update-alternatives

The command for maintaining symbolic link 

## Create symlink

```sh
# Binary with higher priority is used first
sudo update-alternatives --install <path-of-symlink> <command-name> <path-to-binary> <priority>

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 6
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 
```

## Delete symlink

```sh
sudo update-alternatives --remove <command-name> <path-to-binary>

sudo update-alternatives --remove java /opt/java/jdk1.8.0_102/bin/java
```
