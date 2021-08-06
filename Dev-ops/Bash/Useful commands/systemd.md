# Systemd

Systemd is an init system and system manager, becoming new standard for linux distributions. This is used for initialize components that must be started when kernal is booted and manage services.

## Service manager

```sh
systemctl start service-name

systemctl stop service-name

systemctl restart service-name

systemctl reload service-name # Reload the configurations

sytemctl enable service-name # Start service automatically at startup

systemctl disable service-name

systemctl status service-name # show service status
```

## System state overview

```sh
systemctl list-units # display all active units

systemctl list-units # display all units

systemctl list-units --all --state=inactive

systemctl list-units --type=service

systemctl list-dependencies service-name # display service dependencies
```
