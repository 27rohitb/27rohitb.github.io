# Cgroups:

## Installing Cgroups on Ubuntu:

```
sudo apt-get install cgroup-bin cgroup-lite cgroup-tools cgroupfs-mount libcgroup1
```

## Configuring Cgroups

1. Get the username
```
whoami
```

2. Create temporary cgroup with permission for this user:
```
sudo cgcreate -t rohit -a rohit -g memory:test1
sudo cgreate -t <username> -a <username> -g <controlP_param>:<cgroup_name>
```

3. Set limits on for given control param:
```
cgset -r memory.limit_in_bytes=90G test1
cgest -r <control_param>=<value> <cgroup_name>
```

4. Execute the given file in this cgroup:
```
cgexec -g memory:test1 python3 multigate_sim.py
cgexec -g <control_param>:<cgroup_name> <whatever you wanna run>
```

Links:

* <https://www.carnaghan.com/knowledge-base/how-to-find-your-uiduserid-and-gidgroupid-in-linux-via-the-command-line/>
* <https://doc.callmematthi.eu/cgroups.html>
* <https://www.cloudsigma.com/control-groups/>
* <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/starting_a_process>
* <https://wiki.archlinux.org/index.php/cgroups>
* <https://askubuntu.com/questions/651741/cgroups-error-cgroup-change-of-group-failed>
