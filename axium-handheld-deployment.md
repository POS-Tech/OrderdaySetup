# Axium Handheld Deployment Guide

## Overview
This guide covers the complete process for deploying Axium handheld devices for Aloha OrderPay, from estate manager configuration through final payment verification.

---

## Prerequisites
- Access to Ingenico Estate Manager
- Axium handheld devices with charging bases
- Charging bases connected to POS network via ethernet
- Access to Aloha OrderPay configuration program
- WiFi credentials for POS network

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

## Part 4: Verification and Testing

### 4.1 Test Payment Processing
1. At the sign-in screen, tap the three lines (☰) in the top left corner
2. Select "Test Payments"
3. Verify the payment lane shows as open

### 4.2 Troubleshooting Payment Issues
If the payment lane does not show as open:
- Contact the Connected Payments team for assistance
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
