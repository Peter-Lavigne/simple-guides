# Adding storage to ec2 linux instance

## (1/3): Increse volume

Visit the EC2 console -> Volumes

Select the volume that needs to be increased. Check "attachment informatoin" in the details pane to determine which one

Actions -> Modify Volume

Increase the volume size. Note that 10 GB-Months cost $1

## (2/3): Extend partition

SSH into the instance

Run `lsblk` and find the partition. It should be located under a "disk" type and contain less space than the disk

Extend the partition with `sudo growpart /dev/<partition name> 1`

## (3/3): Extend file system

Run `df -h` and determine the file system name (such as `/dev/nvme0n1p1`). It should be the size of the rezied partition

Run `sudo resize2fs <file system name>`

Ensure that the file system is larger with `df -h`
