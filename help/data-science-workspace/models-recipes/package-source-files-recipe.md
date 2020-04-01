---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Paketera källfiler i ett recept
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Paketera källfiler i ett recept

I den här självstudiekursen finns anvisningar om hur du kan paketera de angivna källfilerna för butiksförsäljning i en arkivfil, som kan användas för att skapa ett recept i Adobe Experience Platform Data Science Workspace genom att följa arbetsflödet för receptimport antingen i användargränssnittet eller med API:t.

Koncept att förstå:

- **Recept**: Ett recept är Adobes term för en modellspecifikation och är en behållare på den översta nivån som representerar maskininlärning, artificiell intelligensalgoritm eller en kombination av algoritmer, bearbetningslogik och konfiguration som krävs för att skapa och köra en tränad modell och därmed bidra till att lösa specifika affärsproblem.
- **Källfiler**: Enskilda filer i projektet som innehåller logiken för ett recept.

## Förutsättningar

- [Docker](https://docs.docker.com/install/#supported-platforms)
- [Python 3 och pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Maven](https://maven.apache.org/install.html)

## Recipe creation

Recipe-skapandet börjar med att paketera källfiler för att skapa en arkivfil. Källfiler definierar den maskininlärningslogik och de algoritmer som används för att lösa ett specifikt problem och skrivs antingen i Python, R, PySpark eller Scala Spark. Beroende på vilket språk källfilerna skrivs i blir de inbyggda arkivfilerna antingen en Docker-bild eller en binär fil. När den packade arkivfilen har skapats importeras den till arbetsytan Data Science för att skapa ett recept [i användargränssnittet](./import-packaged-recipe-ui.md) eller [med API:t](./import-packaged-recipe-api.md).

### Skapa modeller med Docker

Med en Docker-bild kan utvecklare paketera ett program med alla delar som behövs, till exempel bibliotek och andra beroenden, och skicka ut det som ett paket.

Den inbyggda Docker-avbildningen skickas till Azure Container Registry med hjälp av de autentiseringsuppgifter som anges när du skapar recept.

>[!NOTE] Endast källfiler skrivna i **Python**, **R** och **Tensorflow** kräver autentiseringsuppgifter för Azure Container Registry.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>för att få dina autentiseringsuppgifter för Azure Container Registry. Navigera till **Arbetsflöden** i den vänstra navigeringskolumnen. Välj **Importera mottagare från källfil** och **starta** en ny importprocedur. Se skärmbilden nedan.

![](../images/models-recipes/package-source-files/workflow_ss.png)

Ange ett lämpligt **mottagarnamn**, t.ex.&quot;Detaljhandelsrecept&quot;, och ange eventuellt en beskrivning- eller dokumentations-URL. Klicka på **Nästa** när du är klar.

![](../images/models-recipes/package-source-files/recipe_info.png)

Välj lämplig **körningsmiljö** och välj sedan **Klassificering** som **typ**. Dina autentiseringsuppgifter för Azure-behållarregistret kommer att genereras.

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

Observera värdena för **Docker Host**, **UserName** och **Password**. Dessa kommer att användas senare för att bygga och trycka din Docker-image.

När den har skickats kan du och andra användare komma åt bilden via URL-adressen. I fältet **Källfil** förväntas den här URL:en som indata.

### Bbinärbaserad modellredigering

För källfiler skrivna i Scala eller PySpark skapas en binär fil. Att skapa den binära filen är lika enkelt som att köra det angivna byggskriptet.
>[!NOTE] Endast källfiler skrivna i ScalaSpark eller PySpark genererar en binär fil när du kör byggskriptet.

### Paketera källfilerna

Börja med att hämta exempelkodbasen som finns i referensdatabasen för <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace</a> . Beroende på vilket programmeringsspråk som exempelkällfilerna är skrivna i skiljer sig själva skapandet av respektive arkivfil åt i proceduren.

- [Skapa Python Docker-bild](#build-python-docker-image)
- [Bygg R Docker-bild](#build-r-docker-image)
- [Skapa PySpark-binärfiler](#build-pyspark-binaries)
- [Bygg Scala-binärfiler](#build-scala-binaries)

#### Skapa Python Docker-bild

Om du inte har gjort det klonar du github-databasen på din lokala dator med följande kommando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigera till katalogen `experience-platform-dsw-reference/recipes/python/retail`. Här hittar du skripten `login.sh` och `build.sh` vilka du använder för att logga in på Docker och för att skapa en python Docker-bild. Om du har dina [Docker-uppgifter](#docker-based-model-authoring) klara anger du följande kommandon i ordning:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observera att när du kör inloggningsskriptet måste du ange Docker-värden, användarnamn och lösenord. När du bygger måste du ange Docker-värden och en versionstagg för bygget.

När byggskriptet är klart får du en URL för Docker-källfilen i konsolutdata. I det här exemplet ser det ut ungefär så här:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Kopiera den här URL:en och gå vidare till [nästa steg](#next-steps).

#### Bygg R Docker-bild

Om du inte har gjort det klonar du github-databasen på din lokala dator med följande kommando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigera till katalogen `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` i din klonade databas. Här hittar du filerna `login.sh` och `build.sh` vilka du använder för att logga in på Docker och för att skapa R Docker-bilden. Om du har dina [Docker-uppgifter](#docker-based-model-authoring) klara anger du följande kommandon i ordning:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Observera att när du kör inloggningsskriptet måste du ange Docker-värden, användarnamn och lösenord. När du bygger måste du ange Docker-värden och en versionstagg för bygget.

När byggskriptet är klart får du en URL för Docker-källfilen i konsolutdata. I det här exemplet ser det ut ungefär så här:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Kopiera den här URL:en och gå vidare till [nästa steg](#next-steps).

#### Skapa PySpark-binärfiler

Om du inte har gjort det klonar du github-databasen på din lokala dator med följande kommando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigera till den klonade databasen på ditt lokala system och kör följande kommandon för att skapa den fil som krävs för att importera ett PySpark-recept: `.egg`

```BASH
cd recipes/pyspark
./build.sh
```

Filen `.egg` genereras i `dist` mappen.

Du kan nu gå vidare till [nästa steg](#next-steps).

#### Bygg Scala-binärfiler

Om du inte redan har gjort det kör du följande kommando för att klona Github-databasen till ditt lokala system:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Om du vill skapa den `.jar` artefakt som används för att importera ett Scala-recept går du till din klonade databas och följer stegen nedan:

```BASH
cd recipes/scala/
./build.sh
```

Den skapade artefakten med beroenden finns i `.jar` `/target` katalogen.

Du kan nu gå vidare till [nästa steg](#next-steps).

## Nästa steg

Den här självstudien gick över till att paketera källfiler i en Recept, vilket är det nödvändiga steget för att importera en Recept till Data Science Workspace. Du bör nu ha en Docker-bild i Azure Container Registry tillsammans med motsvarande bild-URL eller en binär fil som lagras lokalt i ditt filsystem. Nu kan du börja med självstudiekursen om hur du **importerar en paketerad recept till arbetsytan** Data Science. Välj en av självstudielänkarna nedan för att komma igång.

- [Importera en paketerad mottagare i användargränssnittet](./import-packaged-recipe-ui.md)
- [Importera en paketerad mottagare med API:t](./import-packaged-recipe-api.md)