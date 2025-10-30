
## **Product Requirements Document (PRD): Aplikacja do Adnotacji Danych Time-Series i Ruchu Obiektów**

### **1. Wprowadzenie i Cel Produktu**

**1.1. Wprowadzenie**
Niniejszy dokument opisuje wymagania dla zaawansowanej aplikacji webowej i mobilnej umożliwiającej wizualizację i adnotowanie różnych typów danych zależnych od czasu. Aplikacja obsługuje trzy główne tryby danych:
1.  Klasyczne szeregi czasowe (1D), np. dane z sensorów temperatury, ciśnienia.
2.  Ruch obiektów w przestrzeni dwuwymiarowej (2D), np. pojazdy na magazynie, maszyny w kopalni.
3.  Ruch obiektów w przestrzeni trójwymiarowej (3D), np. rozpływy strug odstawy urobku, ramiona robotów, drony.

Celem jest dostarczenie uniwersalnego narzędzia, które pozwala ekspertom na intuicyjne oznaczanie i opisywanie kluczowych zdarzeń, przekształcając surowe dane w ustrukturyzowany dziennik zdarzeń (event log) gotowy do analizy w procesach process mining.

**1.2. Cel Produktu**
Stworzenie platformy mostującej lukę między trudnymi do interpretacji danymi a zrozumiałymi, analitycznymi wynikami. Aplikacja ma zautomatyzować i ułatwić proces tworzenia dzienników zdarzeń poprzez interaktywne adnotacje, niezależnie od tego, czy dane dotyczą pojedynczej wartości w czasie, czy złożonego ruchu obiektu.

**1.3. Problem do Rozwiązania**
Analiza procesów opartych na danych czasowych i przestrzennych jest trudna i czasochłonna. Eksperci muszą ręcznie przeglądać wykresy i mapy, co jest podatne na błędy i nie pozwala na efektywne identyfikowanie wzorców. Brakuje zintegrowanego narzędzia obsługującego różne typy danych wizualnych w jednym miejscu.

### **2. Użytkownicy Docelowi**

*   **Analityk Procesów / Inżynier Danych:** Osoba analizująca dane z sensorów przemysłowych, logów systemowych w celu optymalizacji procesów biznesowych.
*   **Inżynier Górniczy / Kierownik Zmiany:** Specjalista nadzorujący pracę maszyn w kopalni, analizujący wydajność i przestoje.
*   **Inżynier Robotyki / Automatyk:** Osoba projektująca i optymalizująca trajektorie robotów przemysłowych.
*   **Analityk Logistyczny:** Menedżer optymalizujący przepływ towarów i ruch pojazdów w magazynach lub na terenie fabryki.
*   **Badacz / Inżynier R&D:** Osoba badająca zjawiska fizyczne, chemiczne czy techniczne, wymagająca kategoryzacji faz eksperymentu.

### **3. Wymagania Funkcjonalne**

**3.1. Zarządzanie Danymi i Projektami**
*   **FR-001: Użytkownik może utworzyć nowy "projekt" adnotacji.**
*   **FR-002: Użytkownik może załadować dane do projektu poprzez wczytanie pliku (np. CSV, JSON). Aplikacja automatycznie rozpoznaje typ danych (1D, 2D, 3D) na podstawie kolumn.**
*   **FR-003: Aplikacja wyświetla dane w odpowiednim trybie wizualnym (wykres, widok 2D, widok 3D), pobierając je z bazy InfluxDB.**
*   **FR-004: Wszystkie widoki muszą wspierać podstawowe interakcje: przybliżanie (zoom), oddalanie i przesuwanie (pan).**

**3.2. Wspólny Mechanizm Adnotacji**
*   **FR-005: Adnotacja Zakresu (Range):** Użytkownik może wskazać zakres czasu (na osi czasu, ścieżce obiektu) poprzez technikę **drag and drop**.
*   **FR-006: Adnotacja Punktu (Point):** Użytkownik może wskazać pojedynczy punkt poprzez **kliknięcie**. W formularzu adnotacji, pola "Początek Zdarzenia" i "Koniec Zdarzenia" zawierają **identyczną wartość czasu**.
*   **FR-007: Ręczne Adnotacje Wizualne:** Użytkownik może rysować na płótnie (we wszystkich trybach) strzałki i obszary z etykietami tekstowymi. Są one czysto wizualne i nie są eksportowane.

