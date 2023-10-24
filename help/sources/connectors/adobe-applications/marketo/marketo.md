---
keywords: Experience Platform;hemmabruk;populära ämnen;Marketo Engage;markering för att engagera;markering för
solution: Experience Platform
title: Marketo Engage-kontakt
description: Det här dokumentet innehåller en översikt över Marketo Engage-källkopplingen, inklusive information om autentisering, mappning och datalatens.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 50b97ebb8496636a0fccd64d57d7829b1342f87c
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# [!DNL Marketo Engage] koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) är en komplett lösning för lead-hantering och B2B-marknadsförare som vill omvandla kundupplevelser genom att engagera sig i alla faser av komplexa inköpsresor.

Med [!DNL Marketo Engage] källanslutning kan du hämta B2B-data från [!DNL Marketo Engage] till Platform och hålla dessa data uppdaterade med plattformsanslutna program.

>[!IMPORTANT]
>
>Du måste ha tillgång till [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) för att använda alla Marketo-dataset för segmentering med [Kundprofil i realtid](../../../../profile/home.md). Utan Real-Time CDP B2B Edition kan du fortfarande använda Marketo-källan för att överföra data från persondata och aktivitetsdatauppsättningar till kundprofilen i realtid för segmentering.

Dokumentet innehåller en översikt över [!DNL Marketo Engage] källkoppling, inklusive information om hur anslutningen autentiseras, mappa [!DNL Marketo Engage] fält till Experience Data Model (XDM) och anslutningsens datalatens.

## Ställ in organisationsmappning för Adobe

Innan du kan skapa mappningsuppsättningar för [!DNL Marketo Engage]måste du först konfigurera Organisationsmappning för Adobe. Detaljerade anvisningar om hur du slutför detta finns i handboken [konfigurera organisationsmappning för Adobe [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentisera [!DNL Marketo Engage] koppling

För att kunna ansluta [!DNL Marketo Engage] till Platform måste du först hämta värden för `munchkinId`, `clientId`och `clientSecret`.

Se stegen som beskrivs i [Autentisera din Marketo-källanslutning](./marketo-auth.md) för att hämta dina inloggningsuppgifter.

## Konfigurera B2B-namnutrymmen och automatisk schemagenerering

Använd sedan verktyget för automatisk generering av B2B-namnutrymme och schema för att konfigurera din plattformsutvecklarkonsol och Postman-miljö. På så sätt kan du automatiskt fylla i B2B-namnutrymmen och scheman. Detaljerade anvisningar finns i handboken på [konfigurera B2B-namnutrymmen och automatisk generering av scheman](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner som gör att du kan importera data från tredjepartskällor för användning i plattformstjänster längre fram i kedjan.

Genom att följa XDM-standarder kan data integreras enhetligt i plattformens ekosystem, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM och dess roll i Platform finns i [XDM - systemöversikt](../../../../xdm/home.md).

## Fältmappning från [!DNL Marketo Engage] till XDM

Skapa en källanslutning mellan [!DNL Marketo Engage] och Platform måste Marketo källdatafält mappas till sina lämpliga mål-XDM-fält innan de hämtas till Platform.

Mer information om fältmappningsreglerna mellan [!DNL Marketo Engage] datauppsättningar och plattform:

* [Aktiviteter](../mapping/marketo.md#activities)
* [Program](../mapping/marketo.md#programs)
* [Programmedlemskap](../mapping/marketo.md#program-memberships)
* [Företag](../mapping/marketo.md#companies)
* [Statiska listor](../mapping/marketo.md#static-lists)
* [Statiska listmedlemskap](../mapping/marketo.md#static-list-memberships)
* [Namngivna konton](../mapping/marketo.md#named-accounts)
* [Möjligheter](../mapping/marketo.md#opportunities)
* [Kontaktroller för affärsmöjlighet](../mapping/marketo.md#opportunity-contact-roles)
* [Personer](../mapping/marketo.md#persons)

## Förväntad fördröjning för [!DNL Marketo Engage] data på plattformen

I följande tabell visas den förväntade fördröjningen för hämtning [!DNL Marketo Engage] data till plattformen, baserat på typen av förtäring och önskat mål:

| Destination | Förväntad svarstid |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minuter |
| Data Lake | &lt; 60 minuter |

>[!NOTE]
>
>Latenssiffrorna ovan representerar förväntningar på en 95-procentig konfidensnivå. Den faktiska latensen kan variera och i sällsynta fall sträcka sig över 50 %.

## Nästa steg och ytterligare resurser

I följande dokumentation finns mer information om hur du skapar en [!DNL Marketo Engage] källanslutning:

* Mer information om hur du ansluter [!DNL Marketo Engage] data till plattformen, läs självstudiekursen om [skapa [!DNL Marketo Engage] källanslutning i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Mer information om hur du ställer in scheman och importerar anpassade aktivitetsdata finns i självstudiekursen om [skapa en källanslutning och ett dataflöde för [!DNL Marketo Engage] anpassade aktivitetsdata](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* Mer information om de underliggande inställningarna för B2B-namnutrymmen och scheman som används med [!DNL Marketo Engage], läs dokumentationen för [B2B-namnutrymmen och scheman](./marketo-namespaces.md).
* Om du vill ha information om hur du hittar [!DNL Marketo Engage] munchkin-ID och generera dina inloggningsuppgifter, läs [[!DNL Marketo Engage] autentiseringsguide](./marketo-auth.md).
* Mer information om mappningsregler som gäller för [!DNL Marketo Engage] datauppsättningar, läsa dokumentationen om [[!DNL Marketo Engage] fältkopplingar](../mapping/marketo.md).
* Allmän information om [!DNL Real-Time Customer Data Platform B2B Edition] och dess funktioner kan du läsa dokumentationen om [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
