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
```

**Explication :**  
La fonction `setup()` s’exécute une seule fois lors de la mise sous tension. L’instruction `digitalWrite(LED_PIN, HIGH)` applique 5 V sur la broche 13 : la LED reste allumée en continu.

---

### 3.2 Étape 2 : Clignotement automatique continu (Blink)

Cette deuxième étape introduit la gestion du temps via des temporisations logicielles.

```cpp
const int LED_PIN = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH); // Allume
  delay(1000);                 // Attend 1 seconde
  digitalWrite(LED_PIN, LOW);  // Éteint
  delay(1000);                 // Attend 1 seconde
}
```

**Explication :**  
La fonction `loop()` s’exécute en boucle infinie. L’instruction `delay(1000)` bloque le microcontrôleur pendant 1000 ms (1 s). L’alternance entre `HIGH` (5 V) et `LOW` (0 V) génère un cycle de clignotement régulier d’une période totale de 2 s (1 s + 1 s).

---

### 3.3 Étape 3 : Contrôle par bouton-poussoir et clignotement temporisé (5 s)

La phase finale combine l’acquisition d’une entrée numérique avec une structure itérative de comptage.

```cpp
const int LED_PIN = 13;
const int BOUTON_PIN = 2;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BOUTON_PIN, INPUT_PULLUP);
  digitalWrite(LED_PIN, LOW);
}

void loop() {
  if (digitalRead(BOUTON_PIN) == LOW) {
    for (int i = 0; i < 5; i++) {
      digitalWrite(LED_PIN, HIGH);
      delay(500);
      digitalWrite(LED_PIN, LOW);
      delay(500);
    }
  }
}
```

**Explication détaillée :**
* **Configuration `INPUT_PULLUP` :** Active la résistance de rappel interne de l’Arduino reliée au 5 V afin d'éviter une broche flottante (signal instable). Bouton relâché, l’état lu est `HIGH` (5 V) ; bouton appuyé, le courant s’écoule vers la masse et l’état passe à `LOW` (0 V).
* **Boucle `for (int i = 0; i < 5; i++)` :** La variable `i` démarre à `0` et s'incrémente de 1 (`i++`) à chaque tour.
* **Calcul de la temporisation :** Un tour de boucle dure exactement 1 seconde (`500 ms + 500 ms`). Comme la boucle s'exécute pour `i = 0, 1, 2, 3, 4`, elle effectue 5 tours, soit **5 × 1 s = 5 secondes** de clignotement. Dès que `i` atteint `5`, la boucle s'arrête et la LED reste éteinte.

---

## 4. Conclusion

Ce TP a permis de valider la maîtrise des fonctions de base de la programmation sous Arduino :
1. L’écriture sur les broches numériques de sortie (`digitalWrite`).
2. La gestion des délais d'attente (`delay`).
3. La configuration propre d'une entrée avec résistance de rappel interne (`INPUT_PULLUP`).
4. La création d'une temporisation précise grâce à une boucle `for` conditionnée par l'incrémentation `i++`.
