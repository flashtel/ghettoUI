### GhettoUI

*ghettoUI* is an interactive frontend for the *ghettoVCB.sh* and *ghettoVCB-restore.sh* scripts by William Lam.

It is really easy to use. Just keep `ghettoUI`, `ghettoVCB.sh` and  `ghettoVCB-restore.sh` in a directory accessible to your ESXi host and you're done. This can be a directory on the ESXi host or 

*ghettoUI* extracts the information of the available virtual machines from the current host and offers an interactive menu for performing a backup. 

To perform a restore *ghettoUI* checks the available datastores for valid backups and offers an interactive menu for a restore. 

### How it works

ghettoUI is a python script which uses just the available python interpreter and the `vim-cmd` to extract information about virtual machines and datastores from the current host. No other tools or libraries are necessary.

To perform a backup ghettoUI lists the available virtual machines and datastores using vim-cmd, parses the output and displays the information as an interactive menu to the user. Once the user has chosen a machine to backup ghettoUI creates the necessary configuration files on the fly and runs the `ghettoVCB.sh` script to perform the actual backup.

To perform a restore ghettoUI looks for `BACKUP` directories in all available datastores. It assumes the directory structure /path/to/datastore/BACKUP/vm-name/backup-name and presents the user with an interactive menu. After the user has made a choice ghettoUI again creates the necessary configuration files and runs the `ghettoVCB-restore.sh` script.

### Known pitfalls

* ghettoUI currently has a hardcoded configuration for backup and restore for all virtual machines. See the GhettoVCB.backup() and GhettoVCB.restore() methods for details

* ghettoUI does not check if a restore is possible, i.e. if there is not already a virtual machine with the same name on the same datastore

### License

ghettoUI is MIT licensed. I'm happy if it is useful to you. 

### Acknowledgements

ghettoVCB and ghettoVCB-restore were written by William Lam. You can find more information at http://www.virtualghetto.com/. 

The ghettoVCB documentation can be found here: http://communities.vmware.com/docs/DOC-8760

The ghettoVCB VMTN group can be found here: http://communities.vmware.com/groups/ghettovcb