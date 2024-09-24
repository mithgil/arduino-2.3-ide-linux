# arduino-2.3-ide-linux
How to install and use arduino-2.3-ide on Linux
---


Download an move arduino 2.3 IDE to /opt. after opening it with

```bash
/opt/arduino-2.3.2$ ./arduino-ide 
[10887:0924/142312.246531:FATAL:setuid_sandbox_host.cc(158)] The SUID sandbox helper binary was found, but is not configured correctly. Rather than run without sandboxing I'm aborting now. You need to make sure that /opt/arduino-2.3.2/chrome-sandbox is owned by root and has mode 4755.
Trace/breakpoint trap (core dumped)
```

why?

The error you're encountering is related to the SUID sandbox in the Arduino IDE, which is a security mechanism used by Chromium-based applications to provide an additional layer of protection. The error indicates that the chrome-sandbox binary in the Arduino IDE installation is not correctly set up with the necessary permissions.

To fix this issue, you need to change the ownership and permissions of the chrome-sandbox binary. You can do this by running the following commands in your terminal:

```bash
sudo chown root:root /opt/arduino-2.3.2/chrome-sandbox
sudo chmod 4755 /opt/arduino-2.3.2/chrome-sandbox
```

Explanation:
`sudo chown root:root /opt/arduino-2.3.2/chrome-sandbox`: This command sets the owner and group of the chrome-sandbox binary to root.
`sudo chmod 4755 /opt/arduino-2.3.2/chrome-sandbox`: This command sets the permissions of the chrome-sandbox binary to 4755, which means:
`4` (Set-User-ID): When the binary is executed, it runs with the privileges of the file owner (root in this case).
`7` (Read, Write, Execute): The owner (root) has read, write, and execute permissions.
`5` (Read, Execute): The group and others have read and execute permissions.
After running these commands, try launching the Arduino IDE again with:

```bash
./arduino-ide
```
This should resolve the error and allow the IDE to start correctly.


