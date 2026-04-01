# Cahier des charges

## 1. Contexte et justification
Dans de nombreux établissements de santé en Afrique, et particulièrement en République Démocratique du Congo, la gestion des dossiers patients reste largement basée sur le papier. Cette situation entraîne des pertes de temps, des erreurs de recherche, des doublons de dossiers, des difficultés de suivi médical et parfois des retards de prise en charge pouvant mettre des vies en danger.

Le présent projet vise à concevoir une application sanitaire centralisée permettant aux professionnels de santé d’accéder rapidement aux informations d’un patient, quel que soit son lieu d’origine ou l’établissement où il a déjà été reçu.

## 2. Objectif général
Créer une application de gestion sanitaire permettant d’identifier, consulter et suivre un patient en quelques secondes afin de réduire la lourdeur administrative et d’améliorer la continuité des soins.

## 3. Objectifs spécifiques
- Centraliser les dossiers patients.
- Réduire le temps de recherche d’un patient.
- Limiter les doublons de dossiers.
- Faciliter la consultation de l’historique médical.
- Améliorer la coordination entre les structures de santé.
- Sécuriser les données médicales.
- Permettre un usage simple par les médecins et agents de santé.

## 4. Périmètre du projet
L’application couvrira les fonctionnalités suivantes:
- Création et gestion des patients.
- Recherche rapide par nom, téléphone, numéro d’identification ou autre critère.
- Consultation de l’historique médical.
- Enregistrement des consultations.
- Enregistrement des prescriptions.
- Gestion des examens et résultats.
- Gestion des utilisateurs et des rôles.
- Journalisation des actions.
- Synchronisation des données entre établissements, si l’architecture le permet.

Le projet ne couvre pas, dans sa première version:
- La gestion complète de la facturation hospitalière.
- La pharmacie avancée.
- La gestion de stock.
- La télémédecine avancée.
- Les tableaux de bord nationaux complexes.

## 5. Utilisateurs cibles
- Médecins.
- Infirmiers.
- Agents d’accueil / secrétariat.
- Administrateurs système.
- Responsables médicaux.
- Superviseurs régionaux ou hospitaliers.

## 6. Besoin principal
Permettre à un professionnel de santé de retrouver rapidement le dossier d’un patient et de consulter ses informations médicales essentielles sans dépendre des archives papier.

## 7. Fonctionnalités attendues

### 7.1 Gestion des patients
- Créer un dossier patient.
- Modifier les informations d’un patient.
- Rechercher un patient.
- Fusionner les doublons après vérification.
- Archiver un dossier sans le supprimer.

### 7.2 Recherche patient
- Recherche par nom.
- Recherche par prénom.
- Recherche par numéro de téléphone.
- Recherche par numéro d’identification unique.
- Recherche par date de naissance.
- Recherche combinée avec filtres.

### 7.3 Dossier médical
- Afficher les données d’identification du patient.
- Afficher les antécédents médicaux.
- Afficher les allergies connues.
- Afficher les consultations passées.
- Afficher les diagnostics.
- Afficher les prescriptions.
- Afficher les examens et résultats.
- Afficher les hospitalisations passées.

### 7.4 Consultations
- Créer une consultation.
- Saisir les signes cliniques.
- Enregistrer le diagnostic.
- Enregistrer le traitement.
- Générer un résumé de consultation.

### 7.5 Prescriptions
- Ajouter les médicaments prescrits.
- Préciser la posologie.
- Préciser la durée du traitement.
- Associer une prescription à une consultation.

### 7.6 Examens et résultats
- Demander un examen.
- Enregistrer le résultat.
- Joindre un fichier si nécessaire.
- Consulter l’historique des examens.

### 7.7 Gestion des utilisateurs
- Créer un compte utilisateur.
- Assigner un rôle.
- Activer ou désactiver un compte.
- Définir les permissions selon le rôle.

### 7.8 Traçabilité
- Enregistrer qui a consulté un dossier.
- Enregistrer qui a modifié une information.
- Conserver l’historique des changements.

## 8. Données à gérer
Chaque patient devra contenir au minimum:
- Numéro d’identification unique.
- Nom.
- Prénom.
- Sexe.
- Date de naissance.
- Lieu de naissance.
- Adresse ou province.
- Numéro de téléphone.
- Nom d’un contact d’urgence.
- Antécédents médicaux.
- Allergies.
- Groupe sanguin si disponible.
- Historique des consultations.
- Historique des prescriptions.
- Historique des examens.

