# Sniper

## Strzelanie: Karta balistyczna

!!! info "Karta balistyczna"
    Otwórz Kartę, by poznać korektę, jaką masz ustawić na celowniku.

## Strzelanie: Komputer AtraGMX

### Wprowadzanie danych broni do Atragmx

Możesz wprowadzić dane z Arsenału i Karty balistycznej i prawdopodobnie trafisz w centrum masy na 1000m z lekką korektą.

Idealne ustawienie snajperki wymaga odczytania surowych danych z gry i truing'u broni na strzelnicy w specjalnych warunkach pogodowych.

* Prędkość pocisku jest zależna od długości lufy. Więc nie znasz prędkości pocisku.
* C1/G7 jest zależne od tego, co twórca moda wyczytał w swoim ulubionym magazynie o broniach i nie ma nic wspólnego z prawdą.
* Zachowanie pocisku jest nieznane, bo czasem pocisk z modów ma wewnętrzną tabelę z danymi, czasem nie.
* Czasem dane na temat pocisku mogą być w kilku miejscach (prędkość pocisku nie jest w klasie pocisku ani broni).

!!! warning "Uwaga"
    Dlatego **truing** jest niezbędny do precyzyjnego ustawienia komputera.

**W skrócie sposób wygląda tak:**

1. Załaduj dane do Atragmx przy użyciu magicznego skryptu `.sqf`.
2. Zweryfikuj dane.
3. Uruchom Ace Arsenal, uruchom magiczny skrypt blokujący wszystkie efekty pogodowe.
4. Skalibruj broń na 500, 1000, 2000m, albo 500, `Transonic_distance + (Transonic_distance - Subsonic_distance) * 0.75` (pętla):
    * Na danej odległości zmierz **Elev** Atragmx i nastaw lunetę.
    * Strzelaj i koryguj *elev*, aż zaczniesz trafiać dokładnie w cel.
    * Nie przegrzewaj broni albo rotuj lufy.
    * Po znalezieniu idealnego *elev* (w lunecie):
        * Otwórz **Options -> Drag Coef Table**.
        * Wprowadź dystans i NOWY zmyślony BC-coef (C1/G7), który przybliży korektę *elev* do twojej idealnej na lunecie.
        * Jak *elev* na Atragmx będzie się zgadzał z korektą lunety, przejdź do korygowania kolejnego dystansu.

---

### Protokół przygotowania się do oddania strzału w cel

#### Przed misją

* Zbuduj sobie pełny loadout postaci snajpera.
* Wprowadź dane broni i amunicji do komputera Atragmx. **Skalibruj Atragmx!**
* Załaduj mapę, na której będziesz grał:
    * postaw żołnierza, 
    * uruchom misję,
    * w debug console wpisz w watchlist polecenie `ace_common_maplatitude`,
    * odczytaj i zapisz szerokość geograficzną na boku.

#### Przed udaniem się na lokację

* Jeśli masz w plecaku **microDAGR**, musisz:
    * kliknąć w nim górny pasek,
    * kliknąć "connect to", tak żeby na górze była ikonka połączenia Atragmx i Kestrel.
* Jeśli nie masz microDAGR, **Kestrel** jest połączony z Atragmx.
* W Kestrelu wprowadź szerokość geograficzną mapy w kolumnie **Target**.
* Załaduj swoją broń z **Gunlist**.
* Zweryfikuj ustawienia broni, czy nie ma błędów (tryb **D**). Porównaj z kartą.
* Sprawdź pogodę w Kestrel i wprowadź do Atragmx: temperatura, ciśnienie, wilgotność (tryb **M**).
* Możesz ustawić podgląd Kestrel'a na HUD, żeby śledzić wiatr w drodze.
* Zweryfikuj widoczność na potencjalnych punktach OBS, przy użyciu LOS(mod) na mapie (skrót **Q**).
* Ściągnij NVG/Thermo z lunety, jeśli trzeba.
* Skalibruj lunetę na 300m na wszelki wypadek.
* Upewnij się, że broń jest skalibrowana na 100m.

#### Na lokacji

