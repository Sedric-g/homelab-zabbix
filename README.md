# homelab-zabbix

![Zabbix](https://img.shields.io/badge/Zabbix-7.0_LTS-D40000?style=flat-square&logo=zabbix&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-11-F46800?style=flat-square&logo=grafana&logoColor=white)
![Docker](https://img.shields.io/badge/Docker_Compose-2496ED?style=flat-square&logo=docker&logoColor=white)

**FR** · Lab de supervision : Zabbix 7.0 LTS (PostgreSQL) + Grafana, déployé avec Docker Compose. Il sert à tester la surveillance d'hôtes Linux/Windows et d'équipements réseau (SNMP), les déclencheurs et les tableaux de bord.

**EN** · Monitoring lab: Zabbix 7.0 LTS (PostgreSQL) + Grafana, deployed with Docker Compose. Used to practise monitoring Linux/Windows hosts and network devices (SNMP), triggers and dashboards.

## Architecture

```text
             ┌──────────────┐      ┌──────────────┐
  :8080 ───▶ │  zabbix-web  │      │   grafana    │ ◀─── :3000
             └──────┬───────┘      └──────┬───────┘
                    │                     │ (Zabbix plugin / API)
             ┌──────▼───────┐             │
  :10051 ──▶ │zabbix-server │ ◀───────────┘
             └──┬────────┬──┘
                │        │
        ┌───────▼──┐  ┌──▼───────────┐
        │ postgres │  │ zabbix-agent2│
        └──────────┘  └──────────────┘
```

## Démarrage · Quick start

```bash
git clone https://github.com/Sedric-g/homelab-zabbix.git
cd homelab-zabbix
cp .env.example .env      # changez les mots de passe · change the passwords
docker compose up -d
```

| Service | URL | Identifiants par défaut · Default login |
|---|---|---|
| Zabbix | http://localhost:8080 | `Admin` / `zabbix` (à changer · change it) |
| Grafana | http://localhost:3000 | `admin` / valeur de `GRAFANA_ADMIN_PASSWORD` |

### Relier Grafana à Zabbix · Connect Grafana to Zabbix

1. Grafana → *Administration → Plugins* → activer **Zabbix**.
2. *Connections → Data sources → Zabbix* → URL : `http://zabbix-web:8080/api_jsonrpc.php`.
3. Identifiants Zabbix → *Save & test*.

## Feuille de route · Roadmap

- [ ] Surveillance SNMP d'un switch/routeur (Cisco, Aruba) · SNMP monitoring of a switch/router
- [ ] Agent sur un serveur Windows (AD, DNS, DHCP) · Agent on a Windows Server
- [ ] Alertes par courriel / Teams · Email / Teams alerting
- [ ] Tableau de bord Grafana exporté en JSON · Exported Grafana dashboard (JSON)
- [ ] Captures d'écran · Screenshots

## Auteur · Author

**Sedrice Gounou** · Systems & Network Administrator · [sgbtech.ca](https://sgbtech.ca)
