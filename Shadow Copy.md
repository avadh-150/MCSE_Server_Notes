# Simple Step : Configuring Shadow Copies in Windows Server 2022

August 2, 2014

**What Are Shadow Copies?**

A shadow copy is a **snapshot of a set of data, such as a file or folder**.

Shadow copies provide the capability to recover files and folders based on snapshots of storage drives.

After a snapshot is taken, you can view and potentially restore previous versions of files and folders from that snapshot.

A shadow copy does not make a complete copy of all files for each snapshot.

Instead, after a snapshot is taken, Windows Server 2012 R2 tracks changes to the drive. A specific amount of disk space is allocated for tracking the changed disk blocks. When you access a previous version of a file, some of the content might be in the current version of the file, and some might be in the snapshot.

On this post this time, lets go through a very simple step how you can implement & configure shadow copies in Windows Server 2012 R2…

1- For this Shadow Copies demo, i will be using my **F: drive which located in my OSI-SVR01 server**…

right click **F: drive** and then click **Configure Shadow Copies**…

[![1](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/110.png?w=497&h=434)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/110.png)

2 – In the Shadow Copies interface, click drive F:, and then click **Enable**…

[![2](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/22.png?w=497&h=435)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/22.png)

3 – In the Enable Shadow Copies interface, click **Yes**…

[![3](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/31.png?w=497&h=435)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/31.png)

4 – In the drive Shadow Copies interface, click **Settings**…

[![4](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/41.png?w=497&h=432)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/41.png)

5 – In the Settings interface, click **Schedule**…

[![5](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/51.png?w=497&h=436)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/51.png)

6 – In drive F:\ interface, change Schedule Task to Daily, change Start time to 3:00 AM, and then click Advanced…

[![6](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/61.png?w=497&h=435)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/61.png)

7 – In the Advanced Schedule Options interface, select Repeat task, and then set the frequency to every 1 hours, then Select Time, and then change the time value to 2:58 AM…

[![7](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/71.png?w=497&h=433)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/71.png)

8 – Click OK, and then in Settings interface, type 500 in Use limit: box and then click OK…

[![8](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/81.png?w=497&h=431)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/81.png)

9 – next, open IT Consultant folder and then create a file call Profile…

Switch back to the Shadow Copies interface. It should be opened on the Shadow Copies tab and then click Create Now…

[![9](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/91.png?w=497&h=433)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/91.png)

10 – under Shadow copies of selected volume notice that you should have new date & time for shadow copies…

[![10](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/101.png?w=497&h=436)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/101.png)

11 – to simulate the shadow copies function, lets delete the profile.txt file…

[![11](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/111.png?w=497&h=434)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/111.png)

12 – In File Explorer, right-click the IT Consultant folder, and then click Properties…

[![12](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/121.png?w=497&h=433)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/121.png)

13 – In the IT Consultant Properties dialog box, click the Previous Versions tab…

then click the most recent folder version for IT Consultant, and then click Open…

[![13](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/131.png?w=497&h=433)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/131.png)

14 – Confirm that Profile.txt is in the folder, right-click Profile.txt, and then click Copy…

[![14](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/141.png?w=497&h=435)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/141.png)

15 – lastly, in the other File Explorer window, right-click the IT Consultant folder, and then click Paste…

[![15](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/151.png?w=497&h=436)](https://mizitechinfo.wordpress.com/wp-content/uploads/2014/08/151.png)