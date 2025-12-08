## AppArmor

Ubuntu 24.04 and onwards [Ubuntu restricts the creation of unprivilaged user namespaces](https://ubuntu.com/blog/ubuntu-23-10-restricted-unprivileged-user-namespaces) by default via [AppArmor](https://documentation.ubuntu.com/server/how-to/security/apparmor/).
Creation of unrestricted user namespaces is fundemental to the sandboxing tool, [nsjail](https://github.com/google/nsjail), that Code Executor uses to execute user code in isolation. As such we have provided an AppArmor profile that selectively gives the required permissions to the nsjail binary that is run in Code Executor.

To enable the profile on host machine:

1) Install AppArmor profiles:

```
sudo apt install apparmor-profiles
```

2) Copy the provided `usr.bin.nsjail` AppArmor profile to `/etc/apparmor.d/usr.bin.nsjail`


3) Load the profile:

```
sudo apparmor_parser /etc/apparmor.d/usr.bin.nsjail
```

