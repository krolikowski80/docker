# Zadania z Dockerfile

## Zadanie 1: Tworzenie prostego obrazu z aplikacją Hello World
### Kroki:
1. Stwórz plik `Dockerfile`.
2. Użyj oficjalnego obrazu `alpine` jako podstawy.
3. Dodaj polecenie `CMD`, które wypisze "Hello World".

### Podpowiedzi:
- Skorzystaj z `FROM alpine` jako bazowego obrazu.
- Polecenie `CMD ["echo", "Hello World"]` wypisze tekst.

---

## Zadanie 2: Kontener z aplikacją Python
### Kroki:
1. Stwórz plik `Dockerfile`.
2. Użyj obrazu `python:3.9`.
3. Skopiuj plik `app.py` do kontenera.
4. Ustaw jako domyślne polecenie uruchamianie `python app.py`.

### Podpowiedzi:
- Plik `app.py` powinien znajdować się w tym samym katalogu co Dockerfile.
- Użyj instrukcji `COPY` i `CMD`.

---

## Zadanie 3: Tworzenie i montowanie wolumenu
### Kroki:
1. Stwórz `Dockerfile` używający `nginx`.
2. Utwórz wolumen, w którym znajdować się będą pliki statyczne.
3. Uruchom kontener z tym wolumenem.

### Podpowiedzi:
- W `docker run` dodaj flagę `-v` do montowania wolumenu.
- W `Dockerfile` użyj `VOLUME`.

---

## Zadanie 4: Docker Compose - aplikacja Node.js
### Kroki:
1. Stwórz plik `Dockerfile` dla aplikacji Node.js.
2. Stwórz plik `docker-compose.yml`, który uruchomi serwer Node.js i MongoDB.
3. Skonfiguruj połączenie między serwerem a bazą danych.

### Podpowiedzi:
- `docker-compose.yml` powinien zawierać sekcje `services`, `volumes` i `networks`.
- W `Dockerfile` dla Node.js zainstaluj zależności za pomocą `RUN npm install`.

---

## Zadanie 5: Zmniejszenie rozmiaru obrazu
### Kroki:
1. Utwórz obraz aplikacji Python korzystając z `python:3.9`.
2. Zoptymalizuj obraz, zmieniając bazowy obraz na `python:3.9-slim`.
3. Porównaj rozmiary obrazów.

### Podpowiedzi:
- Używaj tylko niezbędnych warstw i plików.
- Usuń zbędne pliki tymczasowe w ramach jednej warstwy.

---

## Zadanie 6: Budowanie obrazu z cache
### Kroki:
1. Stwórz `Dockerfile` dla aplikacji Node.js.
2. Dodaj `package.json` i `package-lock.json`.
3. Skonfiguruj Dockerfile, aby najpierw zbudować cache dla zależności.

### Podpowiedzi:
- Skopiuj `package.json` przed kopiowaniem kodu aplikacji.
- Użyj `RUN npm install` i `COPY . .`.

---

## Zadanie 7: Tworzenie wieloetapowego obrazu
### Kroki:
1. Stwórz aplikację w Node.js, która wymaga kompilacji frontendu.
2. W `Dockerfile` utwórz dwie fazy:
   - Budowanie frontendu.
   - Uruchamianie serwera w lekkim obrazie.

### Podpowiedzi:
- Skorzystaj z `AS` do oznaczania etapów.
- Wykorzystaj obrazy takie jak `node:16` i `nginx:alpine`.

---

## Zadanie 8: Zarządzanie logami w kontenerze
### Kroki:
1. Utwórz kontener aplikacji Python zapisujący logi w plikach.
2. Skonfiguruj wolumen na logi.
3. Przetestuj, czy logi są dostępne na hoście.

### Podpowiedzi:
- Użyj `VOLUME` w Dockerfile.
- W `docker-compose.yml` skonfiguruj mapowanie wolumenu.

---

## Zadanie 9: Commitowanie obrazu z modyfikacjami
### Kroki:
1. Uruchom kontener z `nginx`.
2. Zmodyfikuj jego konfigurację w środku kontenera.
3. Użyj `docker commit`, aby zapisać zmodyfikowany obraz.

### Podpowiedzi:
- Połącz się z kontenerem za pomocą `docker exec`.
- Użyj polecenia `docker commit <container_id> <new_image_name>`.

---

## Zadanie 10: Zaawansowane sieci w Docker Compose
### Kroki:
1. Stwórz plik `docker-compose.yml`, który uruchamia dwa serwisy (Node.js i Redis).
2. Skonfiguruj osobne sieci dla każdego serwisu.
3. Dodaj serwis proxy, który łączy oba serwisy.

### Podpowiedzi:
- Skorzystaj z `networks` w `docker-compose.yml`.
- Ustaw `links` lub `depends_on` dla serwisów, aby zapewnić komunikację.
