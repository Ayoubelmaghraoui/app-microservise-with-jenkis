 Architecture Microservices
Architecture
L'architecture microservices consiste en un ensemble de services indépendants, déployés de manière isolée, et communiquant entre eux par des interfaces bien définies. Cela favorise la résilience et la facilité de mise à l'échelle.
Description des services
Chaque service est dédié à une fonctionnalité spécifique de l'entreprise, assurant ainsi la séparation des préoccupations. Les services sont autonomes, ce qui simplifie le déploiement, la maintenance et les mises à jour.
Account service
Contient la logique générale de saisie et la validation : éléments de revenus/dépenses, paramètres d'épargne et de compte
.

Method	Path	Description	User authenticated	Available from UI
GET	/accounts/{account}	Get specified account data		
GET	/accounts/current	Get current account data	×	×
GET	/accounts/demo	Get demo account data (pre-filled incomes/expenses items, etc)		×
PUT	/accounts/current	Save current account data	×	×
POST	/accounts/	Register new account		×
Statistics service

Effectue des calculs sur les principaux paramètres statistiques et capture des séries chronologiques pour chaque compte. Le point de données contient des valeurs normalisées par rapport à la devise de base et à la période. Ces données sont utilisées pour suivre la dynamique des flux de trésorerie pendant la durée de vie du compte.

Method	Path	Description	User authenticated	Available from UI
GET	/statistics/{account}	Get specified account statistics		
GET	/statistics/current	Get current account statistics	×	×
GET	/statistics/demo	Get demo account statistics		×
PUT	/statistics/{account}	Create or update time series datapoint for specified account		
Notification service
Stocke les informations de contact de l'utilisateur et les paramètres de notification (rappels, fréquence de sauvegarde, etc.). Le travailleur planifié collecte les informations requises auprès d'autres services et envoie des messages électroniques aux clients abonnés.


Method	Path	Description	User authenticated	Available from UI	
GET	/notifications/settings/current	Get current account notification settings	×	×	
PUT	/notifications/settings/current	Save current account notification settings	×	×	

Notes

• Chaque microservice possède sa propre base de données, il n'y a donc aucun moyen de contourner l'API et d'accéder directement aux données de persistance.
• MongoDB est utilisé comme base de données principale pour chacun des services.
• Tous les services communiquent entre eux via l'API Rest
Infrastructure
Spring cloud provides powerful tools for developers to quickly implement common distributed systems patterns -  
Config service

Mécanismes de communication
La communication entre les microservices s'effectue généralement via des API REST ou des mécanismes de messagerie, assurant une interaction efficace tout en minimisant les dépendances.
 <img width="880" alt="730f2922-ee20-11e5-8df0-e7b51c668847" src="https://github.com/Ayoubelmaghraoui/app-microservise-with-jenkis/assets/122055457/c1bae105-0d67-4a2a-aa80-89cbf06b1215">
<img width="880" alt="889" src="https://github.com/Ayoubelmaghraoui/app-microservise-with-jenkis/assets/122055457/7106ab87-0dee-4c23-a1ad-d22084c9d12b">
jenkis:
![ayoub elm](https://github.com/Ayoubelmaghraoui/app-microservise-with-jenkis/assets/122055457/cbc53a2d-2e20-48a7-9b9e-3224b753451a)
![ayoub elm1](https://github.com/Ayoubelmaghraoui/app-microservise-with-jenkis/assets/122055457/023cbbec-2daf-4c5d-a43c-ebca774ea6aa)

Important endpoints
http://localhost:80 - Gateway
http://localhost:8761 - Eureka Dashboard
http://localhost:9000/hystrix - Hystrix Dashboard (Turbine stream link: http://turbine-stream-service:8080/turbine/turbine.stream)
http://localhost:15672 - RabbitMq management (default login/password: guest/guest)

