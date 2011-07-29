# GhettoUI

**ghettoUI** is an interactive frontend for the **ghettoVCB.sh** and **ghettoVCB-restore.sh** scripts by William Lam.

It is really easy to use. Just put **ghettoUI**, **ghettoVCB.sh** and **ghettoVCB-restore.sh** into a directory accessible to your ESXi host and you're done. This can be a directory on the ESXi host or on an NFS server. 

**ghettoUI** extracts the information of the available virtual machines from the current host and offers an interactive menu for performing a backup. 

To perform a restore **ghettoUI** checks the available datastores for valid backups and offers an interactive menu for a restore. 

## How it works

ghettoUI is a python script which uses just the available python interpreter and the **vim-cmd** to extract information about virtual machines and datastores from the current host. No other tools or libraries are necessary.

To perform a backup **ghettoUI** lists the available virtual machines and datastores using **vim-cmd**, parses the output and displays the information as an interactive menu to the user. Once the user has chosen a machine to backup **ghettoUI** creates the necessary configuration files on the fly and runs the **ghettoVCB.sh** script to perform the actual backup.

**ghettoUI** first checks if a configuration file **conf/${vm.name}.conf** exists, then it looks for **conf/default.conf**. If neither of them can be found then the builtin configuration is used.

To perform a restore ghettoUI looks for **BACKUPS** directories in all available datastores. It assumes the directory structure **/path/to/datastore/BACKUPS/vm/backup** and presents the user with an interactive menu. After the user has made a choice **ghettoUI** again creates the necessary configuration files and runs the **ghettoVCB-restore.sh** script.

## Screenshot

Below is a screenshot of a backup procedure

<pre>/vmfs/volumes/23ed4bf3-6292d161 # ls -1         
BACKUPS
LOGS
conf
conf/server-2.conf
ghettoUI
ghettoVCB-restore.sh
ghettoVCB.sh

/vmfs/volumes/23ed4bf3-6292d161 # ./ghettoUI

ghettoUI Menu 0.7
-----------------

What do you want to do?

* 1. Backup a virtual machine
  2. Restore a virtual machine

  Q. Quit

(ENTER: 1) > 

ghettoUI Menu 0.7
-----------------

Select a virtual machine

  1. Ubuntu Server
  2. Windows XP
  3. Windows Vista
  4. Windows 2000
  5. Windows 7
  6. server-1
  7. server-template
  8. server-2
  9. server-3
  10. server-4
  11. server-5
  12. server-6
  13. server-7
  14. firewall

  Q. Return

> 8

ghettoUI Menu 0.7
-----------------

Select a datastore

  1. datastore1 (VMFS)
  2. nfs1 (NFS)

  Q. Return

> 2

ghettoUI Menu 0.7
-----------------

Do you want to backup 'server-2' onto 'nfs1'?

  1. info   - Standard output
  2. debug  - Debug output
* 3. dryrun - Test only. No backup is performed

  Q. Return

(ENTER: 3) > 2

ghettoUI Menu 0.7
-----------------

Start backup

  1. Review configuration 'server-2' (conf/server-2.conf)
* 2. Start backup

  Q. Return

(ENTER: 2) > 1

--- conf/server-2.conf ---
VM_BACKUP_VOLUME=/vmfs/volumes/nfs1/BACKUPS
DISK_BACKUP_FORMAT=zeroedthick
VM_BACKUP_ROTATION_COUNT=3
POWER_VM_DOWN_BEFORE_BACKUP=1
ENABLE_HARD_POWER_OFF=0
ITER_TO_WAIT_SHUTDOWN=3
POWER_DOWN_TIMEOUT=5
ENABLE_COMPRESSION=0
ADAPTER_FORMAT=lsilogic
VM_SNAPSHOT_MEMORY=0
VM_SNAPSHOT_QUIESCE=0
ENABLE_NON_PERSISTENT_NFS=0
UNMOUNT_NFS=0
NFS_SERVER=
NFS_MOUNT=
NFS_LOCAL_NAME=
NFS_VM_BACKUP_DIR=
SNAPSHOT_TIMEOUT=15
EMAIL_LOG=0
EMAIL_DEBUG=0
EMAIL_SERVER=
EMAIL_SERVER_PORT=
EMAIL_TO=
EMAIL_FROM=
--- conf/server-2.conf ---

