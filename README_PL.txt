FGO TRACKER – PWA NA TELEFON
Wersja: 1.0.4

CO ZNAJDZIESZ W PACZCE
- index.html – samodzielna aplikacja (ma wbudowane CSS, JavaScript i początkowe JSON-y)
- styles.css, app.js – osobne kopie źródłowe do późniejszej edycji
- manifest.webmanifest, sw.js, icons/ – instalacja PWA i działanie offline
- fgo_database.json – baza Servantów, materiałów i kosztów rozwoju
- fgo_save.json – początkowy zapis postępów i ekwipunku
- fgo_database_oberon.json – przykładowa baza do testowania kosztów Oberona

URUCHAMIANIE
Plik index.html zawiera wbudowane style, skrypt aplikacji i początkowe dane JSON.
Można go otworzyć bezpośrednio z folderu, aby testować aplikację. Instalacja jako PWA
oraz pewne działanie offline wymagają umieszczenia folderu na hostingu HTTPS.

INSTALACJA NA ANDROIDZIE
1. Otwórz adres HTTPS aplikacji w Chrome.
2. Poczekaj, aż strona załaduje się przynajmniej raz.
3. W menu Chrome wybierz „Zainstaluj aplikację” albo „Dodaj do ekranu głównego”.
4. Aplikacja pojawi się jako ikona na ekranie.

DANE I KOPIE ZAPASOWE
Dane są zapisywane lokalnie w IndexedDB, z próbą użycia localStorage, gdy IndexedDB
jest niedostępne. Aplikacja nie wysyła postępów ani ekwipunku na serwer.
- fgo_database.json: nazwy Servantów, klasy, rzadkość, materiały i koszty.
- fgo_save.json: poziomy, NP, poziomy trzech Skillów, Ascension, ekwipunek, Pure Prisms,
  Embers i ostatnio wybrany widok.

Import bazy gry nie nadpisuje zapisu postępów. Import zapisu nie nadpisuje bazy gry.
Eksportuj regularnie oba pliki, szczególnie przed czyszczeniem danych przeglądarki
lub zmianą urządzenia.

KOSZTY ROZWOJU
Aplikacja pokazuje osobne kafelki dla najbliższego nieukończonego Ascension oraz
następnego poziomu każdego z trzech Skillów. „Łącznie” sumuje tylko te najbliższe
ulepszenia.

Na samym dole znajduje się dodatkowe „Łącznie za wszystko”: suma wszystkich
pozostałych materiałów potrzebnych do 4/4 Ascension i 10/10/10. Cel poziomu postaci
to maksymalny poziom bez Graala (np. Lv. 90 dla 5★). Tracker nie wylicza ilości kart
EXP ani QP. Obie sumy zmieniają się wraz z aktualnym postępem postaci.

QP i Append Skills nie są śledzone. Starsze pliki zapisu mogą nadal zawierać te pola,
ale aplikacja je ignoruje i usuwa z nowego eksportu.

FORMAT KOSZTÓW W BAZIE – SCHEMA 1
Każdy Servant może zawierać:
{
  "id": "oberon",
  "name": "Oberon",
  "class": "Pretender",
  "rarity": 5,
  "skill_names": ["Evening Shroud EX", "Morning Lark EX", "Ending of Dreams EX"],
  "costs": {
    "ascension": [
      {"materials": {"void_dust": 10}}, null, null, null
    ],
    "skills": [
      [
        {"from": 1, "to": 2, "materials": {"seed_of_yggdrasil": 10}}
      ],
      [], []
    ],
    "level_up": []
  }
}

LEVELOWANIE POSTACI
- Docelowy limit poziomu to maksymalny poziom bez Graala, zależny od rzadkości.
- Aplikacja nie wylicza ani nie pokazuje ilości kart EXP potrzebnych do levelowania.
- Materiały Ascension i Skill są liczone osobno; Append Skills oraz QP są pomijane.

NAWIGACJA
Przycisk Wstecz telefonu oraz „Wróć do menu” korzystają z historii widoków aplikacji.
W szczegółach Servanta wracają do menu, a z ekranu ekwipunku lub ustawień do menu.
Cztery przyciski Ascension są sekwencyjne: zaznaczenie etapu zaznacza wcześniejsze,
a odznaczenie etapu usuwa go i wszystkie późniejsze. Limit poziomu wyświetlany przy
postaci aktualizuje się na tej podstawie; sam faktyczny poziom nadal wpisuje się ręcznie.

FUNKCJE
- Menu Servantów z wyszukiwaniem.
- Szczegóły postaci, poziom, NP, Ascension, trzy skille i notatka.
- Koszty najbliższych ulepszeń jako osobne kafelki oraz osobna suma pozostałych materiałów do fulla.
- Ekwipunek materiałów, Pure Prisms i Emberów.
- Dodawanie Servanta bez ręcznej edycji JSON.
- Automatyczny lokalny zapis oraz osobny import/eksport bazy i postępów.
- Nawigacja przyciskiem Wstecz Androida.


Zmiany w v1.0.3:
- Koszty Ascension pokazują tylko najbliższy nieukończony etap.
- Każdy Skill pokazuje osobno materiały potrzebne do następnego poziomu.
- „Łącznie” sumuje najbliższe ulepszenia.
- Usunięto z widoku postaci panel „Poziom i NP”; wcześniejsze dane pozostają w pliku zapisu dla zgodności.

Zmiany w v1.0.4:
- Dodano na dole „Łącznie za wszystko” – pozostałe materiały do 4/4 Ascension i 10/10/10.
- Suma uwzględnia aktualne postępy i pomija już ukończone etapy/poziomy.
- Nie wylicza ilości kart EXP, QP ani materiałów do Append Skills.
