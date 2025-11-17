# Axium Handheld Deployment Guide
**Revision: November 17, 2025**

## Overview
This guide covers the complete process for deploying Axium handheld devices for Aloha OrderPay, from estate manager configuration through final payment verification.

---

## Prerequisites

### System Requirements
- Access to Ingenico Estate Manager
- Axium handheld devices with charging bases
- Charging bases connected to POS network via ethernet
- Access to Aloha OrderPay configuration program
- WiFi credentials for POS network

### Location Configuration Requirements
**Connected Payments Setup**
- Location must be fully configured with Connected Payments before beginning
- Company Number and Store Number must exist in the ServerEPS portal
- Without this setup, you will not be able to add Axiums to the system

**Configuration Center (Not New Aloha Manager)**
- Location must be using Configuration Center for management
- New Aloha Manager is NOT compatible with this setup
- Configuration Center is required for BSL (Business Service Layer) support needed for digital receipts

**Interface Server Requirements**
- **Locations WITH Aloha Takeout or Online Ordering**: Requires a separate dedicated server to act as the interface server
- **Locations WITHOUT Aloha Takeout or Online Ordering**: Can use the Aloha Server as the interface terminal
- **Server Hardware**: Must be a NorTech server - NCR-provided servers will not be fast enough to handle the additional load from OrderPay handhelds

**Note**: The interface server will be configured as device number 70 in the OrderPay configurator.

---

## Part 1: Estate Manager Configuration

### 1.1 Access Estate Manager
Navigate to: https://estate-manager-nar02.icloud.ingenico.com/

### 1.2 Create Estate (New Locations Only)
For new locations, create a new estate with the following naming convention:
- **Signature**: Use the hasp key
- **Name**: `[hasp key number]_[Site name]`

### 1.3 Add Terminals to Estate
1. Hover over the estate name
2. Click the ellipses (⋯) menu
3. Select "Add Terminal"
4. Configure the terminal:
   - **Signature**: Device serial number (S/N)
   - **Name**: Device serial number (S/N)
   - **Type**: Axium
   - **Other settings**: Leave as default
5. Repeat for all handheld devices at the location

---

## Part 2: Axium Device Setup

### 2.1 Access Android Settings
1. Open Android Settings on the Axium
2. Enter password: `350000` (default password)

### 2.2 Configure Network Connection

**Option A: Standard WiFi Connection**
1. Navigate to Network Settings
2. Connect to the POS WiFi network

**Option B: Charging Base WiFi**
1. Open Settings menu
2. Select "Base"
3. Tap the QR code scan icon (top right corner)
4. Scan the QR code on the bottom of the charging base
5. Device will automatically link to the charging base WiFi

**Note**: Ensure the charging base is connected to the POS network via ethernet cable before proceeding.

### 2.3 Uninstall Existing Apps
To ensure clean installation of latest versions, uninstall the following apps from Apps Settings:
- Aloha OrderPay
- Aloha OrderPay CCApp
- Titan Custom Parameters

**Important**: Apps must be uninstalled for the update installation to work properly.

### 2.4 Update System Software
1. Long press the power button to open the admin panel
2. Select "Services"
3. Click "TEM Call"
4. Click "Check for Updates"
5. Install updates when prompted
6. Restart the Axium

### 2.5 Launch Aloha OrderPay
After the device reboots, open the Aloha OrderPay application.

---

## Part 3: Device Pairing and Configuration

### 3.1 Configure Devices in OrderPay Configurator
1. Open the Aloha OrderPay configuration program
2. Create device entries for each handheld
3. Use the following device numbering convention:
   - **Handhelds**: Start at device number 71
   - **Interface Server**: Device number 70
4. Generate QR codes for each handheld device

### 3.2 Pair Handheld Devices
1. On the handheld, tap the three lines (☰) in the top left corner
2. Select "Pair Device"
3. Scan the QR code from the configurator for this specific handheld
4. Wait for pairing to complete

### 3.3 Sign In to Aloha OrderPay
Use the employee's standard Aloha number (same as used at traditional terminals).

---

## Part 4: Connected Payments API Configuration

### 4.1 Configure Lanes in ServerEPS
1. Log in to https://hspclient.servereps.com/ServerEPS/Login.aspx
2. Navigate to the store location
3. Add new lanes for each Axium handheld:
   - For 4 handhelds, add lanes: 71, 72, 73, 74
   - Lane profile: Select any existing profile (specific profiles will be configured later)
4. Gather the following information from the portal:
   - Company Number
   - Company Name
   - Store Name
   - Store Number

### 4.2 Request API Credentials
Email **ConnectedPayments.Support@ncrvoyix.com** with the following information:

```
Company Number: [from portal]
Company Name: [from portal]
Store Name: [from portal]
Store Number: [from portal]
Lane Number(s): 71, 72, 73, 74 (etc.)
Serial Number(s) of Axiums: [S/N from devices]
```

They will send you two files via the NCR Large File Transfer website:
- `Client-API.txt`
- `Client-API-Secret.txt`

### 4.3 Encrypt API Credentials
1. Navigate to `bootdrv/atg/tools/`
2. Run `ATGConfigPasswords.exe`
3. For each API file:
   - Paste the contents into the password field
   - Select "Key1"
   - Generate the encrypted password
   - Save the encrypted output for the next step

### 4.4 Configure Custom Settings in Configuration Center
Navigate to Custom Settings and add the following five items:

| Item Name | Value | Notes |
|-----------|-------|-------|
| ClientKey | [Encrypted password from Client-API.txt] | Use Key1 encryption |
| ClientSecret | [Encrypted password from Client-API-Secret.txt] | Use Key1 encryption |
| TRANSACTIONHOSTADDRESS1 | hspwebeps.servereps.com | Static value |
| TRANSACTIONHOSTADDRESS2 | hspwebeps.servereps.com | Static value |
| CONFIGHOSTADDRESS | hspsvc1.servereps.com | Static value |

### 4.5 Apply Configuration Changes
1. Refresh Configuration Center
2. Reboot all Axium handhelds

---

## Part 5: Verification and Testing

### 5.1 Test Payment Processing
1. Open Aloha OrderPay on the Axium handheld
2. Tap the three lines (☰) in the top left corner
3. Select "Test Payments"
4. Verify the lane status at the bottom shows as **"Idle"**

### 5.2 Troubleshooting Payment Issues
If the payment lane does not show as "Idle", verify the following:

**Configuration Checklist:**
- ✓ Lanes are correctly configured in ServerEPS (hspclient.servereps.com)
- ✓ Lane numbers match between ServerEPS and OrderPay configurator
- ✓ ClientKey and ClientSecret are properly encrypted and entered in Custom Settings
- ✓ All three host addresses are correctly entered in Custom Settings
- ✓ Configuration Center has been refreshed
- ✓ Axium handhelds have been rebooted after configuration changes

**If issues persist:**
- Contact the Connected Payments team (ConnectedPayments.Support@ncrvoyix.com)
- Verify network connectivity
- Confirm charging base ethernet connection

---

## Quick Reference

### Device Numbering Convention
- Interface Server: 70
- Handhelds: 71, 72, 73, etc.

### Default Credentials
- Android Settings Password: `350000`
- OrderPay Login: Standard Aloha employee number

### Required Uninstalls
- Aloha OrderPay
- Aloha OrderPay CCApp
- Titan Custom Parameters

---

## Notes
- All handhelds must be added to Estate Manager before device setup
- Charging bases must have active ethernet connection to POS network
- Apps must be uninstalled before updates will install properly
- Device pairing QR codes are unique to each handheld

---

**Last Updated**: November 2025