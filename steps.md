1. created 4 Redhat Linux servers and 1 ubuntu server
2. Named the 4 Redhat servers

- WEBSERVER 1
- WEBSERVER 2
- WEBSERVER 3
- NFS

3. The ubuntu server is named as DB
   [Servers image]![Alt text](images/proj7.1.PNG)

- command **lsbk** to list block devices
  on NFS ![Alt text](images/pro7.2.PNG)

- command **sudo gdisk** to creat partition on

  - /dev/xvdf ![Alt text](images/pro7.3.PNG)
  - /dev/xvdg ![Alt text](images/pro7.4.PNG)
  - /dev/xvdh ![Alt text](images/pro7.5.PNG)

- command **lsbk** to list block devices![Alt text](images/pro7.6.PNG)

4. installing lvm2 wih **sudo yum install lvm2 -y**

- command **sudo lvmdiskscan** to check for lvm partition

5. creating physical volumes with on the partition

- **sudo pvcreate /dev/xvdf1**
- **sudo pvcreate /dev/xvdg1**
- **sudo pvcreate /dev/xvdh1**
  ![Alt text](images/pro7.9.PNG)

- sudo pvs to check for the physical volume![Alt text](images/pro7.10.PNG)

6. create volume group "webdata" with and add the physical volume to the group
   **sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1**

- check the group with sudo vgs![Alt text](images/pro7.11.PNG)

7. creating Logical volumes

- lv-apps
- lv-logs
- lv-opt
- Each with 9G memeory and added the to the webdata-vg gropu i.e ** sudo lvcreate -n lv-apps -L 9G webata-vg**
  ![Alt text](images/pro7.12.PNG)

8. formating the 3 logical volumes as xfs

- **sudo mkfs -t xfs /dev/webdata-vg/lv-apps**
- **sudo mkfs -t xfs /dev/webdata-vg/lv-log**
- **sudo mkfs -t xfs /dev/webdata-vg/lv-opt**
  ![Alt text](images/pro7.13.PNG)

9. Creating mount points on /mnt directory for the logical volumes

- Mount lv-apps on /mnt/apps – To be used by webservers
- Mount lv-logs on /mnt/logs – To be used by webserver logs
- Mount lv-opt on /mnt/opt – To be used by Jenkins server
  - **sudo mkdir /mnt/apps**
  - **sudo mkdir /mnt/logs**
  - **sudo mkdir /mnt/opt**
    - **sudo mount /dev/webdata-vg/lv-apps /mnt/apps**
    - **sudo mount /dev/webdata-vg/lv-apps /mnt/logs**
    - **sudo mount /dev/webdata-vg/lv-apps /mnt/opt**
