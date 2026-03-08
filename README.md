# 💾 LVM Storage Management

A hands-on Linux lab demonstrating Logical Volume Management (LVM) —
a core skill for system administrators and DevOps engineers.

---

## 📌 What is LVM?

LVM (Logical Volume Manager) allows you to manage disk storage
flexibly — resize, extend, and snapshot volumes **without downtime**.
It's used in production Linux servers worldwide.

---

## 🎯 What I Did in This Lab

- ✅ Created a Physical Volume (PV) on a new disk
- ✅ Created a Volume Group (VG)
- ✅ Created a Logical Volume (LV)
- ✅ Formatted and mounted persistent storage
- ✅ Extended disk space **live** without unmounting

---

## 🛠️ Tools & Commands Used

| Command | Purpose |
|---|---|
| `pvcreate` | Initialize disk as physical volume |
| `vgcreate` | Create a volume group |
| `lvcreate` | Create a logical volume |
| `lvextend` | Extend volume size |
| `resize2fs` | Resize filesystem after extension |
| `mount` + `fstab` | Persistent mount on boot |

---

## 💻 Environment

- **OS:** Rocky Linux 9 / RHEL 9
- **Virtualization:** VirtualBox
- **Added Disk:** /dev/sdb (10GB virtual disk)

---

## 📄 Lab Documentation

Full step-by-step commands → [lvm-storage-lab.md](./lvm-storage-lab.md)
