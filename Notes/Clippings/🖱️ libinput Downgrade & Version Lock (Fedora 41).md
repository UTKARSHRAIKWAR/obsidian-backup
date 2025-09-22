# 🖱️ libinput Downgrade & Version Lock (Fedora 41)

> **Goal:** Fix touchpad issues by downgrading `libinput` to a stable version and preventing Fedora from auto-upgrading it.  
> **System:** Fedora 41 (Wayland)

---

## ⚡ Background
The latest `libinput` update caused instability with my touchpad.  
To restore functionality, I downgraded to a known working version (**1.26.2**) and locked it using DNF.

---

## 📥 Step 1: Install the Working Version

I installed the specific RPM files for `libinput` and its development package:

```bash
sudo dnf install ./libinput-1.26.2-1.fc41.x86_64.rpm ./libinput-devel-1.26.2-1.fc41.x86_64.rpm
```

✔️ This ensures the system is using version **1.26.2**.  

---

## 🔒 Step 2: Prevent Future Upgrades (Version Lock)

To stop Fedora from upgrading `libinput` again, I applied **DNF versionlock**.

- **Check locked packages**
```bash
sudo dnf versionlock list
```

- **Add lock for libinput + devel**
```bash
sudo dnf versionlock add libinput libinput-devel
```

✔️ Both `libinput` and `libinput-devel` are now locked.

---

## 🛠️ Step 3: (Optional) Remove Lock in Future

If I ever need to upgrade `libinput`, I must first remove the lock:

```bash
sudo dnf versionlock delete libinput libinput-devel
```

Then, I can safely run:
```bash
sudo dnf upgrade libinput libinput-devel
```

---

## ✅ Final Notes
- Downgrade fixed the touchpad gestures and restored stability.  
- Version lock ensures Fedora doesn’t break my setup in the future.  
- Keep the `.rpm` files backed up in case Fedora removes old versions.  

---

## 📚 References
- [DNF versionlock Documentation](https://dnf.readthedocs.io/en/latest/command_ref.html#versionlock)