**3.3. Adnotacja Danych Time-Series (1D)**
*   **FR-008: Aplikacja wyświetla dane na interaktywnym wykresie liniowym.**
*   **FR-009: Użytkownik może tworzyć adnotacje zakresu i punktu bezpośrednio na wykresie.**

**3.4. Adnotacja Ruchu Obiektów (2D)**
*   **FR-010: Aplikacja wyświetla interaktywne płótno 2D z animowanymi ścieżkami ruchu obiektów.**
*   **FR-011: Użytkownik może definiować obszary zainteresowania (prostokąty, wielokąty) i tworzyć adnotacje związane z wejściem/wyjściem obiektów z tych obszarów.**
*   **FR-012: Użytkownik może klikać na ścieżkę obiektu, aby utworzyć adnotację punktową związaną z tym obiektem w danym czasie.**

**3.5. Adnotacja Ruchu Obiektów (3D)**
*   **FR-013: Aplikacja wyświetla interaktywną scenę 3D z pełną kontrolą kamery (rotacja, pan, zoom).**
*   **FR-014: Użytkownik może definiować objętości zainteresowania (sześciany, sfery) i tworzyć adnotacje związane z przebywaniem obiektów w tych objętościach.**
*   **FR-015: Użytkownik może włączyć projekcję 2D (np. na płaszczyznę XY) w trybie 3D, aby ułatwić adnotacje.**

**3.6. Tabela Zdarzeń i Eksport**
*   **FR-016: W interfejsie aplikacji znajduje się tabela wyświetlająca wszystkie utworzone adnotacje ze wszystkich trybów.**
*   **FR-017: Tabela jest indywidualnie konfigurowalna dla każdego projektu (możliwość dodawania niestandardowych kolumn).**
*   **FR-018: Użytkownik może wyeksportować dane z tabeli zdarzeń do formatu CSV, zgodnego z wymaganiami process mining.**

### **4. Wymagania Niefunkcjonalne**

*   **NF-001: Wydajność:** Aplikacja musi płynnie renderować wykresy (do 100k punktów) i animacje 2D/3D (do 20 obiektów) na standardowym sprzęcie.
*   **NF-002: Responsywność:** Interfejs użytkownika musi być w pełni responsywny i użyteczny na urządzeniach desktopowych i przenośnych.
*   **NF-003: Użyteczność (Usability):** Interfejs musi być intuicyjny, a przełączanie między trybami (1D, 2D, 3D) proste i spójne.
*   **NF-004: Bezpieczeństwo:** Dostęp do projektów i danych jest chroniony przez system logowania. Komunikacja z bazami danych jest zabezpieczona.

### **5. Założenia Techniczne i Architektura**

*   **Frontend:** **Flutter**. Aplikacja kompilowana do postaci webowej oraz natywnej na Androida/iOS.
*   **Backend:**
    *   **Appwrite:** Do zarządzania użytkownikami, metadanymi projektów, konfiguracją tabel i zapisem adnotacji.
    *   **InfluxDB:** Do wydajnego przechowywania i query'owania surowych danych time-series i o położeniu obiektów.
*   **Integracja:** Komunikacja z InfluxDB odbywa się poprzez **Appwrite Functions**, które działają jako bezpieczna warstwa pośrednicząca.
*   **Deployment:** Całość (aplikacja Flutter, Appwrite, InfluxDB) jest uruchamiana za pomocą **Podman** przy użyciu pliku `docker-compose.yml`.

### **6. Model Danych**

#### **6.1. Struktura Danych w InfluxDB**

Dane są przechowywane w oddzielnych `measurements` dla każdej modalności:
*   **`sensor_data` (1D):** `sensor_data,sensor_id=TLM01 temperature=23.5 1630424257000000000`
*   **`object_position_2d` (2D):** `object_position_2d,object_id=shearer_01 x=150.5,y=25.8 1678886400000000000`
*   **`object_position_3d` (3D):** `object_position_3d,object_id=robot_arm_01 x=10.5,y=25.3,z=5.1 1630424257000000000`

#### **6.2. Kolekcje w Appwrite**

1.  **`projects`**: Metadane projektów, powiązanie z bucketem InfluxDB.
2.  **`annotations`**: Ujednolicona tabela zdarzeń.
    *   `annotationId`, `projectId`, `startTime`, `endTime`, `description`, `attributes` (Map).
    *   `objectId` (String, nullable): ID obiektu.
    *   `annotationType` (String, enum): 'range_on_series', 'point_on_series', 'object_event_2d', 'area_event_2d', 'object_event_3d', 'volume_event_3d'.
