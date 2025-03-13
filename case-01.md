## 🌟 **Introduction**
Dans ce cours, nous allons concevoir une architecture cloud **serverless** sur AWS pour une entreprise fictive "Any Company Online". L'objectif est d'apprendre à créer une infrastructure **scalable, fiable et optimisée** en utilisant des services AWS tels que **Lambda, DynamoDB, SNS et SQS**.

---

## 🔄 **Customer #1 : Use Case and Requirements**
### 🔍 **Présentation du Client**
"Any Company Online" est une entreprise e-commerce souhaitant migrer vers AWS pour bénéficier des avantages du cloud : 
- ✅ **Évolutivité automatique**
- ✅ **Réduction des coûts**
- ✅ **Haute disponibilité**
- ✅ **Découplage des services**

### 💡 **Besoins Fonctionnels**
- Une API REST pour gérer les commandes.
- Un stockage sécurisé et évolutif pour les commandes.
- Un système de notifications pour informer les clients.
- Une architecture event-driven pour assurer la scalabilité.

### 🚫 **Contraintes Techniques**
- Pas de gestion de serveurs.
- Temps de réponse rapide.
- Sécurité des données garantie.

---

## 🛠️ **Architecting the Solution**

### 🏡 **Sélection des Services AWS**
| Fonctionnalité | Service AWS | Raison |
|-----------------|--------------|--------|
| API REST | **AWS Lambda + API Gateway** | Scalabilité, paiement à l'usage |
| Stockage de commandes | **DynamoDB** | NoSQL rapide et sans gestion de serveur |
| Notifications | **SNS** | Envoi de SMS, emails, et push notifications |
| Gestion des files d'attente | **SQS** | Découplage des services |
| Stockage de fichiers | **Amazon S3** | Stockage fiable et économique |

### 🛠️ **Schéma de l'Architecture**
1. Un client passe une commande via **API Gateway**.
2. Une fonction **Lambda** traite la commande.
3. Les données sont stockées dans **DynamoDB**.
4. Une notification est envoyée via **SNS**.
5. Un message est ajouté à une file **SQS** pour traitement différé.

---

## 🛠️ **Selecting a Serverless Compute Service**
### **AWS Lambda Exploration**
**AWS Lambda** permet d'exécuter du code sans gérer de serveurs.
- **Scalabilité automatique**
- **Facturation à la demande**
- **Supporte Python, Node.js, Java, etc.**

#### 📝 **Code Exemple d'une Lambda (Python)**
```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
sns = boto3.client('sns')

def lambda_handler(event, context):
    order = json.loads(event['body'])
    table = dynamodb.Table('Orders')
    table.put_item(Item=order)
    sns.publish(TopicArn='arn:aws:sns:region:account-id:OrderNotifications', Message=f'Commande {order["order_id"]} reçue')
    return {'statusCode': 200, 'body': json.dumps({'message': 'Commande enregistrée'})}
```

---

## 🔄 **Choosing an AWS Database Service**
### **DynamoDB Exploration**
DynamoDB est une base de données **NoSQL** hautement évolutive.
- **Performances garanties** avec des latences millisecondes.
- **Scalabilité automatique**.
- **Sans serveur**, entièrement managé.

#### **Création d'une Table DynamoDB**
1. Aller sur **DynamoDB > Créer une table**.
2. Nom : **Orders**.
3. Clé primaire : **order_id** (String).

---

## 📈 **Building Event-Driven Architectures**
### **SNS Exploration**
Amazon SNS permet d'envoyer des notifications **asynchrones**.
- Notifications via **email, SMS, push, Lambda, SQS**.
- **Temps réel** et **scalabilité automatique**.

#### **Création d'un Sujet SNS**
1. Aller sur **SNS > Créer un sujet**.
2. Nom : **OrderNotifications**.
3. Copier l'ARN et l'ajouter à Lambda.

---

## 🌐 **Decoupling AWS Solutions**
### **SQS Exploration**
Amazon SQS permet de découpler les composants d'une application.
- **File d'attente** permettant un traitement différé.
- **Scalabilité automatique**.
- **Durabilité des messages**.

#### **Création d'une File SQS**
1. Aller sur **SQS > Créer une file**.
2. Nom : **OrderProcessingQueue**.
3. Choisir une **file standard**.

---

## 💡 **Consider this Scenario**
Imaginez qu'une entreprise traite **1000 commandes/minute**. Grâce à **Lambda, DynamoDB, SNS et SQS**, AWS gère automatiquement la charge.

---

## 🌟 **Presenting the Solution to the Customer and Next Steps**
### **Customer #1: Solution Overview**
L'architecture serverless permet :
- **Une haute disponibilité**.
- **Une réduction des coûts**.
- **Un système modulaire et évolutif**.

### **Taking this Architecture to the Next Level**
- Ajouter **AWS Step Functions** pour gérer les workflows.
- Activer **DynamoDB Streams** pour synchroniser les données en temps réel.

---

## 📈 **Exercise 1 Walkthrough**
1. **Créer une fonction Lambda** pour enregistrer une commande.
2. **Créer une table DynamoDB** pour stocker les commandes.
3. **Configurer SNS** pour envoyer des notifications.
4. **Créer une file SQS** pour la gestion asynchrone des commandes.
5. **Tester l'API avec Postman** en envoyant une commande.

---

## 💡 **Challenge: Building a Proof of Concept**
Ajoutez **Amazon SES** pour envoyer des emails de confirmation.

---

## 📊 **Assessment 1**
| Critère | Vérification |
|---------|-------------|
| API Gateway fonctionne | ✅ |
| Lambda exécute bien le traitement | ✅ |
| DynamoDB stocke les commandes | ✅ |
| SNS envoie les notifications | ✅ |
| SQS reçoit les messages | ✅ |

---

## 📈 **Conclusion**
Ce cours vous a permis de concevoir une **architecture serverless AWS** complète. 

### 🚀 **Prochaines Étapes**
- Déployer un **front-end React** pour interagir avec l'API.
- Étudier **AWS Well-Architected Framework**.
- Ajouter **une base de données relationnelle (RDS)** pour des fonctionnalités avancées.
