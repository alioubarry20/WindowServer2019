# TP Réseau — Configuration Windows Server 2019 : DHCP & DNS

**Nom :** Aliou Barry  
**Classe :** B2

---

## 1. Introduction

L'objectif de ce TP était de mettre en place un serveur DHCP et DNS sur Windows Server 2019, ainsi qu'un client Windows 10 configuré pour recevoir automatiquement une adresse IP et résoudre les noms de domaine.

Ce TP permet de comprendre le fonctionnement de l'adressage automatique et de la résolution de noms dans un réseau local.

---

## 2. Configuration initiale du serveur

Le serveur Windows Server 2019 a été configuré avec une adresse IP statique pour assurer la stabilité des services réseau.

**Configuration IPv4 :**

| Paramètre | Valeur |
|-----------|--------|
| Adresse IP | `192.168.10.10` |
| Masque | `255.255.255.0` |
| Passerelle | `192.168.1.254` |
| Serveur DNS | `192.168.10.10` |

---

## 3. Configuration du rôle DHCP

Le rôle DHCP a été installé via le Gestionnaire de serveur.

### Étendue DHCP

| Paramètre | Valeur |
|-----------|--------|
| Nom | `Etendue_Labo` |
| Plage d'adresses | `192.168.10.10` → `192.168.10.100` |
| Exclusion 1 | `192.168.10.10` (serveur) |
| Exclusion 2 | `192.168.10.254` (passerelle) |

---

## 4. Configuration du rôle DNS

### Zone de recherche directe

- Nom de la zone : `supdeco.com`

### Enregistrements DNS

| Type | Nom | Valeur |
|------|-----|--------|
| A | `srv` | `192.168.1.1` |
| CNAME | `www` | `srv.supdeco.com` |
| CNAME | `mail` | `srv.supdeco.com` |

---

## 5. Tests côté client

Le client Windows 10 est configuré en adressage automatique (DHCP).

### Tests réalisés

```cmd
ipconfig /all
```
→ Le client reçoit l'adresse `192.168.10.10`

```cmd
ping 192.168.10.10
```
→ Connectivité OK — 4 paquets envoyés, 0 perdus

```cmd
nslookup srv.supdeco.com
nslookup www.supdeco.com
nslookup mail.supdeco.com
```
→ Tous les noms se résolvent vers `192.168.10.10`

---

## 6. Conclusion

Ce TP a permis de mettre en place un serveur DHCP et DNS fonctionnel sous Windows Server 2019. Le client reçoit automatiquement son adresse IP et peut résoudre les noms de domaine configurés. La communication entre le serveur et le client est opérationnelle.

---

## Environnement

| Élément | Détail |
|---------|--------|
| Serveur | Windows Server 2019 |
| Client | Windows 10 |
| Réseau | `192.168.10.0/24` |
| Domaine DNS | `supdeco.com` |
