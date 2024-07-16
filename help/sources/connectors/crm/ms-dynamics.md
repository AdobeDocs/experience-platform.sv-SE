---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector - översikt
description: Lär dig hur du ansluter Microsoft Dynamics till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics-koppling

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du får möjlighet att strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inhämtning av data från ett CRM-system från tredje part. Stöd för CRM-providers omfattar [!DNL Microsoft Dynamics].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Fältmappning från [!DNL Microsoft Dynamics] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Microsoft Dynamics] och plattformen måste [!DNL Microsoft Dynamics]-källdatafälten mappas till rätt mål-XDM-fält innan de hämtas till plattformen.

Mer information om fältmappningsregler mellan [!DNL Microsoft Dynamics]-datamängder och plattformen finns i följande:

- [Kontakter](../adobe-applications/mapping/dynamics.md#contacts)
- [Leads](../adobe-applications/mapping/dynamics.md#leads)
- [Konton](../adobe-applications/mapping/dynamics.md#accounts)
- [Möjligheter](../adobe-applications/mapping/dynamics.md#opportunities)
- [Kontaktroller för affärsmöjlighet](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Kampanjer](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marknadsföringslista](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Medlemmar i marknadsföringslistan](../adobe-applications/mapping/dynamics.md#marketing-list-members)

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Microsoft Dynamics] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Microsoft Dynamics] till [!DNL Platform] med API:er

- [Skapa en Microsoft Dynamics-basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/ms-dynamics.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Microsoft Dynamics] till [!DNL Platform] med användargränssnittet

- [Skapa en Microsoft Dynamics-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/dynamics.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
