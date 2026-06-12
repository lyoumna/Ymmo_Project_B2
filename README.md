Projet YMMO — Plateforme + Infrastructure Réseau
Ce projet combine une application web complète (backend + frontend + data) et une infrastructure réseau professionnelle basée sur Active Directory.

Il a été réalisé en binôme :

Youmna → Développement (backend, frontend, data)

Kenza → Infrastructure réseau (AD, DNS, GPO, pfSense, sécurité)

🛠 Stack Technique
🔧 Développement (Youmna)
Backend : Node.js, Express, PostgreSQL, JWT, bcrypt

Frontend : React, React Router, Axios

Data : Python (pandas, matplotlib, scikit-learn)

🖥 Infrastructure (Kenza)
pfSense (routeur + firewall)

Windows Server 2022 (Active Directory, DNS, GPO, partages réseau)

Windows 10 Client (intégré au domaine)

Gestion des droits : Groupes AD + Permissions NTFS

Automatisation : GPO (mappage des lecteurs réseau)

📁 Structure du Projet
Code
ymmo-backend/     → API REST (Node.js + Express + PostgreSQL)
ymmo-frontend/    → Interface web (React)
ymmo-data/        → Analyse de données (Python)
ymmo-infra/       → Documentation + schémas + rapport technique
🗄 Base de Données (DEV)
Tables principales :

users : id, nom, email, mot_de_passe (hashé), role, created_at

agences : id, nom, ville, adresse

biens : id, titre, description, type, prix, superficie, ville, statut, agence_id, agent_id

🔌 API — Routes principales
Méthode	URL	Accès
POST	/api/auth/register	Public
POST	/api/auth/login	Public (retourne un JWT)
GET	/api/biens	Public
GET	/api/biens/:id	Public
GET	/api/biens/search?q=	Public
GET	/api/biens/stats/ville	Public
POST	/api/biens	🔐 JWT requis
PUT	/api/biens/:id	🔐 JWT requis
DELETE	/api/biens/:id	🔐 JWT requis


🔐 Sécurité (DEV)
bcrypt : hash des mots de passe

JWT : token 24h, vérifié par middleware

Rôles : admin / user

💻 Frontend — Pages
/ — Accueil

/biens — Liste des annonces

/biens/:id — Détail

/login — Connexion

/register — Inscription

📊 Analyse de données
Prix moyen par ville

Répartition par type

Corrélation prix / superficie

Prédiction de prix (régression linéaire)

🏗 Infrastructure Réseau (Kenza)
🌐 1. pfSense — Routeur & Firewall
pfSense remplace la box Internet dans la maquette.

Fonctions :

Passerelle du réseau : 10.0.0.1

NAT + accès Internet

Firewall

Séparation WAN / LAN

👉 Preuves de fonctionnement :

Ping WAN (8.8.8.8)

Ping LAN (10.0.0.1)

Internet sur le client via pfSense

🏛 2. Active Directory — Domaine ymmo.local
Le serveur Windows est le contrôleur de domaine.

Domaine : ymmo.local

Rôle : Primary Domain Controller

DNS intégré

Gestion des utilisateurs, groupes, GPO

👉 Vérification :
systeminfo | findstr /i "Domain"

🧩 3. DNS — Résolution interne
Zone : ymmo.local

Serveur DNS : 10.0.0.10

Résolution testée via :
nslookup ymmo.local

🗂 4. OU — Organisation du domaine
OU créées :

Siège

Agence

Groupes

Serveurs

Utilisateurs

👥 5. Groupes AD — Gestion des droits
Groupes créés :

GG_Siege

GG_Direction

GG_Commerciaux

Utilisés pour :

Permissions NTFS

Ciblage GPO

Accès aux partages

📁 6. Dossiers partagés + Permissions NTFS
Dossiers dans C:\Partages :

Commun

Direction

Commerciaux

Permissions NTFS basées sur les groupes AD.

🔗 7. GPO — Mappage automatique des lecteurs réseau
GPO : GPO_Mappage_Lecteurs

Chemin :

Code
User Configuration → Preferences → Windows Settings → Drive Maps
Lecteurs montés automatiquement :

H: Commun

I: Direction

J: Commerciaux

Avec Item-Level Targeting selon le groupe AD.

🖥 8. Client Windows — Intégré au domaine
Tests effectués :

Vérification du domaine
systeminfo | findstr /i "Domain"

Vérification réseau
ipconfig /all

Application des GPO
gpupdate /force

Vérification des lecteurs réseau
Explorateur → Ce PC

🧩 Répartition des tâches
Personne	Rôle	Travail réalisé
Youmna	Développement	Backend, Frontend, API, Data
Kenza	Infrastructure	AD, DNS, GPO, pfSense, partages, sécurité réseau


📦 Livrables fournis
Code complet (backend, frontend, data)

Documentation infrastructure

Schéma réseau

MCD

Rapport technique complet (INFRA)

Captures de tests (GPO, DNS, AD, pfSense)

🚀 Lancer le projet
Backend
Code
cd ymmo-backend
npm install
npm run dev
Frontend
Code
cd ymmo-frontend
npm install
npm start
Data
Code
cd ymmo-data
pip install pandas psycopg2-binary matplotlib seaborn scikit-learn
python analyse.py
