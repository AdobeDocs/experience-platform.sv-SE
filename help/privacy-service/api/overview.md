---
title: API-handbok för Privacy Service
description: Lär dig hur du använder Privacy Service-API:t för att programmässigt hantera sekretessjobb för Adobe Experience Cloud-program som stöds.
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: bda8d0ee1db4b58b4b856a23a8790cd7f76c0656
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# [!DNL Privacy Service] API-guide

Privacy Services-API:t innehåller flera slutpunkter som gör att du kan hantera sekretessjobb för din organisation programmatiskt. Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

>[!NOTE]
>
>Den här guiden beskriver hur du använder [!DNL Privacy Service] API. Mer information om hur du använder användargränssnittet finns i [Översikt över användargränssnittet i Privacy Service](../ui/overview.md).

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [API-referens för Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Sekretessjobb

När Privacy Servicen tar emot en begäran om åtkomst till eller radering av personuppgifter för ett ämne, skapar systemet sekretessjobb för att uppfylla denna begäran. Varje sekretessjobb innehåller identitetsinformation om den registrerade, metadata om den Adobe Experience Cloud-produkt som jobbet avser samt behandlingens status.

The `/jobs` kan du skapa och hämta sekretessjobb för din organisation. Om du vill lära dig hur du använder den här slutpunkten kan du läsa [slutpunktshandbok för sekretessjobb](./privacy-jobs.md).

## Godkännande

Vissa bestämmelser kräver uttryckligt samtycke från kunden innan deras personuppgifter kan samlas in. The `/consent` Med slutpunkten kan du bearbeta förfrågningar om kundgodkännande och integrera dem i ditt sekretessarbetsflöde. Se [slutpunktsguide för samtycke](./consent.md) om du vill veta mer.

## Nästa steg

Om du vill börja ringa anrop med Privacy Services-API:t läser du [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.
