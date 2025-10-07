## 🛠️ Lab Setup (leader)
Create networks and the shared volume once:

```bash
docker network create canaverales
docker network create ciudad-cordoba
docker network create las-americas
docker network create vista-hermosa
docker network create villa-fatima
docker network create el-portal
docker network create sindical
docker network create siloe

docker volume create biblioteca-del-pueblo
```

---

### Download image:
```bash
docker pull juanpazcai/cali-service:v1
docker pull davidguerrerod/cali-service:v1
docker pull ghcr.io/jhonierm14/cali-service:v1
docker pull finnito/cali-service:v1
docker pull cobolios/cali-service:v1
docker pull esas9/cali-service:v1
docker pull sxthy/cali-service:v1
docker pull sergios22/cali-service:v1
```
*(For GitHub Packages, ensure you’re logged in with a PAT and `docker login ghcr.io`.)*

---

### Run your service in your neighborhood
Each student runs a container from their **published image** (names below are examples; feel free to customize):

```bash
docker run -d --name svc-juan \
  --network canaverales \
  -e STUDENT_NAME="Juan-Pablo" \
  -e BARRIO="Cañaverales" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 0:8080 juanpazcai/cali-service:v1

docker run -d --name svc-david \
  --network las-americas \
  -e STUDENT_NAME="David Guerrero" \
  -e BARRIO="Las Americas" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 0:8080 davidguerrerod/cali-service:v1

docker run -d --name svc-jhonier
--network vista-hermosa
-e STUDENT_NAME="Jhonier Mendez"
-e BARRIO="Vista Hermosa"
-v biblioteca-del-pueblo:/var/log/app
-p 8080:8080 ghcr.io/jhonierm14/cali-service:v1

docker run -d --name svc-Santi \
  --network Villa-Fatima \
  -e STUDENT_NAME="Santiago Amariles" \
  -e BARRIO="Villa Fatima" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 8080:8080 \esas9/cali-service:v1

docker run -d --name svc-sara \
  --network Portal \
  -e STUDENT_NAME="Sara" \
  -e BARRIO="El Portal" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 8080:8080 \
  sxthy/cali-service:v1

docker run -d --name svc-Tobar \
  --network Sindical \
  -e STUDENT_NAME="Juan Tobar" \
  -e BARRIO="Sindical" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 8080:8080 \
  finnito/cali-service:v1

docker run -d --name svc-cristian \
  --network ciudad-cordoba \
  -e STUDENT_NAME="Cristian" \
  -e BARRIO="Ciudad Cordoba" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 8080:8080 cobolios/cali-service:v1

docker run -d --name svc-Sergio \
  --network Villa-Fatima \
  -e STUDENT_NAME="Sergio Sanchez" \
  -e BARRIO="Siloé" \
  -v biblioteca-del-pueblo:/var/log/app \
  -p 8080:8080 \
  esas9/cali-service:v1

```

---

### Step 6: Test connectivity
```bash
# From host
curl http://localhost:32768

# From another container in the same neighborhood
docker run --rm --network canaverales curlimages/curl -s http://svc-jhonier:8080/
```

---

### Step 7: Check “La Biblioteca del Pueblo”
Verify that logs are being written:

```bash
docker run --rm -v biblioteca-del-pueblo:/data alpine \
  sh -c "tail -n 20 /data/visitas.log"
```

Or enter the volume:
```bash
docker run --rm -it -v biblioteca-del-pueblo:/data alpine sh
```

---

## ✅ What you will learn
- How to **collaborate as a team using trunk-based Git strategy**.  
- How to **build and publish Docker images** to Docker Hub or GitHub Packages.  
- How **Docker networks** isolate and connect services.  
- How **volumes** allow sharing and persistence of data.  
- How collaboration looks when multiple services write to the same shared space.  

---

# 📌 Deliverables
- A folder in the shared repo `/students/<your-name>/` with Dockerfile, code, and dependencies.  
- A published Docker image (Docker Hub or GitHub Packages).  
- A working container in your chosen neighborhood.  
- Evidence that your service wrote to **La Biblioteca del Pueblo**.  
- Short explanation of your design choice (Python, Node.js, Nginx, etc).  
- Optional: use your **own names** for networks, images, and containers to make the demo personal.  
