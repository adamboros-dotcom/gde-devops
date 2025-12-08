# DevOps Hello World Projekt

Ez a projekt a DevOps tárgy beadandó feladata. Egy egyszerű Node.js alkalmazást tartalmaz, amely bemutatja az alapvető DevOps lépéseket: automatizált buildelést, konténerizációt és CI pipeline használatát.

## 1. Alkalmazás (Követelmény 2.1)
Az alkalmazás egy Express.js alapú webszerver.
- **URL:** http://localhost:8080
- **Funkció:** Egy egyszerű "Hello World" üzenetet ad vissza a böngészőben.

## 2. Buildelés (Követelmény 2.2)
A projekt előkészítése és buildelése (függőségek telepítése) az alábbi parancsokkal történik:

```bash
npm install
npm run build
````

## 3\. Git használat - Trunk-based (Követelmény 2.3)

A projekt **trunk-based** fejlesztési modellt követi.

  - A fejlesztés egy közös fő ágon (`main`) történik.
  - A módosítások rövid életű feature branch-eken készülnek, majd gyorsan beolvasztásra (merge) kerülnek a főágba.

## 4\. Dockerizálás (Követelmény 2.4)

Az alkalmazás konténerizálva van, így környezetfüggetlenül futtatható.

**Image buildelése:**

docker build -t hello-devops:v1 .

**Konténer futtatása:**

docker run -p 8080:8080 hello-devops:v1

Indítás után az alkalmazás elérhető a böngészőben: `http://localhost:8080`

## 5\. Választott feladat: CI Pipeline és Registry (Követelmény 3.2)

A projekt tartalmaz egy **GitHub Actions** workflow-t (`.github/workflows/main.yml`).

**A pipeline működése:**
Minden kódmódosításkor (push esemény) automatikusan:

1.  Lekéri a kódot (Checkout).
2.  Telepíti a Node.js környezetet.
3.  Lefuttatja a build parancsot.
4.  Elkészíti a Docker image-et.

**Registry információk:**
A sikeres build után a Docker image a GitHub Container Registry-be (GHCR) kerül publikálásra.

  * **Registry URL:** `ghcr.io`
  * **Image neve:** `ghcr.io/abadamboros-dotcom/gde-devops:latest`

**Image letöltése és futtatása (Deploy):**
Az elkészült image az alábbi parancsokkal húzható le és indítható el tetszőleges környezetben:

# 1. Image letöltése
docker pull ghcr.io/adamboros-dotcom/gde-devops:latest

# 2. Alkalmazás elindítása
docker run -p 8080:8080 ghcr.io/adamboros-dotcom/gde-devops:latest