# telnetlogger

This is a simple program to log login attempts on Telnet (port 23).

It's designed to track the Mirai botnet. Right now (Nov 4, 2016) infected Mirai
machines from around the world are trying to connect to Telnet on every IP address REALLY
OFTEN. This program logs both which IP addresses are doing the attempts, and which
passwords they are using.

I wrote it primarily because installing `telnetd` on a Raspberry Pi wasn't sufficient.
For some reason, the Mirai botnet doesn't like the output from Telnet, and won't try
to login. So I needed something that produced the type of Telnet is was expecting. While
I was at it, I also wrote some code to parse things and extract the usernames/passwords.

# Usage

Just run the program in order to see passwords and IP addresses appear on stdout.

    telnetlogger
  
To log the information to a log file, use the `-o` option.

    telnetlogger -o output.csv
  
To listen on another port (for testing and whatnot), use `-l`.

    telnetlogger -l 2323

Note that on many systems, you'll get an "access denied" error message, because programs
that open ports below 1024 need extra privileges. So you may need to `sudo` the program.

# Compiling

Type `make` or:

    gcc telnetlogger.c -o telnetlogger -lpthread

It'll also compile/run on Windows.

# Output

The program prints a single line in CSV format:
1478281930, 220.134.232.209,'root','dreambox'

This represents the UNIX-time when the login was attempted, the source IP address, and the quoted
form of the attempted username and password.
    


  
