# Modèle de base de données

Ce modèle vise une première version d'une application sanitaire centralisée, simple à déployer dans un hôpital ou un réseau d'établissements. Il est pensé pour retrouver rapidement un patient, suivre ses consultations et conserver la traçabilité des accès.

## Principes de conception
- Chaque patient possède un identifiant unique interne.
- Un même patient peut avoir plusieurs consultations, prescriptions et examens.
- Un utilisateur est rattaché à un rôle.
- Toutes les actions sensibles doivent être historisées.
- La structure doit rester simple, mais évolutive vers un système national.

## Tables principales

### 1. `users`
Représente les comptes applicatifs du personnel de santé et des administrateurs.

Champs:
- `id` : identifiant technique, clé primaire.
- `full_name` : nom complet.
- `email` : adresse de connexion, unique.
- `phone` : numéro de téléphone, optionnel mais recommandé.
- `password_hash` : mot de passe chiffré.
- `role_id` : rôle principal de l'utilisateur.
- `facility_id` : établissement de rattachement.
- `is_active` : statut du compte.
- `created_at` : date de création.
- `updated_at` : date de mise à jour.

### 2. `roles`
Définit les rôles et permissions générales.

Champs:
- `id` : clé primaire.
- `name` : nom du rôle, par exemple `admin`, `doctor`, `nurse`, `receptionist`.
- `description` : description du rôle.

### 3. `facilities`
Représente les hôpitaux, centres de santé ou cliniques.

Champs:
- `id` : clé primaire.
- `name` : nom de l'établissement.
- `type` : hôpital, centre de santé, clinique, poste médical.
- `province` : province.
- `city` : ville ou territoire.
- `address` : adresse complète.
- `phone` : contact principal.
- `is_active` : statut.
- `created_at` : date de création.

### 4. `patients`
Contient les informations d'identification du patient.

Champs:
- `id` : clé primaire.
- `patient_code` : numéro unique du patient, unique.
- `last_name` : nom.
- `first_name` : prénom.
- `gender` : sexe.
- `date_of_birth` : date de naissance.
- `place_of_birth` : lieu de naissance.
- `phone` : téléphone principal.
- `address` : adresse ou quartier.
- `province` : province.
- `national_id_number` : numéro d'identification national si disponible.
- `marital_status` : situation matrimoniale, optionnel.
- `blood_group` : groupe sanguin, optionnel.
- `emergency_contact_name` : contact d'urgence.
- `emergency_contact_phone` : téléphone du contact d'urgence.
- `created_at` : date de création.
- `updated_at` : date de mise à jour.

### 5. `patient_identifiers`
Permet de stocker plusieurs identifiants pour un même patient si nécessaire.

Champs:
- `id` : clé primaire.
- `patient_id` : référence vers `patients`.
- `identifier_type` : type d'identifiant, par exemple national, hospitalier, assurance.
- `identifier_value` : valeur de l'identifiant.
- `issuing_facility_id` : établissement qui a émis l'identifiant.
- `created_at` : date de création.

### 6. `allergies`
Liste des allergies possibles.

Champs:
- `id` : clé primaire.
- `name` : nom de l'allergie.
- `description` : précision éventuelle.

### 7. `patient_allergies`
Table de liaison entre patients et allergies.

Champs:
- `id` : clé primaire.
- `patient_id` : référence vers `patients`.
- `allergy_id` : référence vers `allergies`.
- `severity` : faible, moyenne, grave.
- `notes` : commentaire.
- `created_at` : date de création.

### 8. `medical_histories`
Stocke les antécédents médicaux du patient.

Champs:
- `id` : clé primaire.
- `patient_id` : référence vers `patients`.
- `history_type` : pathologie chronique, chirurgie, traumatisme, autre.
- `description` : détail de l'antécédent.
- `recorded_by` : utilisateur ayant saisi l'information.
- `recorded_at` : date d'enregistrement.

### 9. `encounters`
Représente une consultation, une admission ou un passage médical.

Champs:
- `id` : clé primaire.
- `patient_id` : référence vers `patients`.
- `facility_id` : établissement concerné.
- `doctor_id` : médecin responsable.
- `encounter_type` : consultation, urgence, hospitalisation, suivi.
- `visit_date` : date de la visite.
- `chief_complaint` : motif principal.
- `notes` : observation générale.
- `status` : ouverte, fermée, annulée.
- `created_at` : date de création.

### 10. `diagnoses`
Contient les diagnostics posés à l'occasion d'une consultation.

