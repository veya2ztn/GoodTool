This private 'ssh' file come from [@manojampalam](https://github.com/manojampalam) at <https://github.com/PowerShell/Win32-OpenSSH/issues/1172>

-------

### How to jump multiply jumper at one time

####requirement: 

- Linux: ssh client need support `ProxyJump` (openssh 7.5 or later)
- The `ssh.exe` file in this repo.

1. Edit/create ssh config file at `~/.ssh/config` or `C:\Users\user\.ssh` like

   ```
   Host jumper1
       User          user.name
       Port          22(default)
       HostName      host.ip
   
   Host jumper2
       User          user.name
       Hostname      host.ip
       ProxyJump     jumper1
   
   Host jumper3
       User          user.name
       Hostname      host.ip
       ProxyJump     jumper2
   ```

2. test via 

   ```
   ssh jumper1
   ssh jumper2
   ssh jumper3 
   ```

3. use rsa-key connection if you want.

