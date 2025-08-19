# Cowrie Honeypot + ELK Threat Intelligence Platform

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Architecture Overview](#architecture-overview)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Usage](#usage)
- [Directory Structure](#directory-structure)
- [Contributing](#contributing)
- [Security & Ethics](#security--ethics)
- [Incoming Updates](#incoming-updates)
- [License](#license)

---

## Project Overview
This project integrates the Cowrie SSH/Telnet honeypot with the ELK (Elasticsearch, Logstash, Kibana) stack to provide a robust platform for collecting, enriching, analyzing, and visualizing malicious activity. It is designed for security research, threat intelligence, and hands-on learning in cyber defense.

## Features
- Automated log collection from Cowrie honeypot
- Log enrichment with GeoIP, ASN, and threat intelligence sources (e.g., AbuseIPDB)
- Custom enrichment scripts for advanced analysis
- Pre-built and custom Kibana dashboards for threat hunting and reporting
- Modular pipeline for adding new enrichment or log sources
- Docker Compose for easy deployment
- Secure and ethical deployment guidelines

## Architecture Overview
The platform consists of the following components:
- **Cowrie**: Captures attacker interactions and logs them in JSON format
- **Logstash**: Parses, enriches, and forwards logs
- **Elasticsearch**: Stores and indexes enriched events
- **Kibana**: Visualizes and analyzes data
- **Enrichment Scripts**: Python scripts for additional threat intelligence and data processing

Logs flow from Cowrie to Logstash, where they are enriched and indexed in Elasticsearch. Kibana provides dashboards and search capabilities for analysis.

## Getting Started
### Prerequisites
- Docker & Docker Compose
- Python 3.8+
- (Optional) Elasticsearch and Kibana if running outside Docker

### Cowrie Setup
To set up Cowrie, please follow the official documentation: https://cowrie.readthedocs.io/en/latest/

### GeoIP Database
You must manually download the GeoLite2 City database from MaxMind (https://dev.maxmind.com/geoip/geolite2-free-geolocation-data) and place it in the appropriate location (e.g., `logstash/geoip/GeoLite2-City.mmdb`).

### AbuseIPDB API Key
For log enrichment with AbuseIPDB, you need to obtain a free API key from https://www.abuseipdb.com/ and add it to your environment or configuration as required by the enrichment scripts and Logstash pipeline.

### Quickstart
1. Clone this repository
2. Copy and edit configuration files as needed
3. Run `docker-compose up -d` to start the stack
4. Access Kibana at `http://localhost:5601`

### Manual Setup
Instructions for manual installation will be updated soon.

## Configuration
- **Cowrie**: Configure in `cowrie_template.json` and `cowrie_logs/`
- **Logstash**: Pipeline in `logstash/pipeline/logstash.conf`, GeoIP DB in `logstash/geoip/`
- **Enrichment Scripts**: Settings in `scripts/` and environment variables
- **Docker Compose**: Services and volumes in `docker-compose.yml`

## Usage
- Start/stop the stack with Docker Compose
- View and analyze logs in Kibana
- Run enrichment scripts as needed (see `scripts/`)
- Add new log sources or enrichments by updating Logstash config and scripts

## Directory Structure
- `cowrie_logs/` — Raw Cowrie logs
- `enriched_logs/` — Enriched log output
- `logstash/` — Logstash pipeline and GeoIP data
- `scripts/` — Python enrichment and utility scripts
- `docker-compose.yml` — Container orchestration
- `requirements.txt` — Python dependencies

## Contributing
Contributions are welcome! Please open issues or pull requests for bug fixes, new features, or documentation improvements. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines (if available).

## Security & Ethics
- Deploy in a controlled, isolated environment
- Do not use for unauthorized monitoring or entrapment
- Outbound connections from the honeypot are restricted
- Review and comply with all applicable laws and policies

## Incoming Updates
A Terraform script to codify the honeypot and supporting infrastructure as code (IaC) will be released soon. This will enable automated, reproducible deployments in cloud or on-prem environments.

## License
This project is licensed under the MIT License. See the full license text in the [LICENSE](./LICENSE) file or read the [MIT License](https://opensource.org/licenses/MIT) online.


