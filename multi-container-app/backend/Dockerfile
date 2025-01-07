
# Ustaw Node.js jako bazowy obraz
FROM node:16

# Ustaw katalog roboczy
WORKDIR /app

# Skopiuj pliki projektu
COPY package.json .
COPY index.js .

# Zainstaluj zależności
RUN npm install

# Uruchom aplikację
CMD ["node", "index.js"]
