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

	* With the config drive

``` 
# ls -l /var/lib/cloud/
total 24
drwxr-xr-x 2 root root 4096 Jun  7 11:41 data
drwxr-xr-x 2 root root 4096 Jun  7 11:41 handlers
drwxr-xr-x 3 root root 4096 Jun  7 11:41 instances
drwxr-xr-x 5 root root 4096 Jun  7 11:41 scripts
drwxr-xr-x 2 root root 4096 Jun  7 11:41 seed
drwxr-xr-x 2 root root 4096 Jun  7 11:42 sem
```

* Run example 2 on Rackspace Cloud, Ubuntu 12.04 LTS (PVHVM)

key=sri-key
nova boot --flavor=general1-1 \
--image=0d83aff5-9910-44aa-a721-1c6b28e3c9dc \
--key-name $key \
--config-drive=true \
--user-data=example2.yaml \
c0002


```
key=sri-key
nova boot --flavor=general1-1 \
--image=0d83aff5-9910-44aa-a721-1c6b28e3c9dc \
--key-name $key \
--config-drive=true \
--user-data=example2.yaml \
c0002
```

 * Other Examples; See example3.yaml & example4.yaml

