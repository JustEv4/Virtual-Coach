# 🏋️ Virtual Sports Coach

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61dafb.svg)](https://reactjs.org/)
[![ngrok](https://img.shields.io/badge/ngrok-ready-blueviolet)](https://ngrok.com/)
[![Git LFS](https://img.shields.io/badge/Git%20LFS-enabled-orange)](https://git-lfs.github.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An intelligent, real-time virtual coach that uses computer vision and machine learning to analyze exercise form, provide instant feedback, and track workout progress. Perfect for home workouts, rehabilitation, and fitness training.
## 🎥 Demo

Watch the Virtual Sports Coach in action:

[![Virtual Sports Coach Demo](https://img.youtube.com/vi/fgQ3sqatliQ/0.jpg)](https://www.youtube.com/watch?v=fgQ3sqatliQ)
## ✨ Features

- **Real-time pose detection** using MediaPipe and YOLOv8
- **Exercise form analysis** with custom ML models (LSTM, ONNX)
- **Instant audio feedback** via pyttsx3
- **Public URL access** via ngrok (share your workout session remotely)
- **Hardware integration** for Raspberry Pi (LEDs, buzzer)
- **Progress tracking** with SQLite database
- **Cross-platform** (Windows, Raspberry Pi, Linux)
- **Modern web interface** built with React/Next.js
- **WebSocket support** for real-time communication

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [ML Models](#-ml-models)
- [🌐 Public Access with ngrok](#-public-access-with-ngrok)
- [Project Structure](#-project-structure)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Hardware Setup](#-hardware-setup-for-raspberry-pi)
- [API Documentation](#-api-documentation)
- [Contributing](#-contributing)
- [License](#-license)

<div align="center">

![Couverture du rapport](docs/images/couverture-rapport.jpg)

# Coach Sportif Virtuel Embarqué

**Analyse de mouvement et correction posturale en temps réel**  
**par Pose Estimation et Intelligence Artificielle**

</div>

<p align="center">
  <strong>Projet de fin d'études – Master 1 Intelligence Artificielle</strong><br>
  Université Cadi Ayyad – Faculté des Sciences Semlalia, Marrakech<br>
  Département d'Informatique – Filière : Master Intelligence Artificielle (M1)<br>
  Module : Systèmes Embarqués et IA<br>
  Année universitaire 2025 – 2026
</p>

<p align="center">
  <strong>Réalisé par :</strong><br>
  • MEKKANI Wijdane<br>
  • BAKRAOUI Salma<br>
  • LAMRHNBAR Haytam<br>
  • BATTAHI Zakariaa
</p>

<p align="center">
  <strong>Encadré par :</strong><br>
  Pr. AMEKSA Mohammed
</p>

<p align="center">
  <strong>Contributions techniques importantes :</strong><br>
  Moussaif Abdelkabir
</p>

<p align="center">
  <a href="https://github.com/JustEv4/Virtual-Coach"><img src="https://img.shields.io/github/repo-size/JustEv4/Virtual-Coach?style=flat-square&logo=github" alt="Repo size"></a>
  <a href="https://github.com/JustEv4/Virtual-Coach/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License MIT"></a>
  <a href="https://github.com/JustEv4/Virtual-Coach/stargazers"><img src="https://img.shields.io/github/stars/JustEv4/Virtual-Coach?style=flat-square" alt="Stars"></a>
</p>

<br>

## 🎯 Objectif du projet

Développer un système intelligent embarqué capable d’analyser en temps réel la posture et les mouvements lors d’exercices physiques, de détecter les erreurs posturales courantes et de fournir un retour multimodal immédiat (visuel, vocal, lumineux et sonore), le tout exécuté localement sur un Raspberry Pi 5 ou en architecture hybride (backend embarqué + frontend accessible à distance).

## ✨ Fonctionnalités principales

- Détection précise de la pose en temps réel (MediaPipe Tasks + YOLOv11-pose)
- Classification des exercices et évaluation de la qualité posturale (modèle LSTM + ONNX)
- Comptage automatique des répétitions et détection d’anomalies (genoux, dos, etc.)
- Feedback multimodal : synthèse vocale, LEDs RGB, buzzer piezo
- Centrage automatique de la caméra grâce à un servomoteur
- Suivi des performances et historique des séances (base SQLite)
- Mode hybride : frontend déployé sur Vercel + backend exposé via ngrok
- Interface web moderne, responsive et intuitive (Next.js + Tailwind CSS)

## 🎥 Démonstration

<!-- Remplace cette ligne par ton vrai lien vidéo (upload sur GitHub ou YouTube non répertorié) -->
https://github.com/JustEv4/Virtual-Coach/assets/xxxxxxxx/xxxxxxxxxxxxxxxxxxxxxxxx

> Vidéo de démonstration (~1 min 45) : calibration T-pose → exercices → feedback vocal + LEDs + visualisation des statistiques

<br>

## 🛠️ Stack technique

| Couche                      | Technologie                              | Rôle principal                                      |
|-----------------------------|------------------------------------------|-----------------------------------------------------|
| Backend                     | FastAPI • Python 3.11                    | API REST + WebSocket + streaming vidéo MJPEG        |
| Frontend                    | Next.js 14/15 • React • Tailwind CSS     | Interface utilisateur temps réel                    |
| Vision par ordinateur       | MediaPipe Tasks API • OpenCV • YOLOv11   | Extraction 33 landmarks corporels                   |
| Intelligence Artificielle   | LSTM (Keras) • ONNX Runtime • TFLite     | Classification exercices & détection erreurs        |
| Matériel embarqué           | Raspberry Pi 5 • GPIO Zero • lgpio       | Contrôle servo, LEDs RGB, buzzer                    |
| Déploiement distant         | Vercel (frontend) • ngrok (tunnel)       | Accès public / démonstration à distance             |
| Persistance                 | SQLite (aiosqlite)                       | Profils utilisateurs + historique des séances       |

<br>

## 📂 Structure du dépôt
Virtual-Coach/
├── backend/                # Serveur FastAPI + IA + capture caméra + hardware
├── frontend/               # Application Next.js + interface utilisateur
├── docs/                   # Documentation complète et rapport
│   ├── Architecture.md
│   ├── Architecture_RaspberryPi.md
│   ├── DEPLOYMENT_VERCEL_PI.md
│   ├── HARDWARE_CONFIG.md
│   ├── Setup_RaspberryPi.md
│   └── Rapport_Virtual_Coach_sporif.pdf     # Rapport final (56 pages)
├── models/                 # Modèles IA (stockés via Git LFS)
├── scripts/                # Scripts d’installation et de lancement
└── README.md
text<br>

## 🚀 Installation rapide

### Prérequis
- Python 3.11+
- Node.js 18+
- Git LFS installé (`git lfs install`)

```bash
# Cloner le dépôt + récupérer les modèles
git clone https://github.com/JustEv4/Virtual-Coach.git
cd Virtual-Coach
git lfs pull

# Backend
cd backend
python -m venv venv
source venv/bin/activate          # Windows : venv\Scripts\activate
pip install -r requirements.txt

# Frontend
cd ../frontend
npm install
Lancement local (PC ou Raspberry Pi)
Backend :
Bashuvicorn main:app --host 0.0.0.0 --port 8000
Frontend :
Bashnpm run dev
→ http://localhost:3000
Mode hybride (frontend Vercel + backend Pi)
Consulte le guide détaillé :
→ docs/DEPLOYMENT_VERCEL_PI.md


📚 Documentation complète
Tous les documents sont disponibles dans le dossier /docs :

Architecture globale du système
Architecture spécifique sur Raspberry Pi 5
Installation et configuration sur Raspberry Pi
Câblage matériel (GPIO, servo, LEDs, buzzer)
Déploiement hybride Vercel + ngrok
Rapport de projet complet (PDF 56 pages)



📄 Licence
MIT License – voir le fichier LICENSE



Projet réalisé dans le cadre du Master Intelligence Artificielle
Université Cadi Ayyad – Faculté des Sciences Semlalia Marrakech
Année universitaire 2025 – 2026
```
