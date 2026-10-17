# Vector Syslog to Azure Data Explorer (ADX) for Unraid

[![Unraid App Template](https://img.shields.io/badge/Unraid-App%20Template-orange.svg)](https://unraid.net/)
[![Vector Version](https://img.shields.io/badge/Vector-latest--alpine-blue.svg)](https://vector.dev/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A high-performance, containerized log collector stack powered by [Vector](https://vector.dev/). This template listens on port `514` for local **UDP** and **TCP** Syslog traffic (from firewalls, routers, switches, and smart home hubs) and streams structured JSON events directly to an **Azure Data Explorer (ADX)** Free Cluster using Microsoft Entra ID (Service Principal) authentication.

---

## Features

- **Zero Local Database Overhead:** Ships telemetry straight to cloud Kusto storage for fast KQL queries.
- **Dual-Protocol Ingestion:** Listens natively on both UDP and TCP port 514.
- **Automatic Configuration Setup:** Automatically downloads the default `vector.json` config from GitHub on first boot if missing.
- **Unraid UI Parameterization:** ADX cluster endpoints, database names, table schemas, and batching parameters are fully configurable directly within the Unraid container WebUI.
- **Outage Resilience:** Built-in disk buffering on Unraid appdata storage to queue logs during local network or internet outages.

---

## Prerequisites

1. **Free Azure Data Explorer (Kusto) Cluster:**
   - Create a 100% free perpetual cluster at [aka.ms/kustofree](https://aka.ms/kustofree).
   - Create a database (e.g., `HomeTelemetry`) and a target table (e.g., `Syslogs`).

2. **Azure Entra ID App Registration:**
   - Go to **Azure Portal** > **Microsoft Entra ID** > **App registrations** and create a new registration.
   - Generate a **Client Secret** under *Certificates & secrets*.
   - Grant the App Registration access to your Kusto database by running this KQL command in your ADX WebUI:
     ```kusto
     .add database HomeTelemetry ingestors ('aadapp=<YOUR_CLIENT_ID>;<YOUR_TENANT_ID>')
     ```

---

## Installation on Unraid

### Option 1: Community Applications (App Store)
Search for **Vector Syslog ADX** in the Unraid Community Applications store and click **Install**.

### Option 2: Manual Template Installation
Run this command in the Unraid Terminal to download the container template directly into your local user templates directory:

```bash
curl -sSL [https://raw.githubusercontent.com/DataBitz/unraid-vector-syslog-adx/main/vector-syslog.xml](https://raw.githubusercontent.com/DataBitz/unraid-vector-syslog-adx/main/vector-syslog.xml) -o /boot/config/plugins/dockerMan/templates-user/vector-syslog.xml
