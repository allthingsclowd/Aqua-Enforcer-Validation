## How-To Guide: Verifying Aqua Enforcer Installation for Beginners


### **Update 24/4/24 - Customer Service Architect Recommendations (what's used in reality)**

1. **Check for Enforcer Process**:
   - Use the following command to check for running Aqua Enforcer process
  
     ```bash
     ps -ef | grep -i "slkd" | grep -v grep && echo "True" || echo "False"

     ```
2. **Check for Enforcer Installation on Host**:
   - the presence of this non-empty folder `/opt/aquasec` on the host would shows that an enforcer was running at some point (it may be stopped but not uninstalled)
  
     ```bash
     [ -d "/opt/aquasec" ] && [ "$(ls -A /opt/aquasec)" ] && echo "True" || echo "False"

     ```

### **Update 24/4/24 - Customer Service Architect Recommendations End**




Welcome to this beginner-friendly guide on verifying the presence and operational status of the Aqua Enforcer in Windows, Linux, and Kubernetes environments. If you're new to Aqua Security, this guide will help you use simple command-line instructions to check whether the Aqua Enforcer is installed and running correctly.

### **Windows Verification**

First, ensure you have administrative rights on your Windows machine as you will need them to execute the following commands.

#### **Verification Steps**

1. **Open Command Prompt as Administrator**:
   - Search for `cmd` in the Start menu, right-click on Command Prompt, and select "Run as administrator".

2. **Check for Aqua Enforcer Service**:
   - Run the command below to determine if the Aqua Enforcer service is running.
     ```cmd
     sc query | findstr /i "Aqua" && echo true || echo false
     ```

3. **Check for Running Processes**:
   - To verify if any Aqua Enforcer processes are active, use:
     ```cmd
     tasklist | findstr "Aqua" && echo true || echo false
     ```

### **Linux Verification**

You'll need root or sudo privileges to perform these checks on a Linux system.

#### **Verification Steps**

1. **Open Terminal**:
   - Access your terminal via your Linux desktop or SSH if you are connecting remotely.

2. **Service Status**:
   - Check if the Aqua Enforcer service is active with the following command:
     ```bash
     systemctl is-active --quiet aqua-enforcer.service && echo true || echo false
     ```

3. **Aqua-Specific Directories**:
   - Verify the presence of the installation directories:
     ```bash
     [ -d /opt/aqua-runc/ ] && echo true || echo false
     [ -d /opt/aquasec/ ] && echo true || echo false
     ```

4. **Running Processes**:
   - Determine if any processes related to Aqua are running:
     ```bash
     pgrep -f aqua && echo true || echo false
     ```

5. **System Logs**:
   - Check for the existence of the system log file:
     ```bash
     [ -f /opt/aquasec/tmp/aquasec.log ] && echo true || echo false
     ```
![image](https://github.com/allthingsclowd/Aqua-Enforcer-Validation/assets/9472095/b96348c3-e42c-4f28-832e-8c70ecb03779)


### **Kubernetes Verification**

Ensure you have `kubectl` configured with the appropriate context to manage your Kubernetes cluster.

#### **Verification Steps**

1. **List Aqua Pods**:
   - Use the following command to check for running Aqua Enforcer pods:
     ```bash
     kubectl get pods -n aqua -l app=aqua-enforcer --no-headers | grep -q . && echo true || echo false
     ```

### **Conclusion**

This guide provides the basic steps for verifying the installation of the Aqua Enforcer across different environments using simple command-line commands. Each command returns 'true' if the expected condition is met and 'false' if it is not, making it easy for beginners to understand and confirm the setup of their Aqua Security deployment.

Always refer to [the official AquaSecurity documentation](https://docs.aquasec.com/saas/) for the most up to date information

