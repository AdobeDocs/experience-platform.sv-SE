---
title: PathFactory Source - översikt
description: Lär dig hur du ansluter PathFactory till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/) erbjuder en molnbaserad plattform som hjälper företag att hantera innehållsresor och öka engagemanget med hjälp av smarta innehållsinsikter. Den här guiden beskriver hur du kan integrera data från PathFactory i Experience Platform med hjälp av PathFactorys anslutningar för optimalt databehov.

Du kan importera data från [[!DNL PathFactory]](https://www.pathfactory.com/) med tre primära källor:

* **[!DNL Visitors]**: Importera kund- och kontaktdata som poster för att bättre förstå er målgrupp.
* **[!DNL Sessions]**: Tidsseriehändelser som spårar enskilda användarsessionsaktiviteter på din plattform.
* **[!DNL Page Views]**: Tidsseriehändelser som ger insikter om vilka sidor som visas, vilket hjälper dig att analysera innehållets prestanda.

Läs dokumentet nedan om du vill ha information om hur du kan konfigurera ditt [!DNL PathFactory]-källkonto.

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förhandskrav {#prerequisites}

Innan du börjar integrera [[!DNL PathFactory]](https://www.pathfactory.com/)-anslutningar med Experience Platform måste du kontrollera att du uppfyller följande krav:

* **Ett [PathFactory-konto]**.
   * Kontakta [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) om du inte redan har ett giltigt konto.
* **En aktiv prenumeration** på valfri [!DNL PathFactory]-produkt.
* **Användarnamn, lösenord och domän**.
   * Dessa autentiseringsuppgifter krävs för att komma åt ditt [!DNL PathFactory]-konto och dess data.
* **Åtkomsttoken** och **API-slutpunkter**.
   * Dessa krävs för att ansluta till [!DNL PathFactory] API:er.

### Hämta autentiseringsuppgifter och åtkomsttoken {#gather-credentials}

Om du vill ansluta [!DNL PathFactory] till Experience Platform måste du ange följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning | Slutpunkt |
| --- | --- | --- |
| Användarnamn | Användarnamn för ditt [!DNL PathFactory]-konto. | Ej tillämpligt |
| Lösenord | Lösenordet för ditt [!DNL PathFactory]-konto. | Ej tillämpligt |
| Domän | Domänen som är associerad med ditt [!DNL PathFactory]-konto. | Ej tillämpligt |
| Åtkomsttoken | En unik token som används för API-autentisering. | Ej tillämpligt |
| Slutpunkt för besökare | API-slutpunkten för besöksdata. | `/api/public/v3/data_lake_apis/visitors.json` |
| Slutpunkt för sessioner | API-slutpunkten för sessionsdata. | `/api/public/v3/data_lake_apis/sessions.json` |
| Slutpunkt för sidvisning | API-slutpunkten för sidvisningsdata. | `/api/public/v3/data_lake_apis/page_views.json` |

Detaljerade instruktioner om hur du får ditt användarnamn, lösenord, domän och åtkomsttoken finns på [[!DNL PathFactory] supportcentret](https://support.pathfactory.com/categories/adobe/). Den här resursen innehåller omfattande guider för hur du hämtar och hanterar dina inloggningsuppgifter.

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL PathFactory]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

## Anslut [!DNL PathFactory] till Experience Platform {#pathfactory-connect}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL PathFactory] till Experience Platform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för att hämta [!DNL PathFactory] data till Experience Platform med API:er](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Anslut ditt [!DNL PathFactory] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet ](../../tutorials/ui/dataflow/marketing-automation.md).
