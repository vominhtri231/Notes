# Configuration files

- `/etc/environment`: The system-wide configuration file, own by root and applied to every users. This should not be modified.
- `~/.profile`: the user initialization script, own by each user.
- `/etc/profile` and `/etc/profile.d`: `/etc/profile` is the global initialization script, applied before user specific script. This script also call every scripts inside `/etc/profile.d`.