Champs:
- `id` : clé primaire.
- `encounter_id` : référence vers `encounters`.
- `diagnosis_code` : code médical si disponible.
- `diagnosis_name` : libellé du diagnostic.
- `diagnosis_type` : principal, secondaire, suspecté.
- `notes` : détail complémentaire.
- `created_at` : date de création.

### 11. `prescriptions`
Représente l'ordonnance générée pendant une consultation.

Champs:
- `id` : clé primaire.
- `encounter_id` : référence vers `encounters`.
- `prescribed_by` : utilisateur qui a prescrit.
- `prescription_date` : date de prescription.
- `instructions` : remarques générales.
- `created_at` : date de création.

### 12. `prescription_items`
Liste détaillée des médicaments ou soins prescrits.

Champs:
- `id` : clé primaire.
- `prescription_id` : référence vers `prescriptions`.
- `product_name` : nom du médicament.
- `dose` : dosage.
- `frequency` : fréquence de prise.
- `duration` : durée du traitement.
- `quantity` : quantité.
- `notes` : observation.

### 13. `lab_tests`
Catalogue des examens ou analyses demandés.

Champs:
- `id` : clé primaire.
- `name` : nom de l'examen.
- `description` : précision.
- `category` : biologie, imagerie, autre.

### 14. `lab_orders`
Ordres d'examens demandés pour une consultation.

Champs:
- `id` : clé primaire.
- `encounter_id` : référence vers `encounters`.
- `lab_test_id` : référence vers `lab_tests`.
- `requested_by` : utilisateur demandeur.
- `order_date` : date de demande.
- `status` : demandé, en cours, terminé, annulé.

### 15. `lab_results`
Résultats des examens.

Champs:
- `id` : clé primaire.
- `lab_order_id` : référence vers `lab_orders`.
- `result_text` : résultat textuel.
- `result_file_url` : fichier joint si nécessaire.
- `validated_by` : utilisateur validateur.
- `validated_at` : date de validation.

### 16. `audit_logs`
Journalise les accès et modifications.

Champs:
- `id` : clé primaire.
- `user_id` : utilisateur auteur de l'action.
- `entity_type` : type d'objet affecté, par exemple patient, consultation.
- `entity_id` : identifiant de l'objet.
- `action` : lecture, création, modification, suppression.
- `details` : description de l'action.
- `created_at` : date et heure.

## Relations principales
- Un `role` peut être lié à plusieurs `users`.
- Un `facility` peut avoir plusieurs `users`.
- Un `patient` peut avoir plusieurs `patient_identifiers`.
- Un `patient` peut avoir plusieurs `medical_histories`.
- Un `patient` peut avoir plusieurs `encounters`.
- Un `encounter` peut avoir plusieurs `diagnoses`.
- Un `encounter` peut avoir une ou plusieurs `prescriptions`.
- Une `prescription` peut avoir plusieurs `prescription_items`.
- Un `encounter` peut avoir plusieurs `lab_orders`.
- Un `lab_order` peut avoir un ou plusieurs `lab_results` selon le besoin.
- Un `patient` peut avoir plusieurs `patient_allergies`.
- Chaque action importante doit apparaître dans `audit_logs`.

## Contraintes recommandées
- `patient_code` doit être unique.
- `email` doit être unique dans `users`.
- Les clés étrangères doivent être indexées.
- Les colonnes de recherche fréquente doivent être indexées, notamment `last_name`, `first_name`, `phone`, `patient_code`, `national_id_number`.
- Les suppressions physiques doivent être limitées; privilégier l'archivage.

## Schéma simplifié de départ
Si tu veux une première version très simple, commence avec ces tables seulement:
- `roles`
- `users`
- `facilities`
- `patients`
- `medical_histories`
- `encounters`
- `diagnoses`
- `prescriptions`
- `prescription_items`
- `audit_logs`

## Exemple logique de flux
1. Un utilisateur se connecte.
2. Il recherche un patient par nom ou téléphone.
3. Il ouvre le dossier du patient.
4. Il crée une consultation.
5. Il ajoute un diagnostic.
6. Il ajoute une prescription.
7. L'action est enregistrée dans le journal.

## Recommandation de mise en œuvre
Pour la première version, il est conseillé de créer le schéma SQL dans une base PostgreSQL, puis d'ajouter les index nécessaires à la recherche rapide. Ensuite, il faudra développer l'API backend avant l'interface utilisateur.
