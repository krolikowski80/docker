# Wyjaśnienie pliku docker-compose.yml

Plik `docker-compose.yml` definiuje konfigurację aplikacji wielokontenerowej. W naszym przypadku opisuje dwa serwisy: `backend` (serwer aplikacji) i `db` (baza danych PostgreSQL).

## Struktura pliku

### Nagłówek wersji
```yaml
version: '3.8'
```
- **`version`**: Określa wersję formatu pliku Docker Compose. Wersja `3.8` jest jedną z najnowszych, wspierających zaawansowane funkcje.

### Sekcja `services`
```yaml
services:
```
- **`services`**: Klucz główny, pod którym definiowane są poszczególne usługi (kontenery).

---

## Wyjaśnienie serwisów

### 1. Serwis `backend`
```yaml
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - db
```
#### Szczegóły:
- **`backend`**: Nazwa usługi (dowolna, ale powinna być czytelna).
- **`build`**: Określa lokalizację pliku `Dockerfile`, który będzie użyty do budowy obrazu. W naszym przypadku to folder `./backend`.
- **`ports`**: Mapowanie portów pomiędzy kontenerem a hostem.  
  - `3000:3000`: Port `3000` na hoście (twoim komputerze) jest mapowany na port `3000` w kontenerze.
- **`depends_on`**: Określa zależności między usługami.  
  - `backend` wymaga, aby `db` zostało uruchomione jako pierwsze.

---

### 2. Serwis `db`
```yaml
  db:
    image: postgres:13
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
```
#### Szczegóły:
- **`db`**: Nazwa usługi.
- **`image`**: Określa obraz Dockera, który zostanie użyty. W tym przypadku jest to oficjalny obraz PostgreSQL w wersji `13`.
- **`environment`**: Zestaw zmiennych środowiskowych przekazywanych do kontenera.
  - **`POSTGRES_USER`**: Nazwa użytkownika bazy danych (w naszym przypadku: `postgres`).
  - **`POSTGRES_PASSWORD`**: Hasło dla użytkownika bazy danych (w naszym przypadku: `password`).

---

## Dodatkowe informacje

### Cały plik
```yaml
version: '3.8'
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - db
  db:
    image: postgres:13
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
```

### Co robi ten plik?
1. Buduje obraz Dockera dla backendu na podstawie pliku `Dockerfile` w folderze `./backend`.
2. Uruchamia dwa kontenery:
   - Backend na porcie `3000`.
   - Bazę danych PostgreSQL.
3. Automatycznie ustawia zależność: backend uruchamia się po bazie danych.

### Jak uruchomić plik?
- Aby uruchomić aplikację, użyj:
  ```bash
  docker-compose up
  ```
- Aby uruchomić w tle:
  ```bash
  docker-compose up -d
  ```

### Jak zatrzymać aplikację?
- Użyj:
  ```bash
  docker-compose down
  ```

## Debugowanie
- Aby sprawdzić logi wszystkich usług:
  ```bash
  docker-compose logs
  ```
- Aby sprawdzić logi konkretnej usługi (np. `backend`):
  ```bash
  docker-compose logs backend
  ```

## Podsumowanie
Plik `docker-compose.yml` upraszcza zarządzanie aplikacją wielokontenerową, umożliwiając definiowanie i uruchamianie wszystkich usług za pomocą jednej komendy.
"""

# Zapisanie pliku
with open(md_file_path, "w") as file:
    file.write(docker_compose_explanation_content)

md_file_path