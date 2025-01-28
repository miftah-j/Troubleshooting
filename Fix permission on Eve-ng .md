

  
(All commands must be run as root)

1. Check that the 71st line in the specified file (/opt/unetlab/html/includes/init.php) is such as:


> **$kvm_family = file_get_contents("/opt/unetlab/platform")**


If it's not, edit it to look like this.

2. Run the command:

    

> **dmesg | grep -i cpu | grep -i -e intel -e amd**

if you get an output line with the word "Intel"

then run the following command:

> **echo "intel" > /opt/unetlab/platform**

If you get an output line with the word "amd", then run:

> **echo "amd" > /opt/unetlab/platform**

this should solve your problem with launching `unl_wrapper -a fixpermissions`
