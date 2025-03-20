# WSL GUI ON WIN11
# **📖 Xfce Desktop on WSL2 – Complete Documentation**  
This guide covers everything needed to **install, configure, and use Xfce on WSL2** with **Xrdp** for remote desktop access.

![Xfce Desktop]()


---

## **📌 Part 1: First-Time Setup (Installation & Uninstallation)**  
This section explains how to set up Xfce for the first time.

### **🔹 Step 1: Update Your System**
Before installing anything, update your WSL Ubuntu packages:  
```bash
sudo apt update && sudo apt upgrade -y
```

---

### **🔹 Step 2: Install Xfce Desktop**
Xfce is a **lightweight** desktop environment suitable for WSL2. Install it using:  
```bash
sudo apt install xfce4 xfce4-goodies -y
```
- `xfce4`: Core Xfce desktop environment.  
- `xfce4-goodies`: Extra utilities and plugins for better experience.  

---

### **🔹 Step 3: Install Xrdp (Remote Desktop Server)**
To access Xfce via Windows **Remote Desktop (RDP)**, install **Xrdp**:  
```bash
sudo apt install xrdp -y
sudo systemctl enable xrdp
sudo systemctl start xrdp
```
- `enable xrdp` → Starts Xrdp automatically at boot.  
- `start xrdp` → Runs Xrdp immediately.  

---

### **🔹 Step 4: Configure Xfce for Xrdp**
Tell Xrdp to start the **Xfce session** instead of a different desktop:  
```bash
echo "xfce4-session" > ~/.xsession
sudo service xrdp restart
```
Now, Xfce will launch when you connect via RDP.

---

### **🔹 Step 5: Connect to Xfce from Windows**
1. Open **Remote Desktop Connection** (`mstsc.exe`).  
2. Enter:  
   ```
   localhost:3389
   ```
3. Click **Connect** and log in with your **WSL username & password**.  
4. 🎉 You should see your **Xfce desktop** inside Windows!

---

### **🛑 Uninstalling Xfce and Xrdp**
If you want to **remove everything**:  
```bash
sudo apt remove --purge xfce4 xfce4-goodies xrdp -y
sudo apt autoremove -y
```
This will **completely remove Xfce and Xrdp** from WSL.

---

## **📌 Part 2: Daily Usage & Managing Xfce in WSL**
If you have already installed Xfce and want to **log in again**, follow these steps.

---

### **🔹 Start Xrdp (If Not Running)**
If you restart your PC or shut down WSL, Xrdp might not be running. Start it manually:  
```bash
sudo systemctl start xrdp
```

---

### **🔹 Stop Xrdp (If Not Needed)**
To stop the Xrdp service:  
```bash
sudo systemctl stop xrdp
```

---

### **🔹 Restart Xrdp (For Troubleshooting)**
If Xrdp is acting weird, restart it:  
```bash
sudo systemctl restart xrdp
```

---

### **🔹 Check If Xrdp is Running**
To verify that Xrdp is active, run:  
```bash
sudo systemctl status xrdp
```
If it says **"active (running)"**, you’re good to go! ✅  

---

### **🔹 Log in to Xfce Desktop Again**
If you’ve already set up everything:
1. Open **Remote Desktop Connection** (`mstsc.exe`).
2. Type **`localhost:3389`** and connect.
3. Enter your **WSL username & password**.
4. 🎉 Welcome back to your **Xfce desktop**!

---

## **📌 Additional Tips**
### **🔹 Start Xrdp Automatically on WSL Launch**
If you want **Xrdp to start every time you open WSL**, add this line to your **~/.bashrc** file:  
```bash
sudo systemctl start xrdp
```
Now, every time you open WSL, Xrdp will start automatically.

---

### **🔹 Install a Web Browser**
By default, Xfce doesn’t have a browser. Install **Firefox** or **Chromium**:  
```bash
sudo apt install firefox -y
sudo apt install chromium-browser -y
```

---

### **🔹 Install a File Manager (If Needed)**
Xfce comes with `Thunar`, but if you prefer **GNOME’s Nautilus**:  
```bash
sudo apt install nautilus -y
```

---

## **📌 Conclusion**
- **First-time setup** → Install **Xfce + Xrdp**, configure, and connect via **RDP**.  
- **Daily use** → Start **Xrdp**, log in via **RDP**, and enjoy Linux on Windows!  
- **Uninstall anytime** → Use `apt remove --purge xfce4 xfce4-goodies xrdp`.  

This guide ensures you can **easily use Xfce in WSL**. Let me know if you need any tweaks! 🚀🔥
