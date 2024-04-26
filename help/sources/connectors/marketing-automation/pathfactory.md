---
title: PathFactory Source Overview
description: Lär dig hur du ansluter PathFactory till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# [!DNL PathFactory]

>[!NOTE]
>
>The [!DNL PathFactory] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

[[!DNL PathFactory]](https://www.pathfactory.com/) erbjuder en molnbaserad plattform som hjälper företag att hantera innehållsresor och öka engagemanget med hjälp av smarta innehållsinsikter. Den här guiden beskriver hur du kan integrera data från PathFactory i Experience Platform och använda PathFactorys anslutningar för optimalt databehov.

Du kan importera data från [[!DNL PathFactory]](https://www.pathfactory.com/) med tre primära källor:

* **[!DNL Visitors]**: Använd kunddata och kontaktdata som register för att bättre förstå er målgrupp.
* **[!DNL Sessions]**: Tidsseriehändelser som spårar enskilda användarsessionsaktiviteter på din plattform.
* **[!DNL Page Views]**: Händelser i tidsserier som ger insikter om vilka sidor som visas, vilket hjälper dig att analysera innehållets prestanda.

Läs dokumentet nedan för information om hur du kan konfigurera [!DNL PathFactory] källkonto.

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar {#prerequisites}

Innan du börjar integrera [[!DNL PathFactory]](https://www.pathfactory.com/) anslutningarna till Experience Platform, se till att du uppfyller följande krav:

* **A [PathFactory-konto]**.
   * Kontakt [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) om du inte redan har ett giltigt konto.
* **En aktiv prenumeration** till [!DNL PathFactory] produkt.
* **Användarnamn, lösenord och domän**.
   * Dessa autentiseringsuppgifter krävs för att du ska få åtkomst till dina [!DNL PathFactory] konto och dess data.
* **Åtkomsttoken** och **API-slutpunkter**.
   * Dessa krävs för att ansluta till [!DNL PathFactory] API.

### Hämta autentiseringsuppgifter och åtkomsttoken {#gather-credentials}

Ansluta [!DNL PathFactory] till Experience Platform måste du ange följande uppgifter:

| Autentiseringsuppgifter | Beskrivning | Slutpunkt |
| --- | --- | --- |
| Användarnamn | Dina [!DNL PathFactory] användarnamn för konto. | Ej tillämpligt |
| Lösenord | Dina [!DNL PathFactory] kontolösenord. | Ej tillämpligt |
| Domän | Domänen som är kopplad till din [!DNL PathFactory] konto. | Ej tillämpligt |
| Åtkomsttoken | En unik token som används för API-autentisering. | Ej tillämpligt |
| Slutpunkt för besökare | API-slutpunkten för besöksdata. | `/api/public/v3/data_lake_apis/visitors.json` |
| Slutpunkt för sessioner | API-slutpunkten för sessionsdata. | `/api/public/v3/data_lake_apis/sessions.json` |
| Slutpunkt för sidvisning | API-slutpunkten för sidvisningsdata. | `/api/public/v3/data_lake_apis/page_views.json` |

Detaljerade instruktioner om hur du får ditt användarnamn, lösenord, domän och åtkomsttoken finns på [[!DNL PathFactory] Support Center](https://support.pathfactory.com/categories/adobe/). Den här resursen innehåller omfattande guider för hur du hämtar och hanterar dina inloggningsuppgifter.

### Konfigurera behörigheter i Experience Platform

Du måste ha båda **[!UICONTROL View Sources]** och **[!UICONTROL Manage Sources]** behörigheter för ditt konto för att ansluta [!DNL PathFactory] konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [gränssnittsguide för åtkomstkontroll](../../../access-control/ui/overview.md).

## Anslut [!DNL PathFactory] till plattform {#pathfactory-connect}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL PathFactory] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde som ger [!DNL PathFactory] data till plattformen med API:er](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Koppla samman [!DNL PathFactory] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md).
