# Getting started!

## Setting up the Beaglebone Black

 1. Download Debian 9.5 2018-10-07 (or attempt a later version) from the [BeagleBoard.org Latest Firmware Images](https://beagleboard.org/latest-images) site.

 2. Create a SD card for this image
 
    Instructions for Mac OS X:
     1. Unmount whatever you already have mounted on that disk.
        ```
        $ diskutil unmountDisk /dev/disk2 # Substitute disk2 with whatever disk your SD card is.
        ```
 
     2. Flash the disk using the img file you downloaded above with a block size of 4096 so it doesn't take ages.
        ```
        $ sudo dd if=bone-debian-9.5-iot-armhf-2018-10-07-4gb.img of=/dev/disk2 bs=4096
        ```
        Hint: you can use `ctrl-t` to see progress during a dd command!
 
 
 3. Boot the Beaglebone Black with the microSD card in and USB Connected. Hopefully you should get a network device attached to your computer with the ip 192.168.6.1.
 
 4. SSH into the Beaglebone with default user `debian` and password `temppwd`.
    ```
    $ ssh debian@192.168.6.2
    ```
 
 5. In the SSH session, modify the `/boot/uEnv.txt` file to instruct the microSD to act as a flasher for the internal eMMC of the Beaglebone Black.
    ```
    debian@beaglebone:~$ sudo nano /boot/uEnv.txt
    ```
    
    Remove the `#` sign on the last line of the file:
    ```
    #cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
    ```
    to
    ```
    cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
    ```
    
    Save the file via the key sequence `ctrl-x`, `y`, and `enter`.
 
 6. Restart the Beaglebone into the flasher.
    ```
    debian@beaglebone:~$ sudo reboot
    ```
 
 7. Wait for flashing to complete. The four user LEDs will enter into a cylon sequence (left-to-right bounce) when flashing. All LEDs should be solid when flashing completes successfully. If this is not true, google until you find the answer because I probably have no better idea about what's gone wrong than you do.
 
 8. POWER DOWN THE BEAGLEBONE VIA THE POWER BUTTON.
 
 9. Remove the microSD card.
 
10. Power the Beaglebone up again.
