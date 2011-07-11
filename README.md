### GhettoUI

**ghettoUI** is an interactive frontend for the **ghettoVCB.sh** and **ghettoVCB-restore.sh** scripts by William Lam.

It is really easy to use. Just keep `ghettoUI`, `ghettoVCB.sh` and  `ghettoVCB-restore.sh` in a directory accessible to your ESXi host and you're done. This can be a directory on the ESXi host or 

**ghettoUI** extracts the information of the available virtual machines from the current host and offers an interactive menu for performing a backup. 

To perform a restore *ghettoUI* checks the available datastores for valid backups and offers an interactive menu for a restore. 

### How it works

ghettoUI is a python script which uses just the available python interpreter and the `vim-cmd` to extract information about virtual machines and datastores from the current host. No other tools or libraries are necessary.

To perform a backup ghettoUI lists the available virtual machines and datastores using vim-cmd, parses the output and displays the information as an interactive menu to the user. Once the user has chosen a machine to backup ghettoUI creates the necessary configuration files on the fly and runs the `ghettoVCB.sh` script to perform the actual backup.

To perform a restore ghettoUI looks for `BACKUP` directories in all available datastores. It assumes the directory structure `/path/to/datastore/BACKUP/vm-name/backup-name` and presents the user with an interactive menu. After the user has made a choice **ghettoUI** again creates the necessary configuration files and runs the `ghettoVCB-restore.sh` script.

### Screenshot

This is a screenshot of a backup procedure

  /vmfs/volumes/23ed4bf3-6292d161 # ls         
  BACKUPS               LOGS                  ghettoUI              ghettoVCB-restore.sh  ghettoVCB.sh
  /vmfs/volumes/23ed4bf3-6292d161 # ./ghettoUI 
  
  ghettoUI Menu 0.5
  -----------------

  What do you want to do?

  1. Backup a virtual machine
  2. Restore a virtual machine

  Q. Quit

  > 1
  ghettoUI Menu 0.5
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

  > 12
  ghettoUI Menu 0.5
  -----------------

  Select a datastore

  1. datastore1 (VMFS)
  2. nfs1 (NFS)

  Q. Return

  > 2
  ghettoUI Menu 0.5
  -----------------

  Do you want to backup 'server-6' onto 'nfs1'?

  1. info   - Standard output
  2. debug  - Debug output
  3. dryrun - Test only. No backup is performed

  Q. Return

  > 1
  2011-07-11 20:21:56 -- info: ============================== ghettoVCB LOG START ==============================

  ...

  2011-07-11 20:21:58 -- info: Initiate backup for server-6
  2011-07-11 20:21:58 -- info: Creating Snapshot "ghettoVCB-snapshot-2011-07-11" for server-6
  Destination disk format: VMFS thin-provisioned
  Cloning disk '/vmfs/volumes/datastore1/server-6/server-6.vmdk'...
  Clone: 94% done.
  2011-07-11 20:23:46 -- info: Removing snapshot from server-6 ...
  2011-07-11 20:23:46 -- info: Backup Duration: 1.80 Minutes
  2011-07-11 20:23:47 -- info: Successfully completed backup for server-6!
  2011-07-11 20:23:48 -- info: ###### Final status: All VMs backed up OK! ######

  2011-07-11 20:23:48 -- info: ============================== ghettoVCB LOG END ================================

  ghettoUI Menu 0.5
  -----------------

  What do you want to do?

  1. Backup a virtual machine
  2. Restore a virtual machine

  Q. Quit

  > q
  /vmfs/volumes/23ed4bf3-6292d161 # 
  

### Known pitfalls

* ghettoUI currently has a hardcoded configuration for backup and restore for all virtual machines. See the GhettoVCB.backup() and GhettoVCB.restore() methods for details

* ghettoUI does not check if a restore is possible, i.e. if there is not already a virtual machine with the same name on the same datastore

### License

ghettoUI is MIT licensed. I'm happy if it is useful to you. 

### Acknowledgements

ghettoVCB and ghettoVCB-restore were written by William Lam. You can find more information at http://www.virtualghetto.com/. 

The ghettoVCB documentation can be found here: http://communities.vmware.com/docs/DOC-8760

The ghettoVCB VMTN group can be found here: http://communities.vmware.com/groups/ghettovcb