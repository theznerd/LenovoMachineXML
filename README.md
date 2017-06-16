# LenovoMachineXML
```text
Replacement XML file for Lenovo driver catalog.
User contributed via fork and pull.

The Lenovo XML file is broken down into products. Each product has three attributes: Model, Family, and OS
  - Model: Name Identifier with no spaces - will be pulled by the SCConfigMgr Driver Download Tool
  - Family: tp (ThinkPad), tc (ThinkCenter)
  - OS: win10 (Windows 10), win732 (Windows 7 32-Bit), win764 (Windows 7 64-Bit), win81 (Windows 8.1)

Below each Product element, there are four (or more) potential additional elements Query, DriverPack, HardwareApps, and BIOSUpdate. 

Each Query element has a three elements below it: Types, Version, and Smbios.
  - Types (contains multiple Type elements): first 4 characters from "wmic path Win32_ComputerSystemProduct get Name" (like 10NE for M900)
  - Version: value from "wmic path Win32_ComputerSystemProduct get Version"  (like ThinkCentre M900)
  - Smbios: some unknown length of first few characters from "wmic path Win32_BIOS get SMBIOSBIOSVersion"

Each DriverPack element has an "id" attrubute.
 - "SCCM" (download page for SCCM driver pack)
 - "WinPE 10" (download page for WinPE driver pack)

Each BIOSUpdate element just contains a link to bios update download page

The HardwareApps element is broken down into individual "HardwareApp" elements (HardwareApp). The HardwareApp element has an attribute of Category: "Bluetooth","Hotkey","WAN" and the following elements:
  - Name: Friendly name for package
  - downloadURL: Link to download page
  - installCmd: install command for silent installation
  - tip: a hint for the product (maybe it only applies to a specific version, etc)

Below is an example product:
  <Product model="M600Tiny" family="tc" os="win10">
    <Queries>
      <Types>
        <Type>10G9</Type>
        <Type>10G8</Type>
      </Types>
      <Version>ThinkCentre M600</Version>
      <Smbios>M00</Smbios>
    </Queries>
    <DriverPack id="sccm">https://support.lenovo.com/downloads/ds105115</DriverPack>
    <DriverPack id="WinPE 10">https://support.lenovo.com/downloads/ds105415</DriverPack>
    <BIOSUpdate>http://support.lenovo.com/downloads/ds105487</BIOSUpdate>
    <HardwareApps>
      <HardwareApp category="Bluetooth">
        <name>Qualcomm Atheros Bluetooth Driver</name>
        <downloadURL>https://support.lenovo.com/downloads/ds104695</downloadURL>
        <installCmd>setup.exe /C:"install.exe /s /v/norestart" /t"c:\temp"</installCmd>
        <tip />
      </HardwareApp>
      <HardwareApp category="Bluetooth">
        <name>Intel 8260 Wireless Software for Bluetooth</name>
        <downloadURL>https://support.lenovo.com/downloads/ds105210</downloadURL>
        <installCmd>Setup.exe /qn /norestart</installCmd>
        <tip />
      </HardwareApp>
      <HardwareApp category="Bluetooth">
        <name>Intel 3165 Bluetooth Driver</name>
        <downloadURL>https://support.lenovo.com/downloads/ds105209</downloadURL>
        <installCmd>Setup.exe /qn /norestart</installCmd>
        <tip />
      </HardwareApp>
    </HardwareApps>
  </Product>
```