## 9. Exigences fonctionnelles détaillées
- Le système doit permettre de rechercher un patient en moins de quelques secondes.
- Le système doit empêcher les doublons autant que possible.
- Le système doit conserver l’historique complet des actions.
- Le système doit permettre une consultation rapide du dossier depuis n’importe quel poste autorisé.
- Le système doit être simple à utiliser par un personnel non technique.
- Le système doit fonctionner dans un environnement à faible connexion internet.

## 10. Exigences non fonctionnelles

### 10.1 Performance
- Recherche rapide des dossiers.
- Interface fluide même avec un grand volume de données.
- Temps de réponse réduit pour les opérations courantes.

### 10.2 Sécurité
- Authentification obligatoire.
- Mots de passe sécurisés.
- Gestion stricte des rôles.
- Chiffrement des données sensibles.
- Sauvegarde régulière.
- Journal d’audit.

### 10.3 Disponibilité
- Application accessible pendant les heures de service.
- Mécanisme de reprise après panne.
- Sauvegarde automatique.

### 10.4 Ergonomie
- Interface simple.
- Navigation claire.
- Formulaires courts et compréhensibles.
- Utilisation possible sur ordinateur et tablette.

### 10.5 Compatibilité
- Navigateur web moderne.
- Poste de travail standard.
- Possibilité d’évolution vers mobile.

## 11. Architecture recommandée
- Application web pour les établissements.
- Base de données centrale sécurisée.
- API backend pour les échanges de données.
- Module d’authentification et de gestion des rôles.
- Possibilité de mode hors ligne avec synchronisation différée.

## 12. Proposition technologique
Choix possible pour une première version:
- Frontend: React ou Vue.
- Backend: Node.js, Django ou Laravel.
- Base de données: PostgreSQL.
- Authentification: JWT ou session sécurisée selon l’architecture.
- Déploiement: serveur local hospitalier ou cloud sécurisé.

## 13. Sécurité et confidentialité
- Accès réservé aux utilisateurs autorisés.
- Journalisation des accès aux dossiers.
- Sauvegardes automatiques.
- Protection contre la suppression accidentelle.
- Masquage de certaines données selon le rôle.
- Respect de la confidentialité médicale.

## 14. Phases de réalisation

### Phase 1: Analyse
- Recueil des besoins.
- Validation des fonctionnalités prioritaires.
- Définition des utilisateurs et des rôles.

### Phase 2: Conception
- Maquettes des écrans.
- Modèle de données.
- Architecture technique.

### Phase 3: Développement
- Gestion des patients.
- Recherche.
- Consultations.
- Authentification.
- Historique.

### Phase 4: Tests
- Tests fonctionnels.
- Tests de performance.
- Tests de sécurité.
- Tests utilisateurs.

### Phase 5: Déploiement pilote
- Mise en service dans un hôpital pilote.
- Formation des utilisateurs.
- Correction des anomalies.

### Phase 6: Généralisation
- Extension progressive à d’autres structures.

## 15. Livrables attendus
- Cahier des charges validé.
- Maquettes de l’application.
- Application fonctionnelle.
- Documentation utilisateur.
- Documentation technique.
- Plan de sauvegarde et de sécurité.
- Rapport de tests.

## 16. Critères de réussite
Le projet sera considéré comme réussi si:
- Un patient peut être retrouvé rapidement.
- Le personnel utilise facilement l’outil.
- Les dossiers sont moins souvent perdus ou dupliqués.
- Le temps administratif est réduit.
- Les données sont sécurisées.
- Le système fonctionne dans un hôpital pilote sans blocage majeur.

## 17. Risques et contraintes
- Faible connexion internet.
- Coupures d’électricité.
- Résistance au changement du personnel.
- Mauvaise qualité des données saisies.
- Besoin de formation des utilisateurs.
- Risques liés à la sécurité des données.

## 18. Besoins complémentaires
- Formation du personnel.
- Maintenance technique.
- Support utilisateur.
- Sauvegardes régulières.
- Mise à jour continue du système.

## 19. Conclusion
Ce projet vise à moderniser la gestion sanitaire en République Démocratique du Congo en facilitant l’accès rapide aux informations médicales des patients. Il doit être conçu de manière simple, sécurisée, évolutive et adaptée aux réalités locales.
