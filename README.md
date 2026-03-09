# 1. Projekt-Setup
Zuerst holen wir uns den Quellcode der App von GitHub:

git clone https://github.com/docker/getting-started-app.git
cd getting-started-app

# 2. Image bauen

wir erstellen eine "Dockerfile" in unsere getting-started-app und fügen diesen Zeilen ein: 
'# syntax=docker/dockerfile:1

FROM node:24-alpine
WORKDIR /app
COPY . .
RUN npm install --omit=dev
CMD ["node", "src/index.js"]
EXPOSE 3000'

Befehl zum Erstellen des Images:
docker build -t getting-started .

Der Punkt . am Ende sagt Docker, dass das Dockerfile im aktuellen Verzeichnis liegt.

# 3. Container starten
Nachdem das Image erstellt wurde, starten wir die App:

docker run -dp 127.0.0.1:3000:3000 getting-started

danach kann man in seine browse unter https://localhost:3000 die APP finden

mit "docker ps"
 zeigt es in der terminal die Container ID wie:
 CONTAINER ID        IMAGE               COMMAND
 df784548666d        getting-started     "docker-entrypoint.sâ¦"   
 
 CREATED            STATUS 
 2 minutes ago      Up 2 minutes 

PORTS                      NAMES
127.0.0.1:3000->3000/tcp   priceless_mcclintock  

# 4. Quellcode anpassen
Ändere den Text in der Datei src/static/js/app.js (ca. Zeile 56):

Alt: No items yet! Add one above!
Neu: You have no todo items yet! Add one above!

# 5. Das Image neu bauen
Da Docker-Images statisch sind, müssen wir nach jeder Code-Änderung ein neues Image erstellen:

docker build -t getting-started .

# 6. Den alten Container entfernen

mit "docker ps" zeigt er welche container du hast 
und mit "docker stop <Docker-ID>" stoppte er das Container mit den ID
und löschen brauchen wir "docker rm <Docker-ID>"

# 7. Starten den updated App container
"docker run -dp 127.0.0.1:3000:3000 getting-started"

die browser mit http://localhost:3000 und man sollt schon seine updated help text