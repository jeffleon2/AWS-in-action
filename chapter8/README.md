1.) Check the disk
```
> lsblk
```

2.) Create xfs fyle system 
```
> sudo mkfs -t xfs /dev/$disk
```

3.) Point of mount

```
> sudo mkdir /data
```
4.) Mount disk 

```
> sudo mount /dev/$disk /data 
```

5) Verify mount disk
```
> df -h
> df -h | grep /data
```

### Performance

```
> sudo dd if=/dev/zero of=/data/tempfile bs=1M count=1024 # dd tool | input infinte zeros /dev/zero | /data/tempfile output | read size bs | number of times 'count'
```

### Snapshots

1.) Create
```
> aws ec2 create-snapshot --volume-id $VolumeId
```

2.) 

```
> aws ec2 describe-snapshots --snapshot-ids $SnapshotId
```

* Creating a snapshot safely 

1.) 
```
> sudo fsfreeze -f /data
```

2.) Create Snapshot 
```
> aws ec2 create-snapshot --volume-id $VolumeId
```
3.) 
```
sudo fsfreeze -u /data
```

### Volume By Snapshot

1.) 

```
aws ec2 create-volume --snapshot-id $Snapshotid
```