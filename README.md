# ChronoForge
# Aplikacja do Adnotacji Danych Time-Series i Ruchu Obiektów

Zaawansowane narzędzie do wizualizacji i adnotacji danych zależnych od czasu, wspierające analizę procesów (process mining). Aplikacja umożliwia pracę z trzema typami danych: szeregami czasowymi (1D), ruchem obiektów w 2D oraz ruchem obiektów w 3D.

## 📋 Spis Treści

1.  [Opis Projektu](#opis-projektu)
2.  [Kluczowe Funkcjonalności](#kluczowe-funkcjonalności)
3.  [Zastosowane Technologie](#zastosowane-technologie)
4.  [Struktura Projektu](#struktura-projektu)
5.  [Wymagania Wstępne](#wymagania-wstępne)
6.  [Jak Uruchomić Projekt](#jak-uruchomić-projekt)
7.  [Zmienne Środowiskowe](#zmienne-środowiskowe)
8.  [Architektura](#architektura)
9.  [Wkład w Projekt](#wkład-w-projekt)
10. [Licencja](#licencja)

## 🌟 Opis Projektu

Aplikacja pozwala użytkownikom na wczytywanie surowych danych (np. z sensorów, systemów telemetrycznych), ich interaktywną wizualizację oraz tworzenie adnotacji opisujących kluczowe zdarzenia. Wygenerowany w ten sposób ustrukturyzowany dziennik zdarzeń może być eksportowany do formatu CSV i wykorzystywany w narzędziach do analizy procesowej, takich jak Celonis czy Disco.

Projekt jest zbudowany z myślą o wszechstronności, obsługując zarówno proste dane z czujników, jak i złożone trajektorie ruchu maszyn w przestrzeni.

## ✨ Kluczowe Funkcjonalności

-   **Wizualizacja 1D:** Interaktywne wykresy liniowe dla danych szeregów czasowych.
-   **Wizualizacja 2D:** Animowany ruch obiektów na płaszczyźnie z możliwością definiowania obszarów zainteresowania.
-   **Wizualizacja 3D:** Pełny widok przestrzenny z kontrolą kamery i możliwością definiowania objętości.
-   **Interaktywne Adnotacje:** Tworzenie adnotacji punktowych i zakresowych za pomocą technik `drag-and-drop` oraz klikania.
-   **Tabela Zdarzeń:** Konfigurowalna tabela zbierająca wszystkie adnotacje, gotowa do eksportu.
-   **Eksport do CSV:** Generowanie plików zgodnych z wymaganiami process mining.
-   **Zarządzanie Użytkownikami:** Bezpieczne logowanie i zarządzanie projektami.

## 🛠️ Zastosowane Technologie

-   **Frontend:** [Flutter](https://flutter.dev/)
-   **Backend:** [Appwrite](https://appwrite.io/)
-   **Baza Danych (Time-Series):** [InfluxDB](https://www.influxdata.com/)
-   **Konteneryzacja:** [Podman](https://podman.io/) / Docker
-   **Język:** Dart

## 📁 Struktura Projektu

```
.
├── docker-compose.yml      # Definicja usług kontenerowych (Appwrite, InfluxDB)
├── flutter-app/            # Główna aplikacja Flutter
│   ├── lib/
│   │   ├── main.dart
│   │   ├── screens/        # Ekrany aplikacji
│   │   ├── widgets/        # Widżety reużywalne
│   │   └── services/       # Serwisy do komunikacji z API
│   ├── pubspec.yaml        # Zależności Flutter
│   └── ...
├── appwrite-functions/     # Funkcje serverless Appwrite (logika biznesowa)
│   └── ...
└── README.md
```

## 📦 Wymagania Wstępne

Upewnij się, że masz zainstalowane następujące oprogramowanie:

-   [Flutter SDK](https://flutter.dev/docs/get-started/install) (w wersji >= 3.0)
-   [Podman](https://podman.io/docs/installation) lub [Docker](https://www.docker.com/get-started/)
-   [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## 🚀 Jak Uruchomić Projekt

Postępuj zgodnie z poniższymi krokami, aby uruchomić aplikację w środowisku deweloperskim.

### 1. Sklonuj Repozytorium

```bash
git clone https://github.com/twoja-nazwa-uzytkownika/nazwa-projektu.git
cd nazwa-projektu
```

### 2. Uruchom Usługi Backendowe (Appwrite i InfluxDB)

Użyj pliku `docker-compose.yml`, aby zbudować i uruchomić kontenery Appwrite i InfluxDB w tle.

```bash
podman-compose up -d --build
```

Poczekaj kilka minut, aż wszystkie usługi zostaną w pełni zainicjowane.

### 3. Skonfiguruj Appwrite i InfluxDB (Jednorazowo)

1.  **Otwórz konsolę Appwrite:** Przejdź do [http://localhost](http://localhost) w przeglądarce.
2.  **Utwórz konto** i zaloguj się.
3.  **Stwórz nowy projekt.** Podczas tworzenia projektu Appwrite poda Ci `Project ID` oraz `Endpoint`. Będą one potrzebne do konfiguracji aplikacji Flutter.
4.  **Otwórz konsolę InfluxDB:** Przejdź do [http://localhost:8086](http://localhost:8086).
5.  **Zaloguj się** używając danych ustawionych w pliku `docker-compose.yml` (domyślnie: `admin` / `passwordpassword`).
6.  **W InfluxDB utwórz organizację (org) oraz bucket (np. `time-series-data`)**. Wygeneruj token API z uprawnieniami do odczytu/zapisu do tego bucketa.

### 4. Uruchom Aplikację Flutter

1.  Przejdź do katalogu z aplikacją:
    ```bash
    cd flutter-app
    ```
2.  Zainstaluj zależności:
    ```bash
    flutter pub get
    ```
3.  **Skonfiguruj połączenie z Appwrite:**
    - Stwórz plik `lib/constants/appwrite_constants.dart` (lub użyj pliku `.env`).
    - Wklej do niego dane zebrane w kroku 3:

    ```dart
    // lib/constants/appwrite_constants.dart
    class AppwriteConstants {
      static const String endpoint = 'http://localhost/v1';
      static const String projectId = 'TWOJ_PROJECT_ID';
      // Token API powinien być pobierany bezpiecznie, np. po zalogowaniu użytkownika
      // lub z poziomu funkcji Appwrite, a nie hardkodowany.
    }
    ```
4.  Uruchom aplikację:
    ```bash
    flutter run
    ```

Aplikacja powinna uruchomić się na Twoim urządzeniu lub w przeglądarce.

## ⚙️ Zmienne Środowiskowe

Aplikacja Flutter wymaga skonfigurowania stałych (zobacz krok 4) z następującymi wartościami:
-   `APPWRITE_ENDPOINT`: Adres URL instancji Appwrite (np. `http://localhost/v1`).
-   `APPWRITE_PROJECT_ID`: ID Twojego projektu w Appwrite.
-   `INFLUXDB_TOKEN` (opcjonalnie, do bezpośredniego połączenia): Token API do InfluxDB.

## 🏗️ Architektura

Aplikacja opiera się na architekturze trójwarstwowej:

1.  **Frontend (Flutter):** Odpowiada za interfejs użytkownika, wizualizację danych i interakcje.
2.  **Backend (Appwrite):** Zarządza uwierzytelnianiem, bazą danych metadanych (projekty, adnotacje) i przechowuje pliki. **Appwrite Functions** działają jako bezpieczna warstwa pośrednicząca, która komunikuje się z InfluxDB, chroniąc dane przed nieautoryzowanym dostępem.
3.  **Baza Danych (InfluxDB):** Wydajna, specjalistyczna baza danych do przechowywania i query'owania surowych danych szeregów czasowych i danych o położeniu.

**Przepływ danych:** `Flutter App` -> `Appwrite API / Functions` -> `InfluxDB`.

## 🤝 Wkład w Projekt

Chętnie przyjmiemy Twoje wkłady! Jeśli chcesz pomóc w rozwoju projektu:

1.  Stwórz `fork` tego repozytorium.
2.  Utwórz nową gałąź (`git checkout -b feature/AmazingFeature`).
3.  Zatwierdź swoje zmiany (`git commit -m 'Add some AmazingFeature'`).
4.  Wypchnij zmiany do swojego forka (`git push origin feature/AmazingFeature`).
5.  Otwórz `Pull Request`.

## 📄 Licencja

Ten projekt jest licencjonowany na warunkach licencji Apache 2.0. Szczegóły znajdziesz w pliku [LICENSE](LICENSE).

## 📧 Kontakt

Twoja Nazwa - [@twoj_twitter](https://twitter.com/twoj_twitter) - email@przyklad.com

Link do projektu: [https://github.com/twoja-nazwa-uzytkownika/nazwa-projektu](https://github.com/twoja-nazwa-uzytkownika/nazwa-projektu)
