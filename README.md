# TP 8 : Authentification en mémoire avec Spring Security

## Objectif

Découvrir le fonctionnement fondamental de Spring Security en configurant une authentification en mémoire.

Ce TP permet de comprendre comment Spring intercepte les requêtes, vérifie les identifiants d'un utilisateur et accorde ou refuse l'accès selon son rôle.

## Compétences visées

- Comprendre le modèle d'authentification de Spring Security
- Créer des utilisateurs et rôles statiques
- Restreindre l'accès à certaines pages selon les rôles
- Personnaliser la page de connexion

## Structure du projet

```
spring-security-demo/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── ma/fstg/security/
│   │   │       ├── SpringSecurityDemoApplication.java
│   │   │       ├── config/
│   │   │       │   └── SecurityConfig.java
│   │   │       └── web/
│   │   │           └── HomeController.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── templates/
│   │           ├── login.html
│   │           ├── home.html
│   │           ├── user-dashboard.html
│   │           └── admin-dashboard.html
│   └── test/
└── pom.xml
```

## Utilisateurs configurés

- **Admin** : username=`admin`, password=`1234`, rôle=`ADMIN`
- **User** : username=`user`, password=`1111`, rôle=`USER`

## Routes et accès

- `/` - Accessible à tous les utilisateurs authentifiés
- `/login` - Accessible à tous (page de connexion)
- `/user/dashboard` - Accessible aux rôles USER et ADMIN
- `/admin/dashboard` - Accessible uniquement au rôle ADMIN

## Comment lancer le projet

1. Assurez-vous d'avoir Java 17+ et Maven installés
2. Compilez le projet : `mvn clean install`
3. Lancez l'application : `mvn spring-boot:run`
4. Accédez à http://localhost:8080

## Tests

1. Accédez à http://localhost:8080 - vous serez redirigé vers `/login`
2. Connectez-vous avec `user / 1111` :
   - Accès à `/` et `/user/dashboard` ✓
   - Accès refusé à `/admin/dashboard` ✗
3. Déconnectez-vous et reconnectez-vous avec `admin / 1234` :
   - Accès à toutes les pages ✓


https://github.com/user-attachments/assets/a9099e3a-9539-4656-aa83-570cdba438f4


## Notes importantes

- Les mots de passe utilisent `{noop}` pour indiquer qu'ils ne sont pas encodés (uniquement pour l'apprentissage)
- En production, utilisez toujours `BCryptPasswordEncoder` pour encoder les mots de passe
- Les utilisateurs sont stockés en mémoire et seront perdus au redémarrage de l'application

