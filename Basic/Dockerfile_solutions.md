
# Rozwiązania do zadań z Dockerfile

## Zadanie 1: Tworzenie prostego obrazu z aplikacją Hello World
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
FROM alpine
CMD ["echo", "Hello World"]
```

Budowanie obrazu:
```bash
docker build -t hello-world .
```

Uruchamianie:
```bash
docker run hello-world
```

---

## Zadanie 2: Kontener z aplikacją Python
### Rozwiązanie:
Plik `app.py`:
```python
print("Hello from Python!")
```

Plik `Dockerfile`:
```dockerfile
FROM python:3.9
COPY app.py /app.py
CMD ["python", "/app.py"]
```

Budowanie obrazu:
```bash
docker build -t python-app .
```

Uruchamianie:
```bash
docker run python-app
```

---

## Zadanie 3: Tworzenie i montowanie wolumenu
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
FROM nginx
VOLUME ["/usr/share/nginx/html"]
```

Budowanie obrazu:
```bash
docker build -t nginx-with-volume .
```

Uruchamianie kontenera z wolumenem:
```bash
docker run -d -v $(pwd)/html:/usr/share/nginx/html -p 8080:80 nginx-with-volume
```

---

## Zadanie 4: Docker Compose - aplikacja Node.js
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

Plik `docker-compose.yml`:
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    networks:
      - app-network
  mongo:
    image: mongo
    networks:
      - app-network
networks:
  app-network:
    driver: bridge
```

Budowanie i uruchamianie:
```bash
docker-compose up --build
```

---

## Zadanie 5: Zmniejszenie rozmiaru obrazu
### Rozwiązanie:
Plik `Dockerfile` przed optymalizacją:
```dockerfile
FROM python:3.9
COPY app.py /app.py
CMD ["python", "/app.py"]
```

Plik `Dockerfile` po optymalizacji:
```dockerfile
FROM python:3.9-slim
COPY app.py /app.py
CMD ["python", "/app.py"]
```

Porównanie rozmiarów:
```bash
docker build -t python-app-full -f Dockerfile.full .
docker build -t python-app-slim -f Dockerfile.slim .
docker images
```

---

## Zadanie 6: Budowanie obrazu z cache
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

Budowanie obrazu:
```bash
docker build -t node-cached .
```

Przy kolejnym budowaniu, cache dla zależności `npm install` zostanie użyty.

---

## Zadanie 7: Tworzenie wieloetapowego obrazu
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
# Etap 1: Budowanie frontendu
FROM node:16 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Etap 2: Tworzenie finalnego obrazu
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
```

Budowanie obrazu:
```bash
docker build -t multi-stage-app .
```

Uruchamianie:
```bash
docker run -d -p 8080:80 multi-stage-app
```

---

## Zadanie 8: Zarządzanie logami w kontenerze
### Rozwiązanie:
Plik `Dockerfile`:
```dockerfile
FROM python:3.9
COPY app.py /app.py
RUN mkdir /logs
VOLUME ["/logs"]
CMD ["python", "/app.py"]
```

Uruchamianie z wolumenem:
```bash
docker run -v $(pwd)/logs:/logs python-app
```

---

## Zadanie 9: Commitowanie obrazu z modyfikacjami
### Rozwiązanie:
Uruchomienie kontenera:
```bash
docker run -d --name nginx-container nginx
```

Modyfikacja konfiguracji:
```bash
docker exec -it nginx-container /bin/sh
# Wprowadź zmiany, np. edytuj plik /etc/nginx/nginx.conf
```

Commitowanie obrazu:
```bash
docker commit nginx-container nginx-modified
```

Uruchamianie zmodyfikowanego obrazu:
```bash
docker run -d -p 8080:80 nginx-modified
```

---

## Zadanie 10: Zaawansowane sieci w Docker Compose
### Rozwiązanie:
Plik `docker-compose.yml`:
```yaml
version: '3.8'
services:
  app:
    image: node:16
    networks:
      - app-network
    depends_on:
      - redis
  redis:
    image: redis
    networks:
      - redis-network
  proxy:
    image: nginx
    networks:
      - app-network
      - redis-network
networks:
  app-network:
    driver: bridge
  redis-network:
    driver: bridge
```

Uruchamianie:
```bash
docker-compose up --build
```

---

Powodzenia!
