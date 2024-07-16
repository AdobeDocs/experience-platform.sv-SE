---
title: API-handbok för Privacy Service
description: Lär dig hur du använder Privacy Service-API:t för att programmässigt hantera sekretessjobb för Adobe Experience Cloud-program som stöds.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# API-guide för [!DNL Privacy Service]

Privacy Services-API:t innehåller flera slutpunkter som gör att du kan hantera sekretessjobb för din organisation programmatiskt. Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

>[!NOTE]
>
>I den här handboken beskrivs hur du använder API:t för [!DNL Privacy Service]. Mer information om hur du använder användargränssnittet finns i översikten [Privacy Servicens användargränssnitt](../ui/overview.md).

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [Privacy Services-API-referensen](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Sekretessjobb

När Privacy Servicen tar emot en begäran om åtkomst till eller radering av personuppgifter för ett ämne, skapar systemet sekretessjobb för att uppfylla denna begäran. Varje sekretessjobb innehåller identitetsinformation om den registrerade, metadata om den Adobe Experience Cloud-produkt som jobbet avser samt behandlingens status.

Med slutpunkten `/jobs` kan du skapa och hämta sekretessjobb för din organisation. Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för sekretessjobb](./privacy-jobs.md).

## Godkännande

Vissa bestämmelser kräver uttryckligt samtycke från kunden innan deras personuppgifter kan samlas in. Med slutpunkten `/consent` kan du bearbeta förfrågningar om kundgodkännande och integrera dem i ditt sekretessarbetsflöde. Mer information finns i guiden [för godkännande](./consent.md).

## Nästa steg

Om du vill börja ringa anrop med Privacy Service-API:t läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
