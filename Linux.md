https://www.linuxvmimages.com/
To bypass these Windows 11 setup blocks, you need to handle two issues at once: your PC is missing TPM 2.0, and the installation media is currently blocked because you are running it from inside Audit Mode (Modo de Auditoria).
Because Microsoft blocks in-place upgrades while in Audit Mode, you cannot run the setup file directly from your current desktop screen. Instead, you must perform a clean installation by booting from your installation media (like a USB drive).
Here is how to clear both blocks and successfully install Windows:

Step 1: Exit Audit Mode and Boot from USB

1. Press Windows Key + R, type sysprep and hit Enter.
2. In the Sysprep tool window that opens, change the System Cleanup Action to Enter System Out-of-Box Experience (OOBE).
3. Set the Shutdown Options to Shutdown or Restart, then click OK.
4. Connect your Windows 11 installation USB flash drive to the PC.
5. Turn on the PC and immediately press your motherboard's boot menu key (usually F12, F11, F8, or F2 depending on the brand) to force the computer to boot directly from the USB drive rather than your normal desktop hard drive.

Step 2: Bypass the TPM 2.0 Check During Setup

Once your PC loads the Windows installation environment from the USB, you can use a registry modification to entirely skip the hardware checks:
1. Advance through the initial language selection screen until you see the Install Now button.
2. On that screen, press Shift + F10 on your keyboard to open the Command Prompt terminal.
3. Type regedit and press Enter to open the Registry Editor.
4. In the left panel, navigate to this path:
HKEY_LOCAL_MACHINE\SYSTEM\Setup
5. Right-click on the Setup folder, hover over New, and choose Key. Name this new folder LabConfig.
6. Click on your newly created LabConfig folder. Right-click in the empty space on the right side, select New → DWORD (32-bit) Value.
7. Name the value BypassTPMCheck. Double-click it, change its Value data to 1, and click OK.
8. (Optional) If your machine also lacks a supported CPU or Secure Boot, repeat the process to create two more DWORD (32-bit) values within the same folder:
	• BypassSecureBootCheck (Set value to 1)
	• BypassCPUCheck (Set value to 1)
9. Close both the Registry Editor and the Command Prompt windows.
Click Install Now to proceed. The installer will skip the hardware compatibility block and complete the installation flawlessly.
If you run into any trouble during these steps, please let me know:
• Your computer or motherboard brand (to help find your boot menu key)
• If you are attempting to keep your existing files or if you want to wipe the drive for a completely clean install
