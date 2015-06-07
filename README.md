About
====
<link to PPT>


Usage
====

 * Run example 1 on Rackspace Cloud, CentOS 6 (PVHVM).

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

	* The yaml file we sent will show up under here.
	```
	cat /var/lib/cloud/instance/cloud-config.txt 
	```

	* Runcmd arguments from the Yaml file will also show under scripts.
	```
	cat /var/lib/cloud/instance/scripts/runcmd  
	```

	* The status is also nicely provided.
	```
	cat /var/lib/cloud/data/status.json
	```


 * Run example 2
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

