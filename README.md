# Android-local-dns-setting
note to record how to setting a local dns for Android Wi-Fi hotspot

1. need root Android device

2. edit and save file, hosts for config local dns

       # open hotspot in Android device
       
       # get static inet address with cmd
       adb shell ifconfig # record ip in : wlan0 -> inet addr:$staticIP e.g. 192.168.43.1
       
       # pull file, hosts
       adb pull /system/etc/hosts hosts
       
       # edit hosts
       192.168.43.1 aa.com
       
       # push edited hosts to cover old 
       adb push hosts /system/etc/hosts
       # adb: error: failed to copy 'hosts' to '/system/etc/hosts': remote couldn't create file: Read-only file system
       
       # fix error with cmds
       adb root 
       adb disable-verity # success log : Verity already disabled on /system
       adb remount # success log : remount succeeded
       
       # try push cmd again
       adb push hosts /system/etc/hosts # success log : hosts: 1 file pushed. 0.0 MB/s (76 bytes in 0.011s)
       
3. above 1 and 2, you can get serve from your httpServer in Android device like http://192.168.43.1:8080/index.html as http://aa.com:8080/index.html        
       
