
Debian
====================
This directory contains files used to package hellard/hellar-qt
for Debian-based Linux systems. If you compile hellard/hellar-qt yourself, there are some useful files here.

## hellar: URI support ##


hellar-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install hellar-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your hellar-qt binary to `/usr/bin`
and the `../../share/pixmaps/hellar128.png` to `/usr/share/pixmaps`

hellar-qt.protocol (KDE)

