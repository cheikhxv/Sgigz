# Déploiement sur Vercel

Ce document explique comment déployer le site web multilingue Swiftgigz sur Vercel, une plateforme de déploiement optimisée pour les applications Next.js.

## Prérequis

- Un compte GitHub pour héberger le code source
- Un compte Vercel pour le déploiement
- Le domaine swiftgigz.com déjà acheté et prêt à être configuré

## Étapes de déploiement

### 1. Préparation du code pour le déploiement

Le code est déjà optimisé pour le déploiement avec :
- Configuration multilingue complète
- Optimisations SEO (sitemap.xml, robots.txt)
- Optimisations de performance
- Tests de compatibilité

### 2. Création d'un dépôt GitHub

1. Créer un nouveau dépôt sur GitHub nommé "swiftgigz-website"
2. Initialiser le dépôt Git local et pousser le code :
   ```bash
   cd /home/ubuntu/swiftgigz_site
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/votre-username/swiftgigz-website.git
   git push -u origin main
   ```

### 3. Déploiement sur Vercel

1. Se connecter à [Vercel](https://vercel.com)
2. Cliquer sur "New Project"
3. Importer le dépôt GitHub "swiftgigz-website"
4. Configuration du projet :
   - Framework Preset: Next.js
   - Root Directory: ./
   - Build Command: `npm run build`
   - Output Directory: .next
   - Environment Variables: Aucune nécessaire pour l'instant

5. Cliquer sur "Deploy"

### 4. Configuration du domaine personnalisé

1. Dans le tableau de bord du projet Vercel, aller dans "Settings" > "Domains"
2. Ajouter le domaine "swiftgigz.com"
3. Suivre les instructions pour configurer les enregistrements DNS :
   - Type: A
   - Name: @
   - Value: (adresse IP fournie par Vercel)
   - TTL: 3600

4. Ajouter également le sous-domaine "www" :
   - Type: CNAME
   - Name: www
   - Value: cname.vercel-dns.com
   - TTL: 3600

### 5. Configuration SSL

Vercel fournit automatiquement des certificats SSL Let's Encrypt. Vérifier que HTTPS est activé dans les paramètres du projet.

### 6. Vérification du déploiement

1. Vérifier que le site est accessible à l'adresse swiftgigz.com
2. Tester la redirection automatique vers la langue préférée de l'utilisateur
3. Vérifier que toutes les pages sont accessibles dans les trois langues
4. Tester les performances avec des outils comme Lighthouse ou PageSpeed Insights

### 7. Mise en place d'un pipeline CI/CD

Pour les déploiements futurs, configurer un workflow GitHub Actions :

1. Créer un fichier `.github/workflows/deploy.yml` avec le contenu suivant :
   ```yaml
   name: Deploy to Vercel
   on:
     push:
       branches: [main]
   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Deploy to Vercel
           uses: amondnet/vercel-action@v20
           with:
             vercel-token: ${{ secrets.VERCEL_TOKEN }}
             vercel-org-id: ${{ secrets.ORG_ID }}
             vercel-project-id: ${{ secrets.PROJECT_ID }}
             working-directory: ./
   ```

2. Configurer les secrets GitHub nécessaires

## Maintenance et mises à jour

- Les déploiements futurs seront automatiquement déclenchés par des push sur la branche main
- Surveiller les performances et l'utilisation du site via le tableau de bord Vercel
- Mettre à jour régulièrement les dépendances pour maintenir la sécurité et les performances
