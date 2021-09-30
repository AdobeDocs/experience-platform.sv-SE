---
keywords: Experience Platform;hemmabruk;populära ämnen;Marketo Engage;markering för att engagera;markering för
solution: Experience Platform
title: Marketo Engage-kontakt
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över Marketo Engage-källkopplingen, inklusive information om autentisering, mappning och datalatens.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 50e92ac8c1eccc9ccfb6b078ad8b996817a6d693
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# [!DNL Marketo Engage] koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (nedan kallat&quot;[!DNL Marketo]&quot;) är en komplett lösning för lead-hantering och B2B-marknadsförare som vill omvandla kundupplevelser genom att engagera sig i varje fas av komplexa köpresor.

Med [!DNL Marketo]-källkopplingen kan du hämta B2B-data från [!DNL Marketo] till plattformen och hålla dessa data uppdaterade med plattformsanslutna program.

Det här dokumentet innehåller en översikt över [!DNL Marketo]-källkopplingen, inklusive information om hur du autentiserar kopplingen, hur du mappar [!DNL Marketo]-fält till Experience Data Model (XDM) och anslutningsens datalatens.

## Autentisera din [!DNL Marketo]-koppling

För att kunna ansluta [!DNL Marketo] till plattformen måste du först hämta värden för `munchkinId`, `clientId` och `clientSecret`.

Se stegen som beskrivs i [Verifiera din Marketo-källanslutning](./marketo-auth.md)-dokumentet för att hämta dina autentiseringsuppgifter.

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner som gör att du kan importera data från tredjepartskällor för användning i plattformstjänster längre fram i kedjan.

Genom att följa XDM-standarder kan data integreras enhetligt i plattformens ekosystem, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM och dess roll i Platform finns i [XDM-systemöversikt](../../../../xdm/home.md).

## Fältmappning från [!DNL Marketo] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Marketo] och Platform måste Marketo källdatafält mappas till rätt mål-XDM-fält innan de hämtas till Platform.

Mer information om fältmappningsregler mellan [!DNL Marketo]-datamängder och Platform finns i följande:

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

## Förväntad fördröjning för [!DNL Marketo]-data på plattformen

I följande tabell visas den förväntade fördröjningen för att hämta [!DNL Marketo]-data till plattformen, baserat på typen av förtäring och önskat mål:

| Destination | Förväntad svarstid |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60=&quot;&quot; minutes=&quot;&quot;> |

## Nästa steg och ytterligare resurser

I följande dokumentation finns mer information om hur du skapar en [!DNL Marketo]-källanslutning:

* Information om hur du ansluter dina [!DNL Marketo]-data till plattformen finns i självstudiekursen om att [skapa en Marketo-källkoppling i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Information om den underliggande inställningen för B2B-namnutrymmen och scheman som används med [!DNL Marketo] finns i dokumentationen för [B2B-namnutrymmen och scheman](./marketo-namespaces.md).
* Information om hur du hittar ditt [!DNL Marketo] munchkin-ID och genererar dina inloggningsuppgifter finns i [[!DNL Marketo] autentiseringsguiden](./marketo-auth.md).
* Mer information om de specifika mappningsregler som gäller för [!DNL Marketo]-datamängder finns i dokumentationen om [[!DNL Marketo] fältmappningar](../mapping/marketo.md).
