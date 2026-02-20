# Coach Sportif Virtuel Embarqué

**Analyse de mouvement et correction posturale en temps réel par Pose Estimation et Intelligence Artificielle**

Projet de fin d'études – Master 1 Intelligence Artificielle  
Université Cadi Ayyad – Faculté des Sciences Semlalia, Marrakech  
Module : Systèmes Embarqués et IA  
Année universitaire 2025 – 2026

---

### Réalisé par
- MEKKANI Wijdane  
- BAKRAOUI Salma  
- LAMRHNBAR Haytam  
- BATTAHI Zakariaa
- MOUSSAIF Abdelkabir

### Encadré par
Pr. AMEKSA Mohammed

---

## Présentation du projet

Le **Coach Sportif Virtuel Embarqué** est un système intelligent qui analyse en temps réel la posture et les mouvements de l'utilisateur lors d'exercices physiques, fournit des corrections instantanées et suit les performances, le tout en s'exécutant sur du matériel embarqué (notamment Raspberry Pi) ou en mode hybride.

Le système combine :
- **Vision par ordinateur** (MediaPipe + YOLOv11-Pose)
- **Apprentissage profond** (LSTM pour la classification des exercices et de la qualité)
- **Interface utilisateur moderne** (React/Next.js)
- **Contrôle matériel** (Rpi 5, LEDs, buzzer)

---

## Architecture du projet

Architecture **Client-Server** moderne avec séparation claire :

### Composants principaux
- **Backend** : Serveur FastAPI (Python)  
  → Capture caméra (OpenCV)  
  → Détection de pose (MediaPipe)  
  → Analyse de mouvement (LSTM + ONNX)  
  → Flux vidéo MJPEG + WebSockets pour feedback en temps réel

- **Frontend** : Application React/Next.js  
  → Affichage du flux vidéo avec squelette  
  → Feedback visuel, vocal et textuel  
  → Tableau de bord des performances

- **Matériel embarqué** (optionnel) : Raspberry Pi + webcam + servo + LEDs + buzzer

### Flux de données en temps réel
1. Capture d'images via caméra  
2. Extraction de 33 points clés avec MediaPipe  
3. Analyse de séquences par modèle LSTM → détection exercice + qualité posture  
4. Envoi des résultats via WebSockets (répétitions, erreurs, score confiance)  
5. Diffusion simultanée du flux vidéo annoté (/video_feed)  
6. Feedback multimodal : voix (Web Speech API), LEDs, buzzer, messages à l'écran

---

## Fonctionnalités principales

1. **Analyse posturale en temps réel**  
   Suivi précis des mouvements grâce à MediaPipe et YOLOv11-Pose (même sur Raspberry Pi)

2. **Classification intelligente des exercices**  
   Modèle LSTM identifie l'exercice (squat, pompe, etc.) et évalue la qualité

3. **Retour utilisateur multimodal**  
   - Voix (ex. : « Gardez le dos droit ! »)  
   - Signaux lumineux (LEDs) et sonores (buzzer)  
   - Messages visuels sur l’interface

4. **Suivi des performances**  
   - Comptage automatique des répétitions et séries  
   - Historique des sessions (SQLite)  
   - Statistiques et progression (tableau de bord)

5. **Centrage automatique de la caméra**  
   Utilisation d’un servo-moteur pour recentrer l’utilisateur

6. **Mode Hybride**  
   Backend sur Raspberry Pi + Frontend sur PC / hébergé Vercel

---

## Prérequis techniques

### Logiciels
- Python 3.9+  
- Node.js 18+  
- Bibliothèques clés :
  - `mediapipe`, `opencv-python`, `fastapi`, `uvicorn`
  - `tensorflow` / `keras` (LSTM)
  - `ultralytics` (YOLO)
  - `onnxruntime` (modèles ONNX)

### Matériel recommandé
- Webcam 720p ou mieux  
- Raspberry Pi 5 (ou PC moderne)  
- 4 Go de RAM minimum  
- (optionnel Si Rpi 5) Servo-moteur, LEDs RGB, buzzer piezo

---

## Installation & Lancement

### Backend
```bash
cd backend
python -m venv venv
# Windows : venv\Scripts\activate
# Linux/Mac : source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000
```
### Frontend (local)
```bash
cd frontend
npm install
npm run dev
```
→ Ouvrir http://localhost:3000

### Frontend déployé (Vercel)
Le frontend est déployé ici :
https://coach-sportif-frontend.vercel.app
(Le backend doit être accessible via ngrok ou un tunnel)

### Utilisation de ngrok (pour exposer le backend)
```Bash
ngrok http 8000
```
Copier l’URL https générée, puis la configurer dans Vercel :

NEXT_PUBLIC_API_URL = https://votre-url.ngrok-free.app
NEXT_PUBLIC_WS_URL  = wss://votre-url.ngrok-free.app/ws


Structure des dossiers (après nettoyage)
```text
├── backend/
│   ├── main.py               # Point d'entrée FastAPI
│   ├── models/               # Modèles IA (.h5, .onnx, .pt, .task)
│   ├── requirements.txt
│   └── ...
├── frontend/                 # Application Next.js
│   ├── components/
│   ├── pages/
│   └── ...
├── docs/                     # Documentation détaillée
└── README.md
```
### Documentation complète
Consultez les guides détaillés dans /docs :

Déploiement Hybride Vercel + Raspberry Pi
Configuration matérielle (LEDs, Buzzer, Servo)
Installation sur Raspberry Pi
Architecture détaillée du système


Développé dans le cadre du Master Intelligence Artificielle – Université Cadi Ayyad
Objectif : offrir une solution de coaching sportif accessible, intelligente et embarquée
Année universitaire 2025 – 2026
Marrakech, Maroc
