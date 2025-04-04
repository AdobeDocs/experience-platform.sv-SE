---
title: Hantera Experience Platform-data med Python och SQLAlchemy
description: Lär dig hur du använder SQLAlchemy för att hantera dina Experience Platform-data med Python i stället för SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Hantera Experience Platform-data med [!DNL Python] och [!DNL SQLAlchemy]

Lär dig hur du använder SQLAlchemy för större flexibilitet i hanteringen av dina Adobe Experience Platform-data. För dem som inte är lika bekanta med SQL kan SQLAlchemy avsevärt förbättra utvecklingstiden när de arbetar med relationsdatabaser. Det här dokumentet innehåller instruktioner och exempel för att ansluta [!DNL SQLAlchemy] till frågetjänsten och börja använda Python för att interagera med dina databaser.

[!DNL SQLAlchemy] är en ORM (Object Relational Mapper) och ett [!DNL Python]-kodbibliotek som kan överföra data som lagras i en SQL-databas till [!DNL Python]-objekt. Du kan sedan utföra CRUD-åtgärder på data som finns i Experience Platform datasjön med hjälp av [!DNL Python]-koden. Detta eliminerar behovet av att hantera data med enbart PSQL.

## Komma igång

Om du vill få de nödvändiga autentiseringsuppgifterna för att ansluta [!DNL SQLAlchemy] till Experience Platform måste du ha tillgång till arbetsytan Frågor i Experience Platform-gränssnittet. Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan Frågor.

## [!DNL Query Service] autentiseringsuppgifter {#credentials}

Om du vill hitta dina autentiseringsuppgifter loggar du in på Experience Platform-gränssnittet och väljer **[!UICONTROL Queries]** i den vänstra navigeringen, följt av **[!UICONTROL Credentials]**. Fullständiga anvisningar om hur du hittar dina inloggningsuppgifter finns i handboken [för inloggningsuppgifter](../ui/credentials.md).

![Fliken Autentiseringsuppgifter med utgångsdatum för frågetjänsten är markerad.](../images/use-cases/credentials.png)

Även om port 80 är den rekommenderade porten för en anslutning till Query Service kan du även använda port 5432.

>[!IMPORTANT]
>
>Om du använder utgångna inloggningsuppgifter (enligt bilden ovan) för att ansluta till Query Service, kommer sessionstiden för din anslutning att upphöra efter den angivna tidsperiod som anges i organisationens inställningar. Som standard är den här perioden 24 timmar. Läs dokumentationen om du vill veta mer om hur du [ansluter en klient med autentiseringsuppgifter som inte upphör att gälla](../ui/credentials.md#non-expiring-credentials) eller hur du [ändrar sessionstiden för de autentiseringsuppgifter som upphör att gälla](../ui/credentials.md#expiring-credentials).

När du har åtkomst till dina QS-autentiseringsuppgifter öppnar du den [!DNL Python]-redigerare du vill använda.

### Lagra autentiseringsuppgifter i [!DNL Python] {#store-credentials}

I [!DNL Python]-redigeraren importerar du `urllib.parse.quote`-biblioteket och sparar varje autentiseringsvariabel som en parameter. Modulen `urllib.parse` innehåller ett standardgränssnitt för att bryta URL-strängar i komponenter. Citattfunktionen ersätter specialtecken i URL-strängen för att göra data säkra att använda som URL-komponenter. Ett exempel på den kod som krävs visas nedan:

>[!TIP]
>
>Använd [!DNL Python]s trippelcitattecken för att ange lösenordssträngen för flera rader.

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
>Lösenordet som du anger för att ansluta [!DNL SQLAlchemy] till Experience Platform går ut om du använder förfalloautentiseringsuppgifter. Mer information finns i avsnittet [autentiseringsuppgifter](#credentials).

### Skapa en motorinstans [#create-engine]

När variablerna har skapats importerar du funktionen `create_engine` och skapar en sträng för att kompilera och formatera dina autentiseringsuppgifter för frågetjänsten i SQLAlchemy. Funktionen `create_engine` används sedan för att konstruera en motorinstans.

>[!NOTE]
>
>`create_engine`returnerar en instans av en motor. Anslutningen till frågetjänsten öppnas dock inte förrän en fråga som kräver en anslutning anropas.

SSL måste vara aktiverat vid åtkomst till Experience Platform med tredjepartsklienter. Som en del av motorn använder du `connect_args` för att ange ytterligare nyckelordsargument. Du rekommenderas att ange SSL-läget till `require`. Mer information om godkända värden finns i [dokumentationen för SSL-lägen](../clients/ssl-modes.md).

I exemplet nedan visas den [!DNL Python]-kod som krävs för att initiera en motor och anslutningssträng.

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
>Lösenordet som du anger för att ansluta [!DNL SQLAlchemy] till Experience Platform går ut om du använder förfalloautentiseringsuppgifter. Mer information finns i avsnittet [autentiseringsuppgifter](#credentials).

Du kan nu fråga Experience Platform-data med [!DNL Python]. Exemplet nedan returnerar en array med frågetjänsttabellnamn.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
