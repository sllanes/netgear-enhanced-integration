# Enhanced Netgear Integration for Home Assistant

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)

Enhanced Netgear integration for Home Assistant which adds sensors and switches for Netgear routers.

_Based on previous work by [roblandry](https://github.com/roblandry/netgear-enhanced-integration) and [selfish](https://github.com/selfish/home-assistant-netgear-router-enhanced-integration)._

## Features:

### Switches:

|Friendly Name| Entity | States |
|---|---|---|
| Access Control |  |
| Traffic Meter |  | on/off |
| Parental Control | |
| QOS |
| 2.4g Guest WiFi | switch.ng_enhanced_2g_guest_wifi | on/off |
| 5g Guest WiFi | |
| Run Speed Test | (switch will always toggle to off) |
| Reboot Router | switch.ng_enhanced_reboot | auto-toggles to off |

### Sensors:

**The supported sensors are:**

`Firmware`, `App Firmware`, `Device Config`, `Access Control Status`, `Traffic Meter`, `Traffic Meter Enabled`, `Traffic Meter Opt`, `LAN Config`, `WAN Info`, `Parental Control Enabled`, `All MAC Addresses`, `DNS Masq`, `Info`, `Supported Features`, `Speed Test Result`, `QOS Enabled`, `Bandwidth Control`, `2G Guest Wifi`, `5G Guest Wifi`, `WPA Security Key`, `5G WPA Security Key`, `2G Info`, `5G Info`, `Channel`, `2G Guest Wifi Info`, `5G Guest Wifi Info`, `Smart Connect`

---

## Setup

_Note that you will need to restart Home Assistant after installation, whichever method is used._

### Option 1 - HACS (recommended!):

1. In HACS, go to Integrations, and then click the orange '+' button in the lower right corner to add an integration.
1. Search for "Netgear Enhanced" and install it.

### Option 2 - Manual:

1. Create a directory named `netgear_enhanced` under `custom_components`.
1. Copy the files from to the `netgear_enhanced` folder in this repository.

## Configurations:

- Use the following examples in your configuration file (typically `configuration.yaml`). Note that you may need to merge `switch` and `sensor` keys with existing ones.
- Make sure to modify the parameters to fit your needs. It's recommended to use secrets for all sensitive info.
- After making changes there may be some delay before entities are updated due to the router changing configuration.
- Different routers use different ports for authentication. If you know your router port is different from 5000, specify that, otherwise, ususally 5000 or 80 will work.
- Each configuration key is either required, or is not required because it uses a default value, which is mentioned below

### Default values:

| Config Value | Explanation | Required? (Default) |
|---|---|---|
| username | Router access username | Yes |
| password | Router access password | Yes |
| host | Router access URL/IP | No (Default: 192.168.1.1) |
| port | Router access port. This is typically 5000 or 80. | No (Default: 5000) |
| ssl | Should the integration access the router using SSL? (true/false) | No (Default: false) | 
| prefix | Entities created by the integration will use this as a prefix for their id | No (Default: ng_enhanced) |
| scan_interval | Interval between updates polling from the router | No (Default: 5 minutes) |
| resources | List of resources to use in Home Assistant. See examples below for full lists of available resources | Yes |   

### Actions / Switches:

```yaml
# Configuration.yaml:
switch:
  - platform: netgear_enhanced
    host: !secret my_secret_netgear_ip
    username: !secret my_secret_netgear_user
    password: !secret my_secret_netgear_pass
    resources:
      - 'access_control'
      - 'traffic_meter'
      - 'parental_control'
      - 'qos'
      - '2g_guest_wifi'
      - '5g_guest_wifi'
      - 'run_speed_test'
      - 'reboot'
```

### Sensors:

```yaml
# Configuration.yaml:
sensor:
  - platform: netgear_enhanced
    host: !secret my_secret_netgear_ip
    username: !secret my_secret_netgear_user
    password: !secret my_secret_netgear_pass
    resources:
      - firmware
      - check_app_fw
      - get_device_config_info
      - access_control_on
      - traffic_meter
      - traffic_meter_on
      - traffic_meter_options
      - get_lan_config_info
      - get_wan_ip_info
      - parental_control_on
      - mac_address
      - dns_masq
      - info
      - supported_features
      - speed_test_result
      - qos_enabled
      - bw_control
      - 2g_guest_wifi_on
      - 5g_guest_wifi_on
      - 2g_wpa_key
      - 5g_wpa_key
      - 2g_wifi_info
      - 5g_wifi_info
      - get_channel
      - 2g_guest_wifi_info
      - 5g_guest_wifi_info
      - get_smart_conn
```

### Supported routers:

- Netgear RAX80
- Netgear Orbi
- Netgear R7800
- Netgear R7500v2
- Netgear R7000
- Netgear R6900
- Netgear R6300
- Netgear R6250
- Netgear R6200
- Netgear R6100
- Netgear N300 - Model: C3000 (Port 80)
- Netgear Centria (WNDR4700, WND4720)
- Netgear WNDR4500
- Netgear WNDR4300
- Netgear WNDR4000
- Netgear WNDR3800
- Netgear WNDR3700v3
- Netgear WNDR3700v2
- Netgear WNDR3400v2
- Netgear WNR3500Lv2
- Netgear WNR2200
- Netgear WNR2000v3
- Netgear WNR2000v4 (Port 80)
- Netgear WNR1500
- Netgear WNR1000v2
- Netgear WNR1000v3
- Netgear WNDRMAC
- Netgear WNR612v2