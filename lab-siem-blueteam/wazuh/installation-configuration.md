# 🛡️ Installation et Configuration de Wazuh SIEM

## Environnement

| Composant | Valeur |
|---|---|
| OS | Ubuntu 24.04 LTS |
| IP | 192.168.56.101 |
| Version Wazuh | 4.14.4 |
| Type d'installation | All-in-one (Indexer + Manager + Dashboard) |

---

## 1. Installation via le script officiel Wazuh

### Téléchargement du script et du fichier de configuration

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
curl -sO https://packages.wazuh.com/4.14/config.yml
```

### Configuration des nœuds (config.yml)

```yaml
nodes:
  indexer:
    - name: node-1
      ip: "192.168.56.101"
  server:
    - name: wazuh-1
      ip: "192.168.56.101"
  dashboard:
    - name: dashboard
      ip: "192.168.56.101"
```

### Lancement de l'installation

```bash
sudo bash wazuh-install.sh -a
```

> ⚠️ À la fin de l'installation, noter absolument les credentials générés :
> - **URL** : https://192.168.56.101
> - **User** : admin
> - **Password** : (généré automatiquement)

---

## 2. Vérification des services

```bash
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-dashboard
```

Les trois services doivent être **active (running)**.

---

## 3. Installation des agents

### Commande de vérification des agents connectés

```bash
sudo /var/ossec/bin/agent_control -l
```

### Agents déployés

| ID | Nom | OS | Rôle |
|---|---|---|---|
| 000 | UbuntuJulien | Ubuntu 24.04 | Serveur SIEM (local) |
| 001 | debian-lab_siem | Debian 13 | Cible Linux |
| 002 | windowsServer_lab_siem | Windows Server 2025 | Contrôleur de domaine AD |
| 003 | windows_client_lab_siem | Windows 10 Pro | Poste client AD |

### Installation agent Linux (Debian)

```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.14.4-1_amd64.deb
sudo WAZUH_MANAGER='192.168.56.101' WAZUH_AGENT_NAME='debian-lab_siem' dpkg -i ./wazuh-agent_4.14.4-1_amd64.deb
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

### Installation agent Windows (PowerShell administrateur)

```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.4-1.msi -OutFile $env:tmp\wazuh-agent
msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='192.168.56.101' WAZUH_AGENT_NAME='windows-server_lab_siem'
NET START WazuhSvc
```

---

## 4. Architecture Wazuh

    ┌─────────────────────────────────────────────────┐
    │              Ubuntu 24.04 (SIEM)                │
    │                192.168.56.101                   │
    │                                                 │
    │  ┌─────────────┐  ┌──────────┐  ┌───────────┐  │
    │  │   Indexer   │  │ Manager  │  │ Dashboard │  │
    │  │ OpenSearch  │  │  :55000  │  │   :443    │  │
    │  │   :9200     │  └──────────┘  └───────────┘  │
    │  └─────────────┘                                │
    └─────────────────────────────────────────────────┘
             ▲              ▲              ▲
             │              │              │
        Debian13     WinServer2025    Win10Pro
       Agent:1514   Agent:1514      Agent:1514


---

## 5. Points de vigilance rencontrés

### Problème keystore Dashboard
Le Dashboard utilise un keystore chiffré pour stocker les credentials de connexion à l'Indexer. En cas de problème d'authentification :

```bash
# Mettre à jour les credentials dans le keystore
echo "kibanaserver" | sudo /usr/share/wazuh-dashboard/bin/opensearch-dashboards-keystore add opensearch.username --allow-root --stdin --force
echo "MOT_DE_PASSE" | sudo /usr/share/wazuh-dashboard/bin/opensearch-dashboards-keystore add opensearch.password --allow-root --stdin --force
sudo systemctl restart wazuh-dashboard
```

### Incompatibilité agent/manager sur la même machine
Il est impossible d'installer `wazuh-agent` sur la même machine que `wazuh-manager`. Le manager intègre nativement la supervision locale (ID 000).
