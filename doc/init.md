Sample init scripts and service configuration for hellard
==========================================================

Sample scripts and configuration files for systemd, Upstart and OpenRC
can be found in the contrib/init folder.

    contrib/init/hellard.service:    systemd service unit configuration
    contrib/init/hellard.openrc:     OpenRC compatible SysV style init script
    contrib/init/hellard.openrcconf: OpenRC conf.d file
    contrib/init/hellard.conf:       Upstart service configuration file
    contrib/init/hellard.init:       CentOS compatible SysV style init script

1. Service User
---------------------------------

All three Linux startup configurations assume the existence of a "hellarcore" user
and group.  They must be created before attempting to use these scripts.
The OS X configuration assumes hellard will be set up for the current user.

2. Configuration
---------------------------------

At a bare minimum, hellard requires that the rpcpassword setting be set
when running as a daemon.  If the configuration file does not exist or this
setting is not set, hellard will shutdown promptly after startup.

This password does not have to be remembered or typed as it is mostly used
as a fixed token that hellard and client programs read from the configuration
file, however it is recommended that a strong and secure password be used
as this password is security critical to securing the wallet should the
wallet be enabled.

If hellard is run with the "-server" flag (set by default), and no rpcpassword is set,
it will use a special cookie file for authentication. The cookie is generated with random
content when the daemon starts, and deleted when it exits. Read access to this file
controls who can access it through RPC.

By default the cookie is stored in the data directory, but it's location can be overridden
with the option '-rpccookiefile'.

This allows for running hellard without having to do any manual configuration.

`conf`, `pid`, and `wallet` accept relative paths which are interpreted as
relative to the data directory. `wallet` *only* supports relative paths.

For an example configuration file that describes the configuration settings,
see `contrib/debian/examples/hellar.conf`.

3. Paths
---------------------------------

3a) Linux

All three configurations assume several paths that might need to be adjusted.

Binary:              `/usr/bin/hellard`  
Configuration file:  `/etc/hellarcore/hellar.conf`  
Data directory:      `/var/lib/hellard`  
PID file:            `/var/run/hellard/hellard.pid` (OpenRC and Upstart) or `/var/lib/hellard/hellard.pid` (systemd)  
Lock file:           `/var/lock/subsys/hellard` (CentOS)  

The configuration file, PID directory (if applicable) and data directory
should all be owned by the hellarcore user and group.  It is advised for security
reasons to make the configuration file and data directory only readable by the
hellarcore user and group.  Access to hellar-cli and other hellard rpc clients
can then be controlled by group membership.

3b) Mac OS X

Binary:              `/usr/local/bin/hellard`  
Configuration file:  `~/Library/Application Support/HellarCore/hellar.conf`  
Data directory:      `~/Library/Application Support/HellarCore`
Lock file:           `~/Library/Application Support/HellarCore/.lock`

4. Installing Service Configuration
-----------------------------------

4a) systemd

Installing this .service file consists of just copying it to
/usr/lib/systemd/system directory, followed by the command
`systemctl daemon-reload` in order to update running systemd configuration.

To test, run `systemctl start hellard` and to enable for system startup run
`systemctl enable hellard`

4b) OpenRC

Rename hellard.openrc to hellard and drop it in /etc/init.d.  Double
check ownership and permissions and make it executable.  Test it with
`/etc/init.d/hellard start` and configure it to run on startup with
`rc-update add hellard`

4c) Upstart (for Debian/Ubuntu based distributions)

Drop hellard.conf in /etc/init.  Test by running `service hellard start`
it will automatically start on reboot.

NOTE: This script is incompatible with CentOS 5 and Amazon Linux 2014 as they
use old versions of Upstart and do not supply the start-stop-daemon utility.

4d) CentOS

Copy hellard.init to /etc/init.d/hellard. Test by running `service hellard start`.

Using this script, you can adjust the path and flags to the hellard program by
setting the HELLARD and FLAGS environment variables in the file
/etc/sysconfig/hellard. You can also use the DAEMONOPTS environment variable here.

4e) Mac OS X

Copy org.hellar.hellard.plist into ~/Library/LaunchAgents. Load the launch agent by
running `launchctl load ~/Library/LaunchAgents/org.hellar.hellard.plist`.

This Launch Agent will cause hellard to start whenever the user logs in.

NOTE: This approach is intended for those wanting to run hellard as the current user.
You will need to modify org.hellar.hellard.plist if you intend to use it as a
Launch Daemon with a dedicated hellarcore user.

5. Auto-respawn
-----------------------------------

Auto respawning is currently only configured for Upstart and systemd.
Reasonable defaults have been chosen but YMMV.