1. Upewnij się, że OBS jest bezpieczny.
2. Zespotuj przeciwników.
3. Ustaw trójnóg, obniż go.
4. **Ustaw wiatr:**
    * Kliknij na tryb **M** (metryczny) w Atragmx.
    * Otwórz Kestrel i ustaw na **Headwind**.
    * Znajdź najmocniejszy wiatr w dogodnej lokacji (bez przeszkód, nie na zboczu).
    * Zanotuj kierunek najmocniejszego wiatru.
    
    === "Metoda Headwind"
        * Jeśli wprowadzasz Headwind do Atragmx, zanotuj wartość wiatru (muszą być wartości dodatnie) (na razie crosswind jest pewniejszy).
        * Zanotuj minimalną i maksymalną wartość wiatru, jeśli są porywy.
        * Wprowadź wartości wiatru do **Target -> windspeed 1** (minimalny wiatr) i **2** (maksymalny wiatr).
        * Jeśli wiatr ma taką samą prędkość, wprowadzasz ją w obydwie rubryki 1 i 2.
        * W **wind direction** wprowadzasz godzinę, z której wieje wiatr, względem lufy skierowanej na cel (cel to 12).

    === "Metoda Crosswind"
        * Ustaw w Kestrel zakładkę **Crosswind**.
        * Wyceluj broń w Cel i ustaw Kestrel na auto-heading w tym kierunku.
        * Obróć się w zapamiętanym kierunku headwind.
        * Odczytaj crosswind (musi być dodatni).
        * Zapisz wartość crosswind do **Target -> wind speed 1** i **2**.
        * Wpisz **wind direction 3 lub 9** (Atragmx sam liczy `sin()`).
        * Jeśli patrząc na cel, kierunek wiatru jest po lewej stronie, wpisujesz **9**.
        * Inaczej wpisujesz **3** w wind direction (bo jest przy prawej rączce).

5. Sprawdź, czy zakładka **Atmsphr** wymaga aktualizacji danych pogodowych.
6. Użyj Vector'a i zrób odczyt pozycji celu(Tab+R)(kilka odczytów na duże odległości).
7. Upewnij się, że Atragmx na dole ma ustawioną miarę korekty taką jak luneta (98% to **MILs**).
8. Jeśli wprowadziłeś zakres wiatru, kliknij **LEAD**.
9. Wprowadź korekty lunety z komórek **Elev** i **Wind** (lub Wind2) w kolumnie **Hold**.
10. Nie pomyl kierunków kręcenia pokrętłem i sprawdź jeszcze raz czy nastaw się nie zresetował.
11. Brakujące ułamki w precyzji Atragmx musisz skorygować na lunecie (0.05R itp.).
12. **Gotowe! Możesz strzelać.**

---

## Dobre rady

!!! tip "Wskazówki operacyjne"
    * Używając broni MCC sprawdzaj co chwile kalibracje broni czy się nie zmieniła przypadkowo (`Ctrl` + `Scroll`).
    * Kiedy wbiegłeś na lokacje i musisz szybko oddać strzał - zażyj kawę (caffeine).

## Niezbędne przedmioty dla snajpera

* [x] Karta Balistyczna
* [x] Atragmx
* [x] Kestrel 4500W
* [x] Vector 21 Nite
* [x] Spare Barrel
* [x] SSWT Kit
* [x] Map Tools
* [x] Full Ghillie suit

## Materiały dodatkowe

* [Marksman/snajpa (Reddit)](https://www.reddit.com/r/arma/comments/14xi05y/does_anyone_have_an_atrag_gun_profile_already/)
* [Marksman Guide (Steam)](https://steamcommunity.com/sharedfiles/filedetails/?id=1078577824)
* [Instrukcja do lunet i praca ze spotterem (EN)](https://www.youtube.com/watch?v=GxhxcUkMeug)
* [Instrukcja dla lunet, w tym Tremor3 (YT)](https://www.youtube.com/watch?v=jJWbR8YTOlA)
* [Instrukcja Atragmx (ACE3 Wiki)](https://ace3.acemod.org/wiki/feature/atragmx#37-reseting-atragmx-gunlist)
* [Instrukcja video Atragmx (PL - PKW)](https://www.youtube.com/watch?v=cu82xzcMSlw)