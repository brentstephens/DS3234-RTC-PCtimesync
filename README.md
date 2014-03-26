DS3234-RTC-PCtimesync
=====================

Arduino code to set the time on a DS3234 RTC to your PC's clock.

The idea is to first use the <Time.h> library to read the current time from your computer. This translates cumbersome unix time into something more manageable (i.e., hours, mins, secs, month, day, year). Then we will want to use the <DS3234.h> library, which handles h,m,s,m,d,y formats, to set the RTC time to the computer time.

The way the program works now is by waiting for a signal to the serial port from you computer. As it is waiting, you have to manually open terminal (mac) and send your unix time to the waiting program. You send the following message from terminal while waiting:

	sudo echo "T$(($(date +%s)+60*60*-5))" >/dev/tty.usbmodem1421

where "-5" is the time zone adjustment from GMT (-5 yields CDT)
and tty.usbmodem1421 is your serial port (labeled exactly as in the Arduino IDE)

Needs:
1. We still need to use the RTC.setDateTime function to set to the h,m,s... format captured from the Time functions.
2. We then need to explore ways to automatically send the system's unix time to the awaiting terminal to automate the process.