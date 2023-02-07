Masscan and Nmap Commands
=========================

A collection of Masscan and Nmap commands for various tasks.

Masscan
-------

### Scan for all vulnerable printers on the Internet

cssCopy code

`masscan 0.0.0.0/0 -p9100,515,631 --banners --rate=10000 --open --exclude-file exclude-ips.txt -oG results.txt`

This command scans the entire Internet (IP range from 0.0.0.0 to 255.255.255.255) for ports 9100, 515, and 631, which are commonly used by printers. It retrieves banner information from the open ports and scans at a rate of 10,000 packets per second. The scan only shows open (filtered) ports and excludes the IP addresses specified in the text file "exclude-ips.txt". The results are saved in a file in "grepable" format with a filename of "results.txt".

### Scan for all open passwordless FTP ports

cssCopy code

`masscan 0.0.0.0/0 -p21 --banners --rate=10000 --open --exclude-file exclude-ips.txt -oG results.txt`

This command scans the entire Internet for port 21, which is commonly used by the FTP protocol. It retrieves banner information from the open ports and scans at a rate of 10,000 packets per second. The scan only shows open (filtered) ports and excludes the IP addresses specified in the text file "exclude-ips.txt". The results are saved in a file in "grepable" format with a filename of "results.txt".

Nmap
----

### Scan for all open passwordless SSH ports

cssCopy code

`nmap -iL results.txt -p 22 --script=auth --script-args='userdb=nmap-users.lst,passdb=nmap-passes.lst' -oN output.txt`

This command scans the list of IP addresses specified in the file "results.txt" for port 22, which is commonly used by the SSH protocol. It probes the open ports to determine the version and type of service running and runs the "auth" script to test for authentication-related vulnerabilities. The user and password databases used by the "auth" script are specified with the `--script-args` option. The results are saved in normal format to the file "output.txt".

### Scan for all open passwordless FTP ports

cssCopy code

`nmap -iL results.txt -p 21 --script=auth --script-args='userdb=nmap-users.lst,passdb=nmap-passes.lst' -oN output.txt`

This command scans the list of IP addresses specified in the file "results.txt" for port 21, which is commonly used by the FTP protocol. It probes the open ports to determine the version and type of service running and runs the "auth" script to test for authentication-related vulnerabilities. The user and password databases used by the "auth" script are specified with the `--script-args` option. The results are saved in normal format to the file "output.txt".

### Fingerprint a list of IP addresses

pythonCopy code

`nmap -iL results.txt -sS -Pn -T4 --version-all -`
