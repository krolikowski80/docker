
# Multi-Container App with Docker

Ten projekt pokazuje, jak stworzyć aplikację wielokontenerową z wykorzystaniem Dockera. Aplikacja składa się z backendu (Node.js) i bazy danych (PostgreSQL).

## Wymagania wstępne
- Zainstalowany Docker i Docker Compose

## Struktura projektu
```
multi-container-app/
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   ├── index.js
├── docker-compose.yml
└── README.md
```

## Krok po kroku

1. **Klonuj repozytorium lub skopiuj strukturę projektu**.
2. **Przejdź do folderu projektu**:
   ```bash
   cd multi-container-app
   ```
3. **Uruchom aplikację**:
   ```bash
   docker-compose up
   ```
4. **Otwórz aplikację w przeglądarce**:
   - Aplikacja będzie dostępna pod adresem `http://localhost:3000`.

## Pliki TODO

### backend/Dockerfile
```dockerfile
# TODO: Ustaw Node.js jako bazowy obraz
FROM node:16

# TODO: Ustaw katalog roboczy
WORKDIR /app

# TODO: Skopiuj pliki projektu
COPY package.json .
COPY index.js .

# TODO: Zainstaluj zależności
RUN npm install

# TODO: Uruchom aplikację
CMD ["node", "index.js"]
```

### backend/package.json
```json
{
  "name": "multi-container-backend",
  "version": "1.0.0",
  "main": "index.js",
  "dependencies": {
    "express": "^4.18.2",
    "pg": "^8.11.0"
  }
}
```

### backend/index.js
```javascript
const express = require('express');
const { Pool } = require('pg');

const app = express();
const pool = new Pool({
  user: 'postgres',
  host: 'db',
  database: 'postgres',
  password: 'password',
  port: 5432,
});

app.get('/', async (req, res) => {
  const result = await pool.query('SELECT NOW()');
  res.send(`Hello World! Server time is: ${result.rows[0].now}`);
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

### docker-compose.yml
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

## Debugowanie
- Jeśli coś nie działa, sprawdź logi kontenerów:
  ```bash
  docker-compose logs
  ```

## Zatrzymanie aplikacji
- Aby zatrzymać aplikację, użyj:
  ```bash
  docker-compose down
  ```

## Licencja
Projekt jest dostępny na licencji MIT.
