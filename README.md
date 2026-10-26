# 🔗 MikroTik Site-to-Site VPN (Hub & Spoke)

A production-ready template for connecting **multiple branch offices** to a **central HQ** using MikroTik RouterOS over IPsec Site-to-Site VPN, with OSPF dynamic routing and automatic failover.

![Topology](assets/topology.png)

## 🎯 Problem

An organization has 1 HQ and 3 branches. Each branch needs secure, always-on access to HQ resources (file server, ERP, VoIP) over the public internet, without exposing services directly.

## ✅ Solution

- **IPsec IKEv2** Site-to-Site tunnels from each branch → HQ
- **OSPF** for dynamic route exchange (HQ as ABR)
- **Dual WAN failover** on HQ (primary fiber + backup LTE)
- **VLAN segmentation** at each site (Users / VoIP / Guest)
- **Firewall** rules enforcing least-privilege access

## 🗺️ Topology
┌──────────────────┐
│ HQ │
│ MikroTik CCR │
│ 10.0.0.1/24 │
│ WAN1 + WAN2 │
└────────┬─────────┘
│ IPsec
┌───────────────────┼───────────────────┐
│ │ │
┌─────┴─────┐ ┌─────┴─────┐ ┌─────┴─────┐
│ Branch A │ │ Branch B │ │ Branch C │
│ 10.1.0.1 │ │ 10.2.0.1 │ │ 10.3.0.1 │
└───────────┘ └───────────┘ └───────────┘
