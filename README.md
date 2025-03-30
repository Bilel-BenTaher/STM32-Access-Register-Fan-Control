
# Contrôle de Ventilateurs avec STM32F407VGT6 via Bluetooth

Ce projet utilise un microcontrôleur STM32F407VGT6 pour lire les valeurs d'un potentiomètre via ADC et les utiliser pour commander des ventilateurs via des signaux PWM. Les données sont envoyées à un smartphone via une communication Bluetooth, et un bouton permet d'activer ou de désactiver le système. **Le code est écrit en utilisant l'accès direct aux registres** du microcontrôleur, sans l'utilisation de bibliothèques HAL ou CMSIS.

## Description

Le code configure le STM32F407VGT6 pour :
- Lire les valeurs des canaux ADC via un potentiomètre.
- Utiliser ces valeurs pour ajuster la vitesse des ventilateurs via PWM.
- Envoyer les valeurs des potentiomètres en temps réel vers un smartphone via USART.
- Utiliser un bouton externe pour activer ou désactiver le système.

### Fonctionnalités
- **Lecture ADC** : Trois canaux ADC sont utilisés pour lire les valeurs des potentiomètres.
- **Contrôle PWM** : Les valeurs ADC ajustent les rapports cycliques des signaux PWM qui contrôlent la vitesse des ventilateurs.
- **Communication Bluetooth** : Les valeurs des potentiomètres sont envoyées en temps réel via la communication USART2, qui peut être reliée à un module Bluetooth pour la communication avec un smartphone.
- **Interruption externe** : Un bouton externe (connecté à PA0) permet de démarrer ou d'arrêter le système en activant ou désactivant le Timer2.

## Architecture du système

- **STM32F407VGT6** : Microcontrôleur principal qui gère la lecture des valeurs ADC, le contrôle des ventilateurs (PWM), et la communication avec le smartphone via USART.
- **Potentiomètres** : Trois potentiomètres sont utilisés pour ajuster la vitesse des ventilateurs.
- **Bluetooth (module externe)** : Module Bluetooth connecté à l'USART pour envoyer les valeurs des potentiomètres au smartphone.
- **Bouton** : Connecté à la broche PA0 pour activer/désactiver le système.

## Schéma de connexion

- **ADC** : Les potentiomètres sont connectés aux broches PA1, PA4, et PA5.
- **PWM** : Les ventilateurs sont contrôlés par les broches PA6, PA7, et PB0.
- **Bluetooth** : Connecté à l'USART2 via les broches PA2 (TX) et PA3 (RX).
- **Bouton** : Connecté à la broche PA0.

## Prérequis

- Un environnement de développement pour STM32, tel que **CoIDE de CooCox**.
- Un module Bluetooth HC-06 pour la communication avec le smartphone.
- Un smartphone avec une application pour recevoir et afficher les valeurs envoyées par l'USART via Bluetooth.

## Fonctionnement

1. **Initialisation du système** : Le système configure l'horloge, les interruptions externes, l'ADC, le PWM, et la communication série via USART.
2. **Lecture des potentiomètres** : Les valeurs analogiques des potentiomètres sont lues via l'ADC et converties en valeurs numériques.
3. **Contrôle des ventilateurs** : Les valeurs des potentiomètres sont utilisées pour ajuster le rapport cyclique des signaux PWM, contrôlant ainsi la vitesse des ventilateurs.
4. **Envoi des données** : Les valeurs des potentiomètres sont envoyées via USART2 (et Bluetooth) vers un smartphone.
5. **Activation/Désactivation** : Le bouton connecté à PA0 active ou désactive le système en contrôlant le Timer2.

## Compilation et Téléversement

1. Ouvrir le projet dans **CoIDE de CooCox**.
2. Vérifier que les fichiers de configuration du microcontrôleur sont correctement configurés.
3. Compiler le projet.
4. Connecter le STM32F407VGT6 à votre PC via un programmateur ST-Link.
5. Téléverser le code sur le microcontrôleur.

## Interruption et gestion des périphériques

- **EXTI0_IRQHandler** : Gère l'interruption externe du bouton connecté à PA0 pour activer ou désactiver le Timer2.
- **ADC_IRQHandler** : Gère l'interruption ADC pour lire les valeurs des canaux ADC et ajuster les rapports cycliques PWM en fonction des valeurs lues.

## Vidéo de démonstration

https://github.com/user-attachments/assets/a498a18f-63ed-4e90-af50-f2f8e1c1f231




