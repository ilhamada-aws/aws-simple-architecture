# 🏗️ Architecture AWS Simple : Site Web Statique

**Objectif** : Héberger un site web statique (HTML/CSS) sur AWS avec haute disponibilité.

## 📊 Diagramme
![Architecture AWS](architecture.png)

## 🔧 Composants
1. **Amazon S3** : Stockage des fichiers HTML/CSS.
2. **CloudFront** : CDN pour accélérer le site.
3. **Route 53** : DNS pour le nom de domaine.

## 💡 Bonnes Pratiques
- Activer le **versioning** sur S3.
- Utiliser **HTTPS** via CloudFront.
