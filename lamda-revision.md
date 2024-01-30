To facilitate a clear understanding and application of the setup and update procedures for the Screamer board, this document outlines step-by-step instructions accompanied by a batch script for Windows users. The document is structured into two main sections: "Getting Started with Screamer" for initial setup and "Upgrading Screamer Gateware" for updating the device's firmware.

### Getting Started with Screamer

1. **Disable IOMMU in BIOS Settings**
   - Restart the target system and enter the BIOS setup.
   - Navigate to the settings related to IOMMU and set it to "Disabled."

2. **Connect the Screamer Board**
   - Turn off the target computer.
   - Insert the Screamer board into an available PCIe or M.2 slot, depending on your model. Use the provided adapter if necessary for M.2 connection.

3. **Boot the Target System**
   - Power on the target system. The Screamer will also power up using the PCIe/M.2 connection.
   - Ensure the "Prog Done" LED (LD3) on the Screamer board turns green, indicating successful boot.

4. **Connect Screamer to Control Computer**
   - Use a USB-C or USB 3 cable to connect the Screamer to your control computer.
   - If necessary, use the provided adapter for USB-C to USB 3.1 Type-A.

5. **Run PCILeech**
   - Install PCILeech on the control computer by following the instructions at [PCILeech GitHub](https://github.com/ufrisk/pcileech).
   - Execute the following command in a terminal or command prompt:
     ```
     sudo ./pcileech probe -device fpga -v
     ```
   - Confirm successful connection and memory probing.

### Upgrading Screamer Gateware

1. **Power the Screamer**
   - Ensure the Screamer is powered via the PCIe/M.2 connection.

2. **Connect the JTAG Cable**
   - Connect the JTAG cable between the Screamer and your computer. For the Squirrel version, use the Update Port.

3. **Prepare the Tools**
   - Download and extract the precompiled OpenOCD archive suitable for your operating system.
   - Download and unzip the flashing scripts (`flash_screamer.zip`).

4. **Download the New Gateware**
   - Obtain the appropriate gateware file from the PCILeech GitHub and place it in the `flash_screamer` directory.

5. **Execute the Flashing Script**
   - Open a command prompt or terminal in the `flash_screamer` directory.
   - For Windows, adjust the command to point to the `openocd.exe` location and select the correct configuration file based on your Screamer version. Execute the command:
     ```
     ..\openocd\bin\openocd.exe -f flash_screamer_[version].cfg
     ```
   - For Linux, use a similar approach with the `openocd` command.

### Batch Script for Windows Users

To automate the gateware update process on Windows, you can use the following batch script. Save it as `update_screamer.bat` in the same directory where you have the `openocd` and `flash_screamer` folders.

```batch
@echo off
cd flash_screamer
set /p version="Enter your Screamer version (squirrel/r03_r04): "
..\openocd\bin\openocd.exe -f flash_screamer_%version%.cfg
echo Your Screamer board has been updated. Press any key to exit.
pause > nul
```

To run the script, double-click `update_screamer.bat` and follow the on-screen instructions.

