# Déploiement de projet sur Railway et Netlify en CI/CD avec GitHub Actions

## Dockerfile

Construction d'une image Node.js :

- Utilisation de l'image de base `node:20-alpine`
- Définition d'un dossier de travail `/app` dans le container
- Copie des fichiers `package*.json`
- Installation des dépendances
- Copie du reste du code source
- Exposition du port `8000`
- Lancement de l'application via `node server.js`

---

## Workflow Github Actions (`main.yml`)

À chaque push sur la branche `main` :

- Le backend est rebuild et redéployé sur **Railway**
- Le frontend est rebuild et redéployé sur **Netlify**
- Les deux jobs s'exécutent en parallèle

### Déclencheur

- Push sur la branche `main`

### Jobs

#### Backend (Railway)

- Nom d'affichage personnalisé
- Variables d'environnement Railway
- Système d'exploitation : Ubuntu
- Étapes clés :
  - Envoi du code à Railway (build & déploiement du Dockerfile)
  - Authentification via le token stocké dans les secrets du repo Github

#### Frontend (Netlify)

- Récupération du code
- Installation de Node.js
- Build du frontend (React + Vite)
- Installation et déploiement sur Netlify

---

## Résultat Github Actions

Le workflow a réussi :

- Tous les jobs ont passé leurs tests
- L'image Docker a été buildée et déployée sur Railway sans erreurs
