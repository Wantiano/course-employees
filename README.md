# CI/CD oktatás

Employee alkalmazás CI/CD folyamatának megvalósítása.

Konténerben való buildeléshez használjuk a `Dockerfile.build` fájlt.

```shell
docker tag employees localhost:8092/employees
```

```shell
docker push localhost:8092/employees
```

```shell
docker build -t employees -f Dockerfile.layers .
```

```shell
docker tag employees localhost:8092/employees:1.0.2
```

```shell
docker push localhost:8092/employees:latest
```

```shell
docker push localhost:8092/employees:1.0.2
```

```shell
docker build -t employees -f Dockerfile.build .
```

```shell
docker tag employees wantiano/employees
```

```shell
docker build -t employees .
```

Heroku: több ezer alkalmazást üzemeltetnek a felhőben
a fejlesztők és üzemeleltetők kialakítottak konvenciókat, hogy a felhőben egyszerűen üzemeltethető legyen.

[12factor.net](https://12factor.net)

A Spring környezeti változóba olvassa fel a konfigokat.
Cloudra is és dockerre is passzol ez a működés.

docker-compose -> python (régi)
docker compose -> docker (új)

Meg kell várni, hogy a mariadb szolgáltatás elinduljon (ne csak a container).

Az employees:latest container melyik networkben van
```shell
docker inspect eployees:latest
```

Az employees_default networkben mely containerek vannak.
```shell
docker network inspect employees_default
```

Lognézés
```shell
docker compose logs -f
```

Employees leállítása, elindítása
docker compose down employees
docker compose up employees

Jelenleg read write layerbe pakolja az adatot a mariadb
volume-t kellene felcsatolni, hogy perzisztensen megmaradjon.

Container:
- MariaDB - db
- Employees - alkalmazás
- Selenium grid - Lehetővé teszi a párhuzamos teszt végrehajtást
- Selenium chrome - chrome van feltelepítve
- FFEMPEG nézi a selenium chrome virtuális kijelzőjét és rögzíti ideóra
- selenium konténer - parancsok futtatása