# Projekt-przetwornika-cyfrowo-analogowego-C-A-typu-R-R2
Przetwornik jest 4 bitowy, dwu kanałowy. Stwożony do wyświetlania prostych obrazów i animacji na oscyloskopie. Przetfornik dysponuje 16 stanami napięcia od 0-15 na 2 kanałach X oraz Z, co umożliwia tworzenie prostych obrazów i animacji na np. oscyloskopie. 256x256. 

Projekt składa się z:
- 1x Płytka Arduino Uno,
- 10x Rezystor 10K Omów
- 6x Rezystor 4.7K Omów
- Kabelki połączeniowe.

Schemat połączenia: <img width="1386" height="695" alt="1" src="https://github.com/user-attachments/assets/e6b51923-950d-42ba-a704-11dec816ac41" /> (Schemat wykonany za pomocą https://www.tinkercad.com/)
<br>

<h6>W tym repozytorium znajdują się skrypty, które wyświetlają obrazy na oscyloskopie</h6>
Przykład:
Ten skrypt wyświetla kwadrat.
<code>
const int pinX[] = {2, 3, 4, 5};
const int pinY[] = {8, 9, 10, 11};

void setup() {
  for (int i = 0; i < 4; i++) {
    pinMode(pinX[i], OUTPUT);
    pinMode(pinY[i], OUTPUT);
  }
}

void ustawNapiecieX(int wartosc) {
  for (int bit = 0; bit < 4; bit++) {
    digitalWrite(pinX[bit], (wartosc >> bit) & 1);
  }
}

void ustawNapiecieY(int wartosc) {
  for (int bit = 0; bit < 4; bit++) {
    digitalWrite(pinY[bit], (wartosc >> bit) & 1);
  }
}

void loop() {
  for (int x = 0; x <= 15; x++) {
    ustawNapiecieX(x);
    ustawNapiecieY(0);
    delayMicroseconds(50);
  }

  for (int y = 0; y <= 15; y++) {
    ustawNapiecieX(15);
    ustawNapiecieY(y);
    delayMicroseconds(50);
  }

  for (int x = 15; x >= 0; x--) {
    ustawNapiecieX(x);
    ustawNapiecieY(15);
    delayMicroseconds(50);
  }

  for (int y = 15; y >= 0; y--) {
    ustawNapiecieX(0);
    ustawNapiecieY(y);
    delayMicroseconds(50);
  }
}
