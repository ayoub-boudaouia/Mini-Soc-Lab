# 🛡️ Mini SOC Lab — Cybersecurity Home Lab

> Projet réalisé dans le cadre de ma montée en compétences en cybersécurité.  
> Simulation d'un environnement d'attaque/défense sous Linux avec des outils professionnels.

---

## 📌 Objectif

Mettre en place un laboratoire virtuel simulant une infrastructure réelle, avec :
- Un serveur Linux vulnérable (cible)
- Une machine attaquante (Kali Linux)
- Des mécanismes de détection et de blocage automatique

---

## 🏗️ Architecture du Lab
```
┌─────────────────────────────────────────┐
│              Réseau virtuel             │
│                                         │
│  ┌─────────────────┐  ┌───────────────┐ │
│  │  Ubuntu Server  │  │  Kali Linux   │ │
│  │  192.168.1.28   │  │  192.168.1.29 │ │
│  │  - SSH (port 22)│  │  - Hydra      │ │
│  │  - Apache       │  │  - Nmap       │ │
│  │  - Fail2Ban     │  │               │ │
│  └─────────────────┘  └───────────────┘ │
└─────────────────────────────────────────┘
```

---

## 🛠️ Stack technique

| Outil | Rôle |
|---|---|
| VirtualBox | Hyperviseur pour les VMs |
| Ubuntu Server 24.04 | Serveur cible |
| Kali Linux 2025 | Machine attaquante |
| OpenSSH | Service cible de l'attaque |
| Apache2 | Serveur web exposé |
| Fail2Ban | Détection et blocage automatique |
| Hydra | Outil de brute force SSH |

---

## 📋 Étapes réalisées

### Phase 1 — Mise en place de l'environnement
- Installation et configuration de VirtualBox
- Déploiement d'Ubuntu Server 24.04 LTS
- Déploiement de Kali Linux 2025
- Configuration du réseau bridge
- Vérification de la connectivité (ping entre les deux machines)

### Phase 2 — Sécurisation du serveur
- Installation et démarrage du service SSH
- Installation d'Apache2
- Installation et configuration de Fail2Ban
- Configuration du jail SSH

### Phase 3 — Simulation d'attaque
- Brute force SSH depuis Kali avec **Hydra** sur la wordlist `rockyou.txt`
- Observation du blocage automatique par Fail2Ban après 3 tentatives

### Phase 4 — Analyse des logs
- Lecture des tentatives dans `/var/log/auth.log`
- Vérification du bannissement dans `/var/log/fail2ban.log`
- Confirmation de l'IP bannie via `fail2ban-client status sshd`

---

## 🔍 Résultats
```bash
sudo fail2ban-client status sshd

# Status for the jail: sshd
# |- Currently failed: 0
# |  Total failed: 24
# `- Currently banned: 1
#    Banned IP list: 192.168.1.29
```

**L'IP de Kali a été automatiquement bannie après 3 tentatives échouées.**

---

## 📚 Compétences développées

- Administration Linux (systemctl, journalctl, apt, nano)
- Gestion des services et des logs système
- Configuration de Fail2Ban
- Notions de réseau (IP, ports, SSH)
- Utilisation d'outils offensifs en environnement isolé (Hydra)
- Analyse de logs d'intrusion

---

## 🚀 Améliorations prévues

- [ ] Ajout d'Auditd pour logger toutes les commandes système
- [ ] Scan de ports avec Nmap depuis Kali
- [ ] Mise en place d'un SIEM léger (ELK Stack)

---

## ⚠️

Ce projet est réalisé dans un environnement **entièrement isolé** à des fins **éducatives uniquement**.  
Toute utilisation de ces techniques sur des systèmes sans autorisation explicite est illégale.
