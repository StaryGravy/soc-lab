# Home SOC / Network Monitoring Lab

A lightweight Security Operations Center (SOC) built on a Raspberry Pi 3B+.

## Author
Gerell Perrington

## Stack
- **Suricata 7.0.70** - Network IDS/IPS with 66,00+ Emerging Threats rules
- **Loki** - Log aggregation and storage 
- **Promtail** - Log shipping agent
- **Grafana** - Real-time dashboard and visulization

## Architecture
Network traffic -> Suricata (detection) -> eve.json -> Promtail -> Loki -> Grafana dashboard

## Hardware
- Raspberry Pi 3B+ (1GB RAM)
- Raspberry Pi OS Bookworm (64 - bit) Lite

## Setup
See install steps in SETUP.md


 
