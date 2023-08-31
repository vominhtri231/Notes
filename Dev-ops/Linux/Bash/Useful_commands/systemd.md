# Systemd

Systemd is an init system and system manager, becoming new standard for linux distributions. This is used for initialize components that must be started when kernal is booted and manage services.

## Service manager

```sh
systemctl start service-name

systemctl stop service-name

systemctl restart service-name

systemctl reload service-name # Reload the configurations

systemctl enable service-name # Start service automatically at startup

systemctl disable service-name

systemctl status service-name # show service status

systemctl list-dependencies service-name # display service dependencies
```

## How to create a service unit

Create a `.service` file inside `/etc/systemd/system`, etc `/etc/systemd/system/foo.service`.

A service unit file including:

1. Unit: Specify the description, the starting order, dependencies (weak and hard ones), etc.
2. Service: Specify the command to execute when start/stop/reload the service, service's type, service's environment variables, etc.
3. Install: Specify which service is depending on it, alias, etc.

```
[Unit]
Description=Foo

[Service]
ExecStart=/usr/sbin/foo-daemon
```

Reload the systemd to load the file, using:

```sh
sudo systemctl daemon-reload
```


## Services overview

```sh
systemctl list-units # display all active units

systemctl list-units # display all units

systemctl list-units --all --state=inactive

systemctl list-units --type=service
```
