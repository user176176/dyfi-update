# Current modifications
SSL support taken from fluks: https://github.com/fluks/dyfi-update-ssl-pl

Systemd support added meaning that you can just install with make and then run:

- systemctl start dyfi-update.service
- systemctl restart dyfi-update.service
- systemctl stop dyfi-update.service
- systemctl status dyfi-update.service

Currently needs to run with sudo.

# TODO:
- Systemd Could be changed like https://askubuntu.com/questions/676007/how-do-i-make-my-systemd-service-run-via-specific-user-and-start-on-boot

# dyfi-update
dyfi-update.pl 1.2.0
by dy.fi admins, admin at dy dot fi

A perl client for updating dy.fi hostnames automatically

Only requires perl 5.002 with Socket and strict modules,
HTTP and base64 code has been embedded.

## RUNNING:
	
dyfi-update.pl -f <configfile>     (recommended)

OR:

dyfi-update.pl -u <username> -p <password> -i <pidfile> [-l <logfile>]
    [-d] hostname1.dy.fi hostname2.dy.fi ...


If no logfile is specified, log messages are printed on standard output.
Specify the -d option to produce a very verbose debugging log which
describes every action taken. 

dyfi-update.pl is a daemon. You do not need to run it periodically
from cron - just run it in the background and it will do the job.

dyfi-update.pl does not need root privileges run. Of course you need
to be able to write to the log & pid files, and read the config file.
The pid file is a mandatory option - the file is used to make sure that
no more than one copy of the script is run by accident. It is also
used by the /etc/init.d/dyfi-update script to stop the client.


## INSTALLATION:

To install the client, run 'make install'. This will install the
client script in /usr/local/bin. If a configuration file does not
exist in /usr/local/etc/dyfi-update.conf, it will install a sample
file there. It will also install a systemd script in /etc/systemd/system/.

Next, edit /usr/local/etc/dyfi-update.conf to put your dy.fi config
in there.

Then, try to run trough systemd: "systemctl start dyfi-update"
If there are any problems in the configuration, it should barf on the
console, or the log file you have configured (by default,
/var/log/dyfi-update.log). You can also stop the client using
"systemctl stop dyfi-update.service".

Do not put dyfi-update.pl in cron. It is a daemon.

If you want dyfi-update.pl to automatically start up when the
machine is booting, figure out the runlevels you want it to run at.
Run 'make installboot3' to make it start up at runlevel 3,
'make installboot5' for runlevel 5, etc. You can find out the
default booting runlevel using the command
'grep initdefault /etc/inittab' - you should get a line like
'id:5:initdefault:' where 5 is the default runlevel.


## UNINSTALLING:

  Run 'make uninstall'. This will clear the files installed by the
above commands from the default locations - including the
configuration file!

Have fun!

