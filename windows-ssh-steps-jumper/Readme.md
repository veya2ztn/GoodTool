This private 'ssh' file come from [@manojampalam](https://github.com/manojampalam) at <https://github.com/PowerShell/Win32-OpenSSH/issues/1172>

-------

### How to jump multiply jumper at one time

####requirement: 

- Linux: ssh client need support `ProxyJump` (openssh 7.5 or later)
- The `ssh.exe` file in this repo. [replace the ordinary `ssh.exe` at `C:\Windows\System32\OpenSSH` ]

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

Ref:

1. https://zhuanlan.zhihu.com/p/55016458

-------------

So far, you can `ssh` server very quick. But unlucky, we can not set {'host': jumper3} in Atom's json config. Somehow, it cannot use Proxy Commend.

In order to use it at Atom, you need do one more step. The **Port Forward** !

```
ssh -NfL 8900:localhost:22 -J jumper1,jumper2 jumper3
```

Now you can set 

```json
{
	'host':localhost,
	'port':8900,
	'user':user.name,
	"privatekey": "C:\\Users\\user\\.ssh\\id_rsa",
}
```

Ref:

1. https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts#Port_Forwarding_Through_One_or_More_Intermediate_Hosts



