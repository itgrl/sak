# sak

## Deprecated
I will keep this script here since it is very useful especially for audits where we also need to download information from the runs, but I will probably not continue development on it.

Since the creation of this script, another tool has taken it's place with greater functionality.

Checkout Puppet Bolt 
https://puppet.com/docs/bolt/latest/bolt.html


## About
Swiss Army Knife type of script to aid in day to day administration.  This script allows for copying a file to a system or list of systems, executing a command against a system or list of systems, and copying a file from a system or list of systems.  All three operations can be done in a single execution of this script to allow for copying a script for auditing to a system, executing it, and retrieval of a results file.

## Help Message
sak is a universal tool to aid in day to day adhoc tasks across 1 or more servers.

Usage:

  Multi-server:
  
      sak -f=filename.txt -c="cat /etc/motd" -l=server.list
      
  Single-server:
  
    sak -f=scriptname.txt -c="sudo cp scriptname.txt /root/bin/scriptname.sh" <ip or fqdn>
    
    
Options:

  -h or --help          Print this message.
  
  -c or --command       Command to execute on target server(s).
  
  -f or --file          Specify file to place on target server(s), in your homedir.
  
  -r or --retrieve      Retrieve a file from the target server(s).  (Specify full path).
  
  -l or --list          Server list to execute commands against.

  -t or --timeout       Expect time to wait between commands.  

  -p or --newpass       Indicate this is to change password of user logging in.


### Server List
When supplying a server list, supply one server on each line.  The list can contain IP address, or FQDNs.  If using the hostname only, or shortname, then please be sure each entry on the list is resolvable in DNS from where you are executing the script.

### Order of operation
sak executes the file copy to server, followed by the execution of the supplied command, and then the retrieval of a file from server.  Each server in the list performs all commands specified before moving to the next server in the list.  

### Copied files destinations
Files copied to destination servers are stored in the supplied user's home directory.

Files copied from target servers are stored in the current working directory in a directory for each server in the list.  
The script will make a directory for each target server in the current working directory.

### Credentials
The connect as credentials will be prompted for by the script and stored in a variable for reuse through the runtime of the script.

### Timeout
This sets the timeout that expect waits between commands.  If not set, it uses the expect defaults.  Useful if you are noticing the script move to the next action before completing the previous.

### Installation
This is a basic expect script and will require expect to be installed on the system where you execute the scripts.  Simply copy the sak script or clone the repository via git to the location you wish to execute the script from.  i.e. /root/bin/  ~/bin/ etc


