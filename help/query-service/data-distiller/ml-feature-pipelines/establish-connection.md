---
title: Anslut till Data Distiller från en Jupyter-anteckningsbok
description: Lär dig hur du ansluter till Data Distiller från en Jupyter-anteckningsbok.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Anslut till Data Distiller från en Jupyter-anteckningsbok

För att berika dina maskininlärningspipelines med värdefulla kundupplevelsedata måste du först ansluta till Data Distiller från [!DNL Jupyter Notebooks]. Det här dokumentet innehåller stegen för att ansluta till Data Distiller från en [!DNL Python]-anteckningsbok i maskininlärningsmiljön.

## Komma igång

Den här handboken förutsätter att du känner till de interaktiva [!DNL Python] bärbara datorerna och har tillgång till en anteckningsboksmiljö. Anteckningsboken kan finnas på en molnbaserad maskininlärningsmiljö, eller lokalt med [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Hämta anslutningsreferenser {#obtain-credentials}

Om du vill ansluta till Data Distiller och andra Adobe Experience Platform-tjänster behöver du en Experience Platform API-autentiseringsuppgift. API-autentiseringsuppgifter kan skapas i [Adobe Developer Console](https://developer.adobe.com/console/home) av någon med Developer-åtkomst till Experience Platform. Du rekommenderas att skapa en Oauth2 API-autentiseringsuppgift specifikt för arbetsflöden inom datavetenskap och att ha en Adobe-systemadministratör från din organisation som tilldelar autentiseringsuppgifterna till en roll med lämplig behörighet.

Se [Autentisera och få åtkomst till Experience Platform API:er](../../../landing/api-authentication.md) för detaljerade anvisningar om hur du skapar en API-autentiseringsuppgift och får de behörigheter som krävs.

Rekommenderade tillstånd för datavetenskap är bland annat:

- Sandbox(er) som ska användas för datavetenskap (vanligen `prod`)
- Datamodellering: [!UICONTROL Manage Schemas]
- Datahantering: [!UICONTROL Manage Datasets]
- Intag av data: [!UICONTROL View Sources]
- Destinationer: [!UICONTROL Manage and Activate Dataset Destinations]
- Frågetjänst: [!UICONTROL Manage Queries]

Som standard blockeras en roll (och API-autentiseringsuppgifter som tilldelats den rollen) från att komma åt alla märkta data. I enlighet med organisationens datahanteringsprinciper kan en systemadministratör ge rollen tillgång till vissa märkta data som anses lämpliga för datavetenskapen. Experience Platform-kunder ansvarar för att hantera åtkomsten till och reglerna för etiketterna på lämpligt sätt för att följa gällande regler och organisationsregler.

### Lagra autentiseringsuppgifter i en separat konfigurationsfil {#store-credentials}

För att skydda dina autentiseringsuppgifter bör du undvika att skriva autentiseringsuppgifter direkt i koden. Istället sparar du inloggningsuppgifterna i en separat konfigurationsfil och läser in de värden som behövs för att ansluta till Experience Platform och Data Distiller.

Du kan till exempel skapa en fil med namnet `config.ini` och inkludera följande information (tillsammans med annan information, som datauppsättnings-ID:n, som kan användas för att spara mellan sessioner):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

I anteckningsboken kan du sedan läsa informationen om autentiseringsuppgifter i minnet med hjälp av paketet `configParser` från standardbiblioteket [!DNL Python]:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Du kan sedan referera till autentiseringsvärden i koden enligt följande:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installera ett epp Python-bibliotek {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) är ett Adobe-hanterat öppen källkodsbibliotek [!DNL Python] som innehåller funktioner för att ansluta till Data Distiller och skicka frågor, som att göra förfrågningar till andra Experience Platform-tjänster. Biblioteket `aepp` i sin tur är beroende av PostgreSQL-databaskortpaketet `psycopg2` för interaktiva Data Distiller-frågor. Det går att ansluta till Data Distiller och skicka frågor till Experience Platform-datauppsättningar med enbart `psycopg2`, men `aepp` erbjuder större bekvämlighet och ytterligare funktionalitet för att göra förfrågningar till alla Experience Platform API-tjänster.

Om du vill installera eller uppgradera `aepp` och `psycopg2` i din miljö kan du använda det magiska kommandot `%pip` i din anteckningsbok:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Du kan sedan konfigurera biblioteket `aepp` med dina autentiseringsuppgifter med följande kod:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Skapa en anslutning till Data Distiller {#create-connection}

När `aepp` har konfigurerats med dina autentiseringsuppgifter kan du använda följande kod för att skapa en anslutning till Data Distiller och starta en interaktiv session enligt följande:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Sedan kan du fråga datauppsättningarna i din Experience Platform-sandlåda. Med ID:t för en datauppsättning som du vill fråga kan du hämta motsvarande tabellnamn från katalogtjänsten och köra frågor i tabellen:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Ansluta till en enda datauppsättning för snabbare frågeprestanda {#connect-to-single-dataset}

Som standard ansluter Data Distiller-anslutningen till alla datauppsättningar i din sandlåda. För snabbare frågor och minskad resursanvändning kan du i stället ansluta till en viss datamängd som är av intresse. Du kan göra detta genom att ändra `dbname` i Data Distiller-anslutningsobjektet till `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att ansluta till Data Distiller från en [!DNL Python]-anteckningsbok i maskininlärningsmiljön. Nästa steg på vägen mot nya rörledningar från Experience Platform för anpassade modeller i maskininlärningsmiljön är att [utforska och analysera datauppsättningarna](./exploratory-analysis.md).
