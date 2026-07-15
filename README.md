<h1 align="center">Générateur de règles iptables</h1>

<p align="center">
  <em>Décrivez un flux réseau (source, destination, service) et obtenez les règles iptables cohérentes, aller + retour, prêtes à coller.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/iptables-EE0000?style=flat&logo=linux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Bash-4EAA25?style=flat&logo=gnubash&logoColor=white"/>
  <img src="https://img.shields.io/badge/Type-Outil_web_HTML-lightgrey?style=flat&logo=html5&logoColor=white"/>
</p>

---

## En bref

Outil web autonome (fichier `.html`) qui aide à écrire un **pare-feu Linux propre et documenté** sans erreur de syntaxe. Vous renseignez les zones, les interfaces et le service à autoriser : l'outil génère les règles `iptables` correspondantes (le flux aller **et** son retour), prêtes à être copiées ou téléchargées en `.sh`.

L'outil part du principe d'une **politique par défaut `DROP`** : on ajoute donc uniquement les `ACCEPT` nécessaires, dans une logique de moindre exposition.

## Fonctionnalités

- **Catalogue de services courants** pré-remplissant protocole + port : SSH, HTTP/HTTPS, DNS, DHCP, FTP, SMTP, IMAP(S), POP3, LDAP(S), Kerberos, SMB, RDP, MySQL/MariaDB, SNMP, NTP, SIP, ICMP… ou un service **personnalisé**.
- **Type de trafic** : `FORWARD` (routé entre zones), `INPUT` (vers le pare-feu) ou `OUTPUT` (depuis le pare-feu).
- **Action** : `ACCEPT`, `REJECT` (refus avec réponse) ou `DROP` (rejet silencieux).
- **Source & destination** : nom/repère, interface (entrée/sortie) et IP ou réseau (CIDR).
- **Protocole** : TCP, UDP, ICMP ou tous ; **port(s)** simples, multiples ou plages (`22`, `80,443`, `1000:2000`).
- Options : **règle de retour** automatique, préfixe `sudo`, journalisation (`LOG`), commentaires, et **MASQUERADE** (partage de connexion Internet).
- **Redirection de port (DNAT)** pour publier un service interne vers l'extérieur.
- Boutons **Copier** et **Télécharger `.sh`**.

## Prérequis

Pour **utiliser l'outil** : un navigateur web. Aucune installation.

Pour **appliquer les règles générées** :

- Une machine **Linux** utilisant `iptables`.
- Les **droits root** (ou `sudo`).
- Recommandé : connaître la politique par défaut de vos chaînes (l'outil suppose `DROP`).

## Guide d'utilisation pas à pas

1. **Ouvrez** `Generateur-iptables.html` dans votre navigateur.
2. Choisissez un **service courant** (le protocole et le port se remplissent tout seuls) ou passez en mode **personnalisé**.
3. Sélectionnez le **type de trafic** (FORWARD / INPUT / OUTPUT) et l'**action**.
4. Renseignez **source** et **destination** (interfaces, IP/réseaux).
5. Ajustez les **options** : règle de retour, `sudo`, `LOG`, commentaires, MASQUERADE.
6. Cliquez sur **« Générer les règles »**, puis **Copier** ou **Télécharger `.sh`**.
7. Appliquez les règles sur la machine Linux (en root) et **rendez-les persistantes** (`iptables-save` / `netfilter-persistent`).

> Ne cumulez pas les deux approches de suivi d'état : soit une règle globale `ESTABLISHED,RELATED` en tête de chaîne (et vous décochez « retour »), soit une règle de retour par flux. Faire les deux est redondant.

## Avertissement

Une mauvaise règle peut **vous couper l'accès distant** (SSH) à la machine. Testez de préférence via une **console locale/KVM** ou prévoyez un mécanisme de restauration automatique avant d'appliquer une politique `DROP`.

---

<p align="center"><em>Automatiser · Standardiser · Sécuriser</em></p>
