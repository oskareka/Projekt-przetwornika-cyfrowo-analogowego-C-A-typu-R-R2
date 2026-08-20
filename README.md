# Projekt-przetwornika-cyfrowo-analogowego-C-A-typu-R-R2
Przetwornik jest 4 bitowy, dwu kanałowy. Stwożony do wyświetlania prostych obrazów i animacji na oscyloskopie. Przetfornik dysponuje 16 stanami napięcia od 0-15 na 2 kanałach X oraz Z, co umożliwia tworzenie prostych obrazów i animacji na np. oscyloskopie. 256x256. 

Po co?
Ogolnie da się na oscyloskopie wyświetlić jakiś obraz i da się to zrobić z arduino, więc pomyslalem że spróboje.

Jak to działa?
Arduino może nadawać tylko dwa typy sygnału o mocy 5V albo 0 albo 1. Arduino nie potrafi sterować napięciem, ale tworząc przetwornik możemy kontrolować moc sygnałua a to umożliwia nam wyświetlenie jakiegoś obrazu itd na oscyloskopie.

Projekt składa się z:
- 1x Płytka Arduino Uno,
- 10x Rezystor 10K Omów
- 6x Rezystor 4.7K Omów
- Kabelki połączeniowe.

Schemat połączenia: <img width="1386" height="695" alt="1" src="https://github.com/user-attachments/assets/e6b51923-950d-42ba-a704-11dec816ac41" /> (Schemat wykonany za pomocą https://www.tinkercad.com/)
<h6>W ramach sprostowania to <img width="81" height="29" alt="image" src="https://github.com/user-attachments/assets/52aef62e-f8ac-4420-a828-addfddd54bfe" />
 jest rezystor 10k Omów a to <img width="86" height="28" alt="image" src="https://github.com/user-attachments/assets/760fb902-7d58-4248-95ed-3a42392996d1" /> rezystor 4.7k Omów.

Ogolnie to niestety w środowisku tinkercad nie da się łądnie wcisnąć rezystorów więc te 4.7KOmów są na schemacie podłączone kabelkami, ale Ty w swoim projekcie masz je wczepić normalnie nóżkami w otwory na płytce stykowej. I na samym dole płytki stykowej tam gdzie jest masa GND to tak zgadza się rezystoryy 10KOmów idą z kanału 2 oraz z kanału 8 do GND. 

Pamietaj jeszcze, żeby wszystko było wcisnięte oraz rezystor nie dotykał rezystora.
</h6>


<br>

<h2>W tym repozytorium znajdują się skrypty, które wyświetlają obrazy na oscyloskopie</h2>
Przykład:
Ten skrypt wyświetla kwadrat.

```cpp
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
