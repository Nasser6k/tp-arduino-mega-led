# TP Arduino MEGA 2560 — LED & Bouton-poussoir

**Auteur :** Ahamada Nasser  
**Classe :** BTS CIEL ER  

---

## 1. Objectif du TP

L’objectif de cette manipulation est de prendre en main la carte microcontrôleur **Arduino MEGA 2560** à travers 3 étapes progressives :

1. Réaliser l’allumage permanent d’une LED.
2. Programmer un clignotement continu à intervalle régulier.
3. Associer un bouton-poussoir pour déclencher un clignotement d’une durée exacte de 5 secondes après une pression.

---

## 2. Matériel utilisé, câblage et logiciel

### Matériel
* **Carte Arduino MEGA 2560** : Carte de développement à microcontrôleur.
* **LED rouge** : Reliée à la broche numérique `13` et à la masse (`GND`).
* **Résistance de protection (220 Ω)** : Connectée en série avec la LED pour limiter le courant.
* **Bouton-poussoir** : Connecté entre la broche numérique `2` et la masse (`GND`).
* **Breadboard et câbles de connexion** : Pour le câblage du circuit.

### Chaîne logicielle (Arduino IDE)
1. Lancer l’**Arduino IDE** sur l’ordinateur.
2. Brancher la carte Arduino MEGA 2560 via le câble USB.
3. Dans **Outils > Type de carte**, sélectionner **Arduino Mega or Mega 2560**.
4. Saisir le code dans l’éditeur.
5. Téléverser le code sur la carte et observer le résultat.

---

## 3. Expérimentations et codes sources

### 3.1 Étape 1 : Allumage simple et permanent de la LED

Cette première phase permet de vérifier la validité du câblage de la LED et de prendre en main la fonction `pinMode()`.

```cpp
const int LED_PIN = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, HIGH);
}

void loop() {
}

