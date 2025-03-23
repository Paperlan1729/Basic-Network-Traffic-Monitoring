# Basic-Network-Traffic-Monitoring

Creating a **network traffic analyzer** in **CMD (Command Prompt)** can be done using built-in Windows tools like `netstat` and `PowerShell`, or by installing third-party utilities like **Wireshark** or **Npcap**. Below is a step-by-step guide on how to monitor network traffic using CMD.

---

## **Method 1: Using `netstat` (Basic Analysis)**
`netstat` (Network Statistics) is a built-in tool in Windows that provides details about network connections, including active connections, listening ports, and statistics.

### **Steps to Monitor Network Traffic:**
1. **Open CMD as Administrator**  
   - Press `Win + R`, type **cmd**, and press `Ctrl + Shift + Enter` to open it as an administrator.

2. **Check Active Connections**  
   Run the following command to view all active network connections:
   ```cmd
   netstat -an
   ```
   This will display a list of all active TCP and UDP connections, along with their **IP addresses** and **port numbers**.

3. **Monitor Traffic in Real-Time**  
   To continuously monitor network activity, use:
   ```cmd
   netstat -an 5
   ```
   This refreshes the list every **5 seconds**.

4. **Find Specific Traffic (Example: Port 80 - HTTP Traffic)**  
   ```cmd
   netstat -an | findstr ":80"
   ```
   This filters connections using port **80** (HTTP traffic).

5. **Show Connections with Process IDs (PIDs)**  
   ```cmd
   netstat -ano
   ```
   This adds the **PID (Process ID)**, which you can use to identify applications consuming network bandwidth.

6. **Identify Which Application is Using the Network**  
   Find the program associated with a PID using:
   ```cmd
   tasklist | findstr <PID>
   ```
   Replace `<PID>` with the process ID from the `netstat -ano` output.

---

## **Method 2: Using PowerShell for Advanced Monitoring**
If you want **real-time network traffic monitoring** in a more structured format, use PowerShell.

### **View Real-Time Network Traffic**
1. Open **PowerShell as Administrator** (`Win + X → Windows Terminal (Admin)`)
2. Run:
   ```powershell
   Get-NetTCPConnection
   ```
   This provides details about all active **TCP connections**.

3. **Filter by Specific Ports**
   ```powershell
   Get-NetTCPConnection | Where-Object { $_.LocalPort -eq 443 }
   ```
   This filters connections using **port 443** (HTTPS).

---

## **Method 3: Using `pktmon` (Windows Packet Monitoring)**
Windows has a hidden **packet monitoring tool** called `pktmon` that can capture and analyze network traffic.

### **Steps to Capture and Analyze Network Packets:**
1. **Start Capturing All Network Traffic**
   ```cmd
   pktmon start --etw
   ```
   This command starts capturing network packets.

2. **Stop the Capture**
   ```cmd
   pktmon stop
   ```

3. **Convert the Capture File to Readable Format**
   ```cmd
   pktmon format PktMon.etl -o capture.txt
   ```
   This converts the captured **.etl** file into a human-readable **text format**.

4. **View the Traffic Report**
   ```cmd
   notepad capture.txt
   ```
   This opens the captured network data in **Notepad**.

---

## **Method 4: Using `Wireshark` for Advanced Network Analysis**
If you need a **GUI-based** detailed packet analysis, install **Wireshark** (free and open-source).

1. **Download Wireshark**: [https://www.wireshark.org/](https://www.wireshark.org/)
2. **Install and Run Wireshark**  
3. **Start Packet Capture** on the desired network interface (Wi-Fi, Ethernet, etc.).
4. **Analyze Packets** with filters like:
   ```
   tcp.port == 80
   ```
   (Filters HTTP traffic)

---

## **Conclusion**
- If you need **basic network traffic monitoring**, use `netstat` or `pktmon`.
- If you want **real-time monitoring with filtering**, use **PowerShell**.
- For **deep packet analysis**, use **Wireshark**.

Would you like a script that automates traffic analysis in CMD or PowerShell?