Press ENTER to continue

ghettoUI Menu 0.7
-----------------

Start backup

  1. Review configuration 'server-2' (conf/server-2.conf)
* 2. Start backup

  Q. Return

(ENTER: 2) > 
2011-07-29 10:50:23 -- info: === ghettoVCB LOG START ===

2011-07-29 10:50:23 -- debug: Succesfully acquired lock directory - /tmp/ghettoVCB.lock

2011-07-29 10:50:23 -- debug: HOST VERSION: VMware ESXi 4.1.0 build-260247
2011-07-29 10:50:23 -- debug: HOST LEVEL: VMware ESXi 4.1.0 GA
2011-07-29 10:50:23 -- debug: HOSTNAME: kleinebox.dragage.yde

2011-07-29 10:50:23 -- info: CONFIG - USING GLOBAL GHETTOVCB CONFIGURATION FILE = conf/server-2.conf
2011-07-29 10:50:23 -- info: CONFIG - VERSION = 2011_05_22_1
2011-07-29 10:50:23 -- info: CONFIG - GHETTOVCB_PID = 34340
2011-07-29 10:50:23 -- info: CONFIG - VM_BACKUP_VOLUME = /vmfs/volumes/nfs1/BACKUPS
2011-07-29 10:50:23 -- info: CONFIG - VM_BACKUP_ROTATION_COUNT = 3
2011-07-29 10:50:23 -- info: CONFIG - VM_BACKUP_DIR_NAMING_CONVENTION = 2011-07-29_10-50-23
2011-07-29 10:50:23 -- info: CONFIG - DISK_BACKUP_FORMAT = zeroedthick
2011-07-29 10:50:23 -- info: CONFIG - ADAPTER_FORMAT = lsilogic
2011-07-29 10:50:23 -- info: CONFIG - POWER_VM_DOWN_BEFORE_BACKUP = 1
2011-07-29 10:50:23 -- info: CONFIG - ENABLE_HARD_POWER_OFF = 0
2011-07-29 10:50:23 -- info: CONFIG - ITER_TO_WAIT_SHUTDOWN = 3
2011-07-29 10:50:23 -- info: CONFIG - POWER_DOWN_TIMEOUT = 5
2011-07-29 10:50:23 -- info: CONFIG - SNAPSHOT_TIMEOUT = 15
2011-07-29 10:50:23 -- info: CONFIG - LOG_LEVEL = debug
2011-07-29 10:50:23 -- info: CONFIG - BACKUP_LOG_OUTPUT = /vmfs/volumes/23ed4bf3-6292d161/LOGS/server-2-backup-2011-07-29_10-50-23.log
2011-07-29 10:50:23 -- info: CONFIG - VM_SNAPSHOT_MEMORY = 0
2011-07-29 10:50:23 -- info: CONFIG - VM_SNAPSHOT_QUIESCE = 0
2011-07-29 10:50:23 -- info: CONFIG - VMDK_FILES_TO_BACKUP = all
2011-07-29 10:50:23 -- info: CONFIG - EMAIL_LOG = 0
2011-07-29 10:50:23 -- info: 
2011-07-29 10:50:24 -- debug: Storage Information before backup: 
2011-07-29 10:50:24 -- debug: SRC_DATASTORE: datastore1
2011-07-29 10:50:24 -- debug: SRC_DATASTORE_CAPACITY: 227.8 GB
2011-07-29 10:50:24 -- debug: SRC_DATASTORE_FREE: 128.1 GB
2011-07-29 10:50:24 -- debug: SRC_DATASTORE_BLOCKSIZE: 1
2011-07-29 10:50:24 -- debug: SRC_DATASTORE_MAX_FILE_SIZE: 256 GB
2011-07-29 10:50:24 -- debug: 
2011-07-29 10:50:24 -- debug: DST_DATASTORE: nfs1
2011-07-29 10:50:24 -- debug: DST_DATASTORE_CAPACITY: 297.8 GB
2011-07-29 10:50:24 -- debug: DST_DATASTORE_FREE: 113.6 GB
2011-07-29 10:50:24 -- debug: DST_DATASTORE_BLOCKSIZE: NA
2011-07-29 10:50:24 -- debug: DST_DATASTORE_MAX_FILE_SIZE: NA
2011-07-29 10:50:24 -- debug: 
2011-07-29 10:50:25 -- debug: getVMDKs() - server-2.vmdk###5:
2011-07-29 10:50:25 -- info: Powering off initiated for server-2, backup will not begin until VM is off...
2011-07-29 10:50:25 -- info: VM is still on - Iteration: 0 - sleeping for 60secs (Duration: 0 seconds)
2011-07-29 10:51:26 -- info: VM is powerdOff
2011-07-29 10:51:26 -- info: Initiate backup for server-2
2011-07-29 10:51:26 -- debug: findVMDK() - Searching for VMDK: "server-2.vmdk" to backup
2011-07-29 10:51:26 -- debug: /sbin/vmkfstools -i "/vmfs/volumes/datastore1/server-2/server-2.vmdk" -a "lsilogic" -d "zeroedthick" "/vmfs/volumes/nfs1/BACKUPS/server-2/server-2-2011-07-29_10-50-23/server-2.vmdk"
Destination disk format: VMFS zeroedthick
Cloning disk '/vmfs/volumes/datastore1/server-2/server-2.vmdk'...
Clone: 95% done.
2011-07-29 10:53:33 -- info: Powering back on server-2
2011-07-29 10:53:35 -- info: Backup Duration: 2.15 Minutes
2011-07-29 10:53:35 -- info: Successfully completed backup for server-2!

