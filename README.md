About
====
<link to PPT>


Usage
====

 * Use your Rackspace Cloud account or get a [developer one for free](https://developer.rackspace.com/signup/)

 * Clone this repo to your local folder
 ```
 git clone https://github.com/srirajan/cloudinit-demo
 cd cloudinit-demo
 ```

 * Run example 1 on Rackspace Cloud, CentOS 6 (PVHVM). Replace 'key' with your own key name. If you don't have a key 

```
key=sri-key
nova boot --flavor=general1-1 \
--image=518d156d-d4e0-483d-a7db-89cd27b50180 \
--key-name $key \
--config-drive=true \
--user-data=example1.yaml \
c0001
```

 * A look under the hood 

	* With the config drive you should see a small 67MB~ disk
	```
	fdisk -l

	Disk /dev/xvda: 21.5 GB, 21474836480 bytes
	255 heads, 63 sectors/track, 2610 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x00040be1

	    Device Boot      Start         End      Blocks   Id  System
	/dev/xvda1   *           1        2611    20970496   83  Linux

	Disk /dev/xvdd: 67 MB, 67108864 bytes
	255 heads, 63 sectors/track, 8 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0x00000000
	```

	* Mount the drive meta_data.json
	```
	mkdir -p /mnt/configdrive
	mount /dev/xvdd  /mnt/configdrive
	```

	* Look at the meta data files
	```
	cat /mnt/configdrive/openstack/latest/meta_data.json | python -m json.tool

	cat /mnt/configdrive/openstack/latest/vendor_data.json | python -m json.tool

	```

	* The yaml file we sent will show up under both these locations.
	```
	less  /mnt/configdrive/openstack/latest/user_data
	less /var/lib/cloud/instance/cloud-config.txt 
	```

	* Unmount - A good admin never leaves unwanted drives mounted :)
	```
	umount /mnt/configdrive
	```

	* Runcmd arguments from the Yaml file will also show under scripts.
	```
	less /var/lib/cloud/instance/scripts/runcmd  
	```

	* The status is also nicely provided.
	```
	less /var/lib/cloud/data/status.json
	```

	* Review logs
	```
	#If you have the example 1 output config
	less /var/log/cloud-init-output.log 

	#Ubuntu
	less /var/log/cloud-init.log 

	#CentOS
	grep "CLOUDINIT" /var/log/messages
	```


 * Run example 2 & see if /home/demo/.chef/knife.rb was created
```
key=sri-key
nova boot --flavor=general1-1 \
--image=518d156d-d4e0-483d-a7db-89cd27b50180 \
--key-name $key \
--config-drive=true \
--user-data=example2.yaml \
c0003
```

 * Other Examples; See [example 3](https://github.com/srirajan/cloudinit-demo/blob/master/example3.yaml) & [example 4](https://github.com/srirajan/cloudinit-demo/blob/master/example4.yaml)

 * Read the (docs)[https://cloudinit.readthedocs.org/en/latest/]
 

