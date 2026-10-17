# unraid-vector-syslog-adx
Vector Syslog to Azure Data Explorer (ADX) - Unraid App Template

A high-performance, containerized log collector stack powered by Vector. Listens on port 514 for local UDP and TCP Syslog traffic (from firewalls, routers, switches, and smart home hubs) and streams structured JSON events to an Azure Data Explorer Free Cluster using Microsoft Entra ID (Service Principal) authentication.

Key Features:

Zero Local DB Overhead: Ships logs directly to cloud Kusto storage for fast KQL queries.

Dual Protocol Support: Listens on both UDP and TCP port 514 natively.

Fully Configurable via Environment Variables: ADX endpoints, database names, table schemas, and batch settings are managed directly in the Unraid WebUI.

Built-in Resilience: Supports disk buffering on Unraid appdata to queue logs safely during internet outages.
