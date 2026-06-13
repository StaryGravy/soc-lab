# SOC Lab Setup Guide

## Hardware Requirements
- Raspberry Pi 3B+
- MicroSD card (16GB+)
- Network connection (WiFi or Ethernet)

## Step 1 - Flash Raspberry Pi OS
1. Download Raspberry Pi Imager from raspberrypi.com/software
2. Select Rapberry Pi OS lite (64-bit)
3. In setting enables SSH, set username to 'pi', set a password
4. Flash to microSD card and boot the Pi

## Step 2 - Connect via SSH
'''bash
ssh pi@
'''

## Step 3 - Update the System
'''bash
sudo apt update && sudo apt upgrade -y
'''

## Step 4 - Install Suricata
''bash
sudo apt install suricata -y
sudo nano /etc/suricata/suricata.yaml # change eth0 to wlan0
sudo suricata-update
sudo systemctl enable suricata
sudo systemctl start suricata
'''

## Step 5 - Install Grafana
''bash
sudo apt install  -y apt-transport-https wget
wget -q -O /tmp/grafana.key https://packages.grafana.com/gpg.key
sudo gpg --dearmor -o /etc/apt/keyrings/grafana.key
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt update
sudo apt install grafana -y
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
,,,

## Step 6 - Install Loki and Promtail
,,,bash
sudo apt install loki promtail -y
sudo systemctl enable loki promtail
sudo systemctl start loki promtail
'''

## Step 7 - Configure Promtail
Edit /etc/promtail/config.yml and set the path to:
'/var/log/suricata/eve.json'

## Step 8 - Connect Loki to Grafana
1. Open Grafana at http://<your-pi-ip>:3000
2. Go to Connections > Data Sources > Add data source
3. Select Loki, set URL to http://localhost:3100
4. Click Save & Test

## Step 9 - Create Dashboard
1. Go to Dashboards > New Dashboard
2. Add a Logs panel with query: '{job="suricata"}'
3. Save as "Home SOC Dashboard"
