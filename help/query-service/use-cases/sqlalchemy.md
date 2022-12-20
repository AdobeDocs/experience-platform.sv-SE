---
title: Hantera plattformsdata med Python och SQLAlchemy
description: Lär dig hur du använder SQLAlchemy för att hantera plattformsdata med Python i stället för SQL.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Hantera plattformsdata med [!DNL Python] och [!DNL SQLAlchemy]

Lär dig hur du använder SQLAlchemy för större flexibilitet i hanteringen av dina Adobe Experience Platform-data. För dem som inte är lika bekanta med SQL kan SQLAlchemy avsevärt förbättra utvecklingstiden när de arbetar med relationsdatabaser. Det här dokumentet innehåller instruktioner och exempel för att ansluta [!DNL SQLAlchemy] till Query Service och börja använda Python för att interagera med databaser.

[!DNL SQLAlchemy] är en ORM (Object Relational Mapper) och en [!DNL Python] kodbibliotek som kan överföra data som lagras i en SQL-databas till [!DNL Python] objekt. Sedan kan du utföra CRUD-åtgärder på data som lagras inom sjön för plattformsdata med [!DNL Python] kod. Detta eliminerar behovet av att hantera data med enbart PSQL.

## Komma igång

Hämta nödvändiga autentiseringsuppgifter för anslutning [!DNL SQLAlchemy] för Experience Platform måste du ha tillgång till arbetsytan Frågor i användargränssnittet för plattformen. Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan Frågor.

## [!DNL Query Service] autentiseringsuppgifter {#credentials}

Logga in på användargränssnittet för plattformen och välj **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Fullständiga anvisningar om hur du hittar dina inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md).

![Fliken Autentiseringsuppgifter med utgångsdatum för frågetjänsten är markerad.](../images/use-cases/credentials.png)

Även om port 80 är den rekommenderade porten för en anslutning till Query Service kan du även använda port 5432.

>[!IMPORTANT]
>
>Om du använder utgångna inloggningsuppgifter (enligt bilden ovan) för att ansluta till Query Service, kommer sessionstiden för din anslutning att upphöra efter den angivna tidsperiod som anges i organisationens inställningar. Som standard är den här perioden 24 timmar. Läs dokumentationen för att lära dig mer om [ansluta en klient med autentiseringsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials)eller hur [ändra sessionens livslängd för dina förfallande autentiseringsuppgifter](../ui/credentials.md#expiring-credentials).

När du har åtkomst till dina QS-autentiseringsuppgifter öppnar du [!DNL Python] valfri redigerare.

### Lagra autentiseringsuppgifter i [!DNL Python] {#store-credentials}

I [!DNL Python] redigeraren, importera `urllib.parse.quote` bibliotek och spara varje referensvariabel som en parameter. The `urllib.parse` -modulen innehåller ett standardgränssnitt för att dela upp URL-strängar i komponenter. Citattfunktionen ersätter specialtecken i URL-strängen för att göra data säkra att använda som URL-komponenter. Ett exempel på den kod som krävs visas nedan:

>[!TIP]
>
>Använd [!DNL Python]&#39;s triple quotes to enter your multiple lines password string.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Lösenordet du anger för att ansluta [!DNL SQLAlchemy] Experience Platform upphör att gälla om du använder inloggningsuppgifterna. Se [informationssektion](#credentials) för mer information.

### Skapa en motorinstans [#create-engine]

När variablerna har skapats importerar du `create_engine` och skapa en sträng för att kompilera och formatera dina inloggningsuppgifter för frågetjänsten i SQLAlchemy. The `create_engine` används sedan för att konstruera en motorinstans.

>[!NOTE]
>
>`create_engine`returnerar en instans av en motor. Anslutningen till frågetjänsten öppnas dock inte förrän en fråga som kräver en anslutning anropas.

SSL måste vara aktiverat vid åtkomst till plattformen med tredjepartsklienter. Använd `connect_args` om du vill ange ytterligare nyckelordsargument. Du rekommenderas att ange SSL-läget till `require`. Se [Dokumentation för SSL-lägen](../clients/ssl-modes.md) för mer information om godkända värden.

I exemplet nedan visas [!DNL Python] kod som krävs för att initiera en motor och anslutningssträng.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Lösenordet du anger för att ansluta [!DNL SQLAlchemy] Experience Platform upphör att gälla om du använder inloggningsuppgifterna. Se [informationssektion](#credentials) för mer information.

Du är nu redo att fråga efter plattformsdata med [!DNL Python]. Exemplet nedan returnerar en array med frågetjänsttabellnamn.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