2011-07-29 10:53:36 -- debug: Storage Information after backup: 
2011-07-29 10:53:36 -- debug: SRC_DATASTORE: datastore1
2011-07-29 10:53:36 -- debug: SRC_DATASTORE_CAPACITY: 227.8 GB
2011-07-29 10:53:36 -- debug: SRC_DATASTORE_FREE: 128.1 GB
2011-07-29 10:53:36 -- debug: SRC_DATASTORE_BLOCKSIZE: 1
2011-07-29 10:53:37 -- debug: SRC_DATASTORE_MAX_FILE_SIZE: 256 GB
2011-07-29 10:53:37 -- debug: 
2011-07-29 10:53:37 -- debug: DST_DATASTORE: nfs1
2011-07-29 10:53:37 -- debug: DST_DATASTORE_CAPACITY: 297.8 GB
2011-07-29 10:53:37 -- debug: DST_DATASTORE_FREE: 113.6 GB
2011-07-29 10:53:37 -- debug: DST_DATASTORE_BLOCKSIZE: NA
2011-07-29 10:53:37 -- debug: DST_DATASTORE_MAX_FILE_SIZE: NA
2011-07-29 10:53:37 -- debug: 
2011-07-29 10:53:37 -- info: ###### Final status: All VMs backed up OK! ######

2011-07-29 10:53:37 -- debug: Succesfully removed lock directory - /tmp/ghettoVCB.lock

2011-07-29 10:53:37 -- info: === ghettoVCB LOG END ===


ghettoUI Menu 0.7
-----------------

What do you want to do?

* 1. Backup a virtual machine
  2. Restore a virtual machine

  Q. Quit

(ENTER: 1) > q
/vmfs/volumes/23ed4bf3-6292d161 # 

</pre>

## Known pitfalls

* **ghettoUI** currently has a hardcoded configuration for the restore for all virtual machines. See the `GhettoVCB.restore()` methods for details

* **ghettoUI** does not check if a restore is possible, i.e. if there is not already a virtual machine with the same name on the same datastore

## Version History

0.7 - 29 Jul 2011
-----------------

 * Added support for external configuration files
 * Added support for reviewing the configuration prior to backup
 * Added menu defaults
 
0.6 - 28 Jul 2011
-----------------

 * Fixed handling of VMs with spaces in their names
 * Fixed handling of inaccessible NFS datastores

0.5 - 11 Jul 2011
-----------------

 * First useful version

## License

**ghettoUI** is MIT licensed. I'm happy if it is useful to you. 

## Disclaimer

Please use **ghettoUI** at your own risk. It works in my environment but hasn't been battle tested and for sure isn't yet a0.7s configurable as it needs to be for the different configurations out there. 

## Acknowledgements

**ghettoVCB** and **ghettoVCB-restore** were written by William Lam. You can find more information at http://www.virtualghetto.com/. 

The ghettoVCB documentation can be found here: http://communities.vmware.com/docs/DOC-8760

The ghettoVCB VMTN group can be found here: http://communities.vmware.com/groups/ghettovcb