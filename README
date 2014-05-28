#!/bin/bash

##################################################
##    http://github.com/dlnetworks/scripflip    ##
##################################################
## aggravates rippers by changing the title as  ##
## many rippers write new files on title change ##
##################################################



#########################
## start configuration ##
#########################

## DNAS version (1 or 2)
scv="2"

## stream id (DNAS V2 only)
sid="1"

## DNAS password
passwd="dnas-admin-pass"

## hostname or ip address
host="stream.domain.com"

## enter port (if you dont have a port use port="80"
port="8000"

## what to change the title to
title="station name or promo text or any text"

## seconds to wait before changing back
waittime="1"

## seconds to sleep before repeating
sleeptime="30"

##############################################
## end configuration # do not edit the rest ##
##############################################



sc1url="http://$host:$port"
sc2url="http://$host:$port"
tmptitle="$(echo "$title" | sed 's/ /%20/g')";

while true
	do
		if [ "$scv" = "1" ]
			then
				sc1current="$(curl -s -A "$agent" "$sc1url"/7.html | cut -d',' -f 7- | cut -d'<' -f -1)";
				sc1string="$(echo "$sc1current" | sed 's/ /%20/g')";
				curl -s -A 'Mozilla/sc-ripflip' "$sc1url/admin.cgi?mode=updinfo&song=$tmptitle&pass=$passwd";
				echo "Title set to: $title"
				sleep "$waittime"
				curl -s -A 'Mozilla/sc-ripflip' "$sc1url/admin.cgi?mode=updinfo&song=$sc1string&pass=$passwd";
				echo "Title returned to: $sc1current"
			else
				sc2current="$(curl -s -A "$agent" "$sc2url"/currentsong?sid=$sid | cut -d',' -f 7- | cut -d'<' -f -1)";
				sc2string="$(echo "$sc2current" | sed 's/ /%20/g')";
				curl -s -A 'Mozilla/sc-ripflip' "$sc2url/admin.cgi?sid=$sid&mode=updinfo&song=$tmptitle&pass=$passwd";
				echo "Title set to: $title"
				sleep "$waittime"
				curl -s -A 'Mozilla/sc-ripflip' "$sc1url/admin.cgi?sid=$sid&mode=updinfo&song=$sc2string&pass=$passwd";
				echo "Title returned to: $sc2current"
		fi
	sleep "$sleeptime"
done
