# Save over HTTP — A Civ4 Pitboss helper script for fast logins

If this script is running on the client side it can significant speed
up the login in Civ4:BTS Pitboss games. Th

## Dependecies & Setup:
1. Install fuse for Python
```
	sudo apt-get install pip
	sudo pip install fusepy
```

2. Remap your z:-Drive of wine
  Create a folder e.g. '~/.wine/PBdrive',
  call 'winecfg' and connect drive 'z:' with the new folder.

	Note that you cann not use an other drive letter but 'z:'!

3. Create a mount point for the downloaded files, e.g.
		'~/.wine/PBdownloads'

## Usage:
```
  python ./pb_downloader.py "~/.wine/PBdownloads" "~/.wine/PBdrive"
```

## Note for PB hosts
In the default configuration, it just speeds up logins on pb.zulan.net.
Extend the included list of URLs if you host your own games.

Moreover, you had to prepare the Pitboss host to serve the games
over HTTP(s) and with the correct directory structure:

### Directory setup
Assume the ALTROOT argument of your PB is set on
*ALTROOT="/home/USERNAME/PBs/PB1"*

1. Change the path by adding the folder '_http_[your server ip or domain]'
*ALTROOT="/home/USERNAME/_http_[your server ip/domain]/PBs/PB1"*

2. This path will be translated by Wine into…
*Z:\home\USERNAME\_http_[your server ip/domain]\PBs\PB1*

… and the Civ4:BTS client will try to load following file during the login:
*Z:\home\USERNAME\_http_[your server ip/domain]\PBs\PB1\Saves\pitboss\auto\Recovery_{NICKNAME}.CivBeyondSwordSave*

3. Because we encoded the server IP into the path we could exploit this file
lookup into a download (done by this script or similar programs).
On the server side we need to fulfill the given pattern: Create 
*[your www root dir]/PBs/PB1/Saves/pitboss* and place a symbolic link on above 'auto' folder.


