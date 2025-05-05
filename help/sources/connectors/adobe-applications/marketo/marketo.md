---
keywords: Experience Platform;hemmabruk;populära ämnen;Marketo Engage;marknadsför för att engagera;marknadsför till
solution: Experience Platform
title: Marketo Engage Connector
description: Det här dokumentet innehåller en översikt över Marketo Engage källanslutning, inklusive information om autentisering, mappning och datalatens.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# [!DNL Marketo Engage]-koppling

>[!IMPORTANT]
>
>Du kan nu använda källan [!DNL Marketo Engage] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../landing/multi-cloud.md).

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) är en komplett lösning för lead-hantering och B2B-marknadsförare som vill omvandla kundupplevelser genom att engagera i alla faser av komplexa inköpsresor.

Med [!DNL Marketo Engage]-källanslutningen kan du hämta B2B-data från [!DNL Marketo Engage] till Experience Platform och hålla dessa data uppdaterade med Experience Platform-anslutna program.

>[!IMPORTANT]
>
>Du måste ha tillgång till [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) för att kunna använda alla Marketo-datauppsättningar för segmentering med [kundprofilen i realtid](../../../../profile/home.md). Utan Real-Time CDP B2B edition kan ni fortfarande använda Marketo-källan för att överföra data från persondata och aktivitetsdatauppsättningar till kundprofilen i realtid för segmentering.

Det här dokumentet innehåller en översikt över [!DNL Marketo Engage]-källkopplingen, inklusive information om hur du autentiserar kopplingen, hur du mappar [!DNL Marketo Engage]-fält till Experience Data Model (XDM) och anslutningsens datalatens.

## Konfigurera Adobe organisationsmappning

Innan du kan skapa mappningsuppsättningar för [!DNL Marketo Engage] måste du först konfigurera Adobe organisationsmappning. Detaljerade anvisningar om hur du slutför detta finns i guiden [Konfigurera Adobe organisationsmappning för [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=sv-SE).

## Autentisera din [!DNL Marketo Engage]-anslutning

För att kunna ansluta [!DNL Marketo Engage] till Experience Platform måste du först hämta värden för `munchkinId`, `clientId` och `clientSecret`.

Se stegen som beskrivs i dokumentet [Verifiera din Marketo-källanslutning](./marketo-auth.md) för att hämta dina autentiseringsuppgifter.

## Konfigurera B2B-namnutrymmen och automatisk schemagenerering

Använd sedan verktyget för automatisk generering av B2B-namnutrymme och schema för att konfigurera din Experience Platform-utvecklarkonsol och Postman-miljö. På så sätt kan du automatiskt fylla i B2B-namnutrymmen och scheman. Detaljerade instruktioner finns i guiden om [hur du konfigurerar B2B-namnutrymmen och automatisk schemagenerering](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner som gör att du kan importera data från tredjepartskällor för användning i Experience Platform-tjänster i senare led.

Genom att följa XDM-standarder kan data integreras enhetligt i Experience Platform ekosystem, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM och dess roll i Experience Platform finns i [XDM-systemöversikten](../../../../xdm/home.md).

## Fältmappning från [!DNL Marketo Engage] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Marketo Engage] och Experience Platform måste Marketo källdatafält mappas till rätt mål-XDM-fält innan de hämtas till Experience Platform.

Mer information om fältmappningsregler mellan [!DNL Marketo Engage]-datamängder och Experience Platform finns i följande:

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

## Förväntad fördröjning av [!DNL Marketo Engage]-data på Experience Platform

I följande tabell visas den förväntade fördröjningen för att hämta [!DNL Marketo Engage]-data till Experience Platform, baserat på typen av förtäring och önskat mål:

| Mål | Förväntad svarstid |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minuter |
| Data Lake | &lt; 60 minuter |

>[!NOTE]
>
>Latenssiffrorna ovan representerar förväntningar på en 95-procentig konfidensnivå. Den faktiska latensen kan variera och i sällsynta fall sträcka sig över 50 %.

## Nästa steg och ytterligare resurser

I följande dokumentation finns mer information om hur du skapar en [!DNL Marketo Engage]-källanslutning:

* Mer information om hur du ansluter dina [!DNL Marketo Engage]-data till Experience Platform finns i självstudiekursen [Skapa en [!DNL Marketo Engage] källanslutning i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Mer information om hur du ställer in scheman och importerar anpassade aktivitetsdata finns i självstudiekursen [Skapa en källanslutning och ett dataflöde för  [!DNL Marketo Engage] anpassade aktivitetsdata](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Mer information om hur du migrerar din ECID-mappning från datauppsättningen [!DNL Person] till datamängden [!DNL Activity] finns i [Migreringsguiden för ECID-mappning](./migration.md).
* Mer information om den underliggande inställningen för B2B-namnutrymmen och scheman som används med [!DNL Marketo Engage] finns i dokumentationen för [B2B-namnutrymmen och scheman](./marketo-namespaces.md).
* Mer information om hur du hittar ditt [!DNL Marketo Engage] munchkin-ID och genererar dina autentiseringsuppgifter finns i [[!DNL Marketo Engage] autentiseringsguiden](./marketo-auth.md).
* Mer information om de specifika mappningsregler som gäller för [!DNL Marketo Engage]-datauppsättningar finns i dokumentationen om [[!DNL Marketo Engage] fältmappningar](../mapping/marketo.md).
* Allmän information om [!DNL Real-Time Customer Data Platform B2B Edition] och dess funktioner finns i dokumentationen om [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
