---
title: Oracle DB Source Connector - översikt
description: Lär dig hur du ansluter Oracle till Adobe Experience Platform med API:er eller användargränssnittet.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] är ett kraftfullt relationsdatabashanteringssystem som utvecklats av [!DNL Oracle Corporation]. Du kan använda [!DNL Oracle DB] för att lagra, hantera och hämta stora volymer strukturerade data effektivt och säkert.

Använd källan [!DNL Oracle DB] i Adobe Experience Platform-källkatalogen för att ansluta databasen och importera data till Experience Platform.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter ditt [!DNL Oracle DB]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på antingen Azure eller Amazon Web Services (AWS). Mer information finns i guiden [tillåtslista IP-adresser för att ansluta till Experience Platform på Azure och AWS](../../ip-address-allow-list.md).

### Autentisera till Experience Platform på Azure {#azure}

Ange en anslutningssträng för att autentisera och ansluta ditt [!DNL Oracle DB]-konto till Experience Platform på Azure.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Anslutningssträng | En anslutningssträng är en textsträng som används av program för att ansluta till en databas. Anslutningssträngsmönstret [!DNL Oracle DB] är: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| Anslutningsspecifikation-ID | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL Oracle] är `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

### Autentisera till Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Ange värden för följande autentiseringsuppgifter för att autentisera och ansluta ditt [!DNL Oracle DB]-konto till Experience Platform på AWS.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Server | IP-adressen eller värdhanteraren för [!DNL Oracle DB]-servern. |
| Port | Portnumret för databasservern. Standardportnumret är `1521`. |
| Användarnamn | Användarkontot [!DNL Oracle DB] som används för att autentisera och komma åt databasen. |
| Lösenord | Den hemliga nyckel som är kopplad till ditt användarnamn och som används för autentisering. |
| Databas | Den specifika [!DNL Oracle]-databasinstans som du vill ansluta till. |
| Schema | Behållaren för databasobjekt, t.ex. tabeller, vyer eller procedurer. |
| SSL-läge | Ett booleskt värde som styr om SSL används eller inte. Den här konfigurationen beror på din serversupport och är som standard `false`. |
| Anslutningsspecifikation-ID | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL Oracle] är `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |


## Anslut [!DNL Oracle] till [!DNL Experience Platform] med API:er

- [Anslut Oracle DB med API:t för Flow Service](../../tutorials/api/create/databases/oracle.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Oracle] till [!DNL Experience Platform] med användargränssnittet

- [Anslut Oracle DB med Experience Platform UI-arbetsyta.](../../tutorials/ui/create/databases/oracle.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
