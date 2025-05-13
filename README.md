# 🏗️ Architecture Serverless :  "Chantier BTP connecté"  

**Objectif** : Suivi de chantier avec quicksight

## 📊 Diagramme
![Architecture AWS](architecture.png)

## 🔧 Composants
1. **IoT Core**: Collect la data depuis les capteurs IoT sur les engins.  
2. **Amazon S3** : Stockage de la data brute avec versioning enabled.
3. **Lambda** : Traitement de la data et détéection des alertes.
4. **DynamoDB** : Database pour stocker les alertes.
5. **Quicksight**: Visualisation des alertes et suivi des engins/coûts.
   

## 💡 Well architected Framewrok : 
1. **Operational excellence** : #Etre déployée en 1 Clic avec documentation reproductible
- Automatisation : Déploiement avec Cloud formation (pour reproductibilité) + script Python pour simuler les capteurs (éviter des tests manuels)
- Monitoring : CloudWatch (acrivé par défaut sur IoT Core et Lambda) pour tracer les erreurs
 
2. **Security** : #Least privilge pricniple + Encryption end to end
- Encryption end to end : IoT Core utilise TLS pour le chiffrement données en transit + S3 utilise AES-256 at rest
- Least privilege : Ajouter des rôles IAM restrictifs pour Lambda (accès uniquement à DynamoDB)
- Access control : Authentification via Certificat X.509 in Iot Core
 
3. **Reliability** : #Highly Available (AZ failure) and Scalable (+100capteurs)
- Redundance : S3 est multi-AZ par défaut + Dynamo DB est en mode standard (highly available)
- Gestion de pannes : Lambda retry automatiquement en cas d'échec
- Scalability : IoT Core et Lambda scale automatiquement avec la charge
 
4. **Performance efficiency** : #Architecture Serverless pour un temps de réponse <100ms pour les alertes
- Serverless : Lambda et IoT Core évite le surprovisionnement
- Optimization ressource : Dynamo "on demand" per-per-use and S3 intelligent-Tiering
- Latence maitrisée avec : Quicksight accède aux données pré-agrées (pas de requêtes lentes)

5. **Cost optimization**: #Tient dans la FreeTier mais concu pour optimiser les coûts à grande échelle
- Serverless : sans couts fixe, pay as you go
- Utilisation free tier : IoT Core avec 250message/min gratuit et S3 avec 5Go de stockage gratuit
- Alertes de couts : AWS budget pour éviter les surprises


