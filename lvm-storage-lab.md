# 💾 LVM Storage Management Lab

**Goal:** Demonstrate storage administration skills by implementing Logical Volume Management — a core sysadmin competency.

---

## Why LVM Matters

LVM lets you resize, extend, and snapshot storage **without downtime** — a critical skill for production Linux environments.

---

## Lab Environment

- OS: Rocky Linux 9 / RHEL 9
- Added a new virtual disk: `/dev/sdb` (10GB) in VirtualBox

---

## Step-by-Step Implementation

### Step 1 — Create a Physical Volume (PV)

```bash
# Verify new disk is detected
lsblk

# Initialize disk as physical volume
pvcreate /dev/sdb

# Verify
pvdisplay
pvs
```

---

### Step 2 — Create a Volume Group (VG)

```bash
# Create volume group named "data_vg"
vgcreate data_vg /dev/sdb

# Verify
vgdisplay
vgs
```

---

### Step 3 — Create a Logical Volume (LV)

```bash
# Create 5GB logical volume named "data_lv"
lvcreate -L 5G -n data_lv data_vg

# Verify
lvdisplay
lvs
```

---

### Step 4 — Format and Mount

```bash
# Format with ext4 filesystem
mkfs.ext4 /dev/data_vg/data_lv

# Create mount point and mount
mkdir -p /mnt/data
mount /dev/data_vg/data_lv /mnt/data

# Verify
df -h /mnt/data
```

---

### Step 5 — Make Mount Persistent (fstab)

```bash
# Get the UUID
blkid /dev/data_vg/data_lv

# Add to /etc/fstab
echo "UUID=<your-uuid>  /mnt/data  ext4  defaults  0 2" >> /etc/fstab

# Test fstab without rebooting
mount -a
```

---

### Step 6 — Extend the Logical Volume (No Downtime)

```bash
# Extend by 2GB
lvextend -L +2G /dev/data_vg/data_lv

# Resize the filesystem to use new space
resize2fs /dev/data_vg/data_lv

# Verify new size
df -h /mnt/data
```

---

## Verification Output

```
$ lvs
  LV      VG      Attr       LSize Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  data_lv data_vg -wi-ao---- 7.00g

$ df -h /mnt/data
Filesystem                    Size  Used Avail Use% Mounted on
/dev/mapper/data_vg-data_lv   6.9G   24M  6.5G   1% /mnt/data
```

---

## Skills Demonstrated

- Physical volume creation and management
- Volume group creation and extension
- Logical volume provisioning and resizing
- Persistent storage configuration via `/etc/fstab`
- **Zero-downtime** disk extension in a live environment

---