3.  **`spatial_areas`**: Definicje obszarów/objętości 2D/3D.
    *   `areaId`, `projectId`, `name`, `type` ('rectangle', 'polygon', 'cube', 'sphere'), `coordinates` (JSON).
4.  **`tableConfigurations`**: Konfiguracja kolumn tabeli zdarzeń dla projektu.

### **7. Scenariusze Użycia (User Stories)**

*   **Jako analityk procesów, chcę wczytać plik CSV z danymi z czujników temperatury (1D), aby oznaczyć fazy nagrzewania i chłodzenia w procesie produkcyjnym.**
    1.  Tworzę projekt, wgrywam plik `temp_data.csv`.
    2.  Aplikacja wyświetla wykres liniowy.
    3.  Przeciągam myszą po obszarze rosnącej temperatury, tworzę adnotację "Faza: Nagrzewanie".
    4.  Eksportuję tabelę zdarzeń do narzędzia process mining.

*   **Jako inżynier górniczy, chcę przeanalizować cykl pracy kombajnu ścianowego (2D), aby zrozumieć przyczyny przestojów.**
    1.  Ładuję dane telemetryczne kombajnu (`object_id: KS-01`, `x`, `y`).
    2.  Na płótnie 2D widzę ścieżkę kombajnu wzdłuż ściany.
    3.  Definiuję obszar "Strefa Cięcia" i "Strefa Manewrowa".
    4.  Klikam na ścieżkę w miejscu postoju, tworzę adnotację "Postój - awaria hydrauliki".
    5.  System automatycznie tworzy adnotacje przy każdym wejściu do "Strefy Manewrowej".
    6.  Analizuję tabelę i dowiaduję się, że manewry zajmują 35% czasu cyklu.

*   **Jako inżynier robotyki, chcę przeanalizować ruch ramienia robota (3D), aby zoptymalizować jego ścieżkę.**
    1.  Ładuję dane z enkoderów robota (`x`, `y`, `z`).
    2.  W trybie 3D odtwarzam cykl pracy robota.
    3.  Definiuję sześcian wokół stacji spawalniczej jako "strefę zakazaną".
    4.  System automatycznie flaguje momenty, w których narzędzie weszło do tej strefy.
    5.  Tworzę adnotację "Błąd trajektorii" i eksportuję dane do dalszej optymalizacji.

### **8. Kryteria Akceptacji**

*   **Dla FR-002:** **Gdy** użytkownik wczyta plik, **wtedy** aplikacja poprawnie identyfikuje jego typ (1D/2D/3D) i wyświetla dane w odpowiednim widoku.
*   **Dla FR-006:** **Gdy** użytkownik kliknie w punkt na wykresie/ścieżce, **wtedy** formularz adnotacji ma pola "Początek" i "Koniec" wypełnione tą samą wartością.
*   **Dla FR-011:** **Gdy** inżynier zdefiniuje "Strefę Cięcia" dla kombajnu, **wtedy** system poprawnie oblicza i wyświetla procent czasu, jaki kombajn spędził wewnątrz tego obszaru.
*   **Dla FR-015:** **Gdy** użytkownik jest w trybie 3D, **wtedy** może włączyć projekcję 2D i utworzyć na niej adnotację, która zostanie poprawnie powiązana z danymi 3D.
*   **Dla Wdrożenia:** **Gdy** deweloper uruchomi `podman-compose up --build`, **wtedy** cały system (Appwrite, InfluxDB, aplikacja) uruchamia się poprawnie i jest dostępny pod zdefiniowanym adresem.

### **9. Załącznik: Fragment `docker-compose.yml`**

```yaml
version: '3.8'

services:
  appwrite:
    image: appwrite/appwrite:latest
    container_name: appwrite
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./appwrite/data:/var/run/appwrite
      - ./appwrite/config:/usr/local/etc/appwrite
    environment:
      - _APP_ENV=development
      - _APP_OPENSSL_KEY_V1=your-secret-key
    depends_on:
      - influxdb

  influxdb:
    image: influxdb:2.7
    container_name: influxdb
    ports:
      - "8086:8086"
    volumes:
      - influxdb-data:/var/lib/influxdb2
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=passwordpassword
      - DOCKER_INFLUXDB_INIT_ORG=my-org
      - DOCKER_INFLUXDB_INIT_BUCKET=my-bucket
      - DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=my-super-secret-auth-token

  flutter-app:
    build: ./flutter-app
    container_name: flutter-app
    ports:
      - "3000:3000"
    depends_on:
      - appwrite

volumes:
  influxdb-data:
```


