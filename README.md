# WSL GUI ON WIN11
# **📖 Xfce Desktop on WSL2 – Complete Documentation**  
This guide covers everything needed to **install, configure, and use Xfce on WSL2** with **Xrdp** for remote desktop access.

![Xfce Desktop](https://raw.githubusercontent.com/dev-arctik/WSL-GUI/refs/heads/main/gui_screenshot.png)


---

## **🟢 Part 1: First-Time Setup**  
### **1️⃣ Install Required Packages**  
Before installing anything, update your WSL Ubuntu packages:  
```bash
sudo apt update && sudo apt upgrade -y
```

Xfce is a **lightweight** desktop environment suitable for WSL2. Install it using:  
```bash
sudo apt install xfce4 xfce4-goodies -y
```
- `xfce4`: Core Xfce desktop environment.  
- `xfce4-goodies`: Extra utilities and plugins for better experience.  

---

### **2️⃣ Install & Configure XRDP (Remote Desktop Server)**  
To access Xfce via Windows **Remote Desktop (RDP)**, install **Xrdp**:  
```bash
sudo apt install xrdp -y
```
Enable the XRDP service to start automatically:  
```bash
sudo systemctl enable xrdp
```
Start the XRDP service:  
```bash
sudo systemctl start xrdp
```

### **3️⃣ Configure XRDP to Use XFCE4**  
Edit the `startwm.sh` file:  
```bash
sudo nano /etc/xrdp/startwm.sh
```
Delete everything inside and **replace it** with the following:  
```bash
#!/bin/sh
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR

. /etc/X11/Xsession
startxfce4
```
Save and exit:  
- Press `CTRL + X`  
- Press `Y` (Yes)  
- Press `Enter`  

Make sure the file is executable:  
```bash
sudo chmod +x /etc/xrdp/startwm.sh
```

### **4️⃣ Restart XRDP**  
```bash
sudo systemctl restart xrdp
```

### **5️⃣ Allow XRDP in Firewall (If Needed)**
If using a firewall, allow the XRDP port:  
```bash
sudo ufw allow 3389/tcp
```

---

## **🛑 Uninstall XRDP & XFCE4 (If Needed)**  
If you want to remove everything:  
```bash
sudo apt remove --purge xrdp xfce4 xfce4-goodies -y
sudo apt autoremove -y
sudo rm -rf /etc/xrdp
```

---

## **🟢 Part 2: Using XRDP After Setup**  
### **1️⃣ Starting XRDP Service (If Not Running)**  
```bash
sudo systemctl start xrdp
```

### **2️⃣ Connecting via Remote Desktop**  
1. Open **Remote Desktop Connection (`mstsc.exe`)** on Windows.  
2. Enter `localhost:3389` as the address.  
3. Login with your **WSL username and password**.  

### **3️⃣ Properly Disconnecting from XRDP**
- **To log out completely:**  
  Go to **Applications Menu → Log Out**  
- **To keep the session running:**  
  Simply close the RDP window (`X`) and select **"OK"** to disconnect without logging out.  

### **4️⃣ Stopping XRDP Manually**
If needed, stop XRDP manually:  
```bash
sudo systemctl stop xrdp
```

### **5️⃣ Restarting XRDP in Case of Issues**  
```bash
sudo systemctl restart xrdp
```

### **6️⃣ Debugging Connection Issues**  
If you get disconnected, check logs:  
```bash
cat ~/.xsession-errors
sudo journalctl -u xrdp --no-pager | tail -50
```

---

## **🎯 Troubleshooting Tips**
- **If Remote Desktop disconnects immediately:**  
  - Make sure `startwm.sh` is correctly configured (see Step 3).  
  - Restart XRDP:  
    ```bash
    sudo systemctl restart xrdp
    ```  
- **If you get a black screen after login:**  
  - Try running:  
    ```bash
    echo "xfce4-session" > ~/.xsession
    ```

---

This documentation covers everything from **installation to troubleshooting**. 🚀 Let me know if you'd like any modifications! 😊