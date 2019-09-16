# Troubleshooting

---

```
Stderr: VBoxManage.exe: error: VT-x is not available (VERR_VMX_NO_VMX)
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole
```
Enable Intel VT-x in your BIOS or UEFI.

---

```
<various error messages>
```
You need to disable Windows Hyper-V, which is only an issue where Hyper-V is running (Windows Professional or similar).

You can disable Hyper-V by executing `bcdedit /set hypervisorlaunchtype off` from an Administrator Command Prompt and rebooting.

You can verify your Hyper-V launch type setting by executing `bcdedit /enum`.
