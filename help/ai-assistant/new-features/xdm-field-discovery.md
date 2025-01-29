---
title: XDM-fältidentifiering med AI Assistant
description: Läs det här dokumentet och lär dig hur du kan använda AI Assistant för identifiering av XDM-fält (Experience Data Model).
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 041034c6-da45-437f-ad46-f9c2ded9f82c
source-git-commit: 58cf5d90d70239a4b47c600bd3a7a37129b07dc3
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# XDM-fältidentifiering med AI Assistant

>[!AVAILABILITY]
>
>Den här funktionen är i Alpha och är kanske inte tillgänglig för din organisation. Om du vill delta i programmet Alpha och få tillgång till den här funktionen kontaktar du ditt kontoteam på Adobe.

Du kan använda AI Assistant för att söka efter och identifiera XDM-fält (Experience Data Model) som du sedan kan använda för att skapa målgrupper i Experience Platform.

Läs följande tabell för frågor och uppmaningsmönster som stöds för identifiering av XDM-fält i AI Assistant.

>[!TIP]
>
>Fråge- och promptmönstren kan vara desamma för olika användningsområden, men den exakta formuleringen av en fråga varierar beroende på vilka XDM-fält och -scheman som används för en viss sandlåda.

| Frågetyp | Fråga/fråga-mönster | Exempel |
| --- | --- | --- |
| XDM-fältidentifiering efter datavän eller dataområde | Visa de XDM-fält som används för att representera {DATA_DOMAIN/AREA}. | <ul><li>Visa mig de XDM-fält som används för att representera data om samtycke.</li><li>Visa de XDM-fält som används för att representera information om e-postprenumerationer.</li></ul> |
| XDM-fältidentifiering efter allmänt fältnamn | <ul><li>Visa XDM-fälten som hör till {DATA_DOMAIN/AREA}.</li><li>Vilka XDM-fält innehåller {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Visa XDM-fälten för order.</li><li>Visa XDM-fälten för interaktionsinformation.</li><li>Vilket XDM-fält innehåller besökar-ID:n?</li><li>Vilket XDM-fält innehåller produktkategorier?</li></ul> |
| XDM-fältidentifiering per datamodellrad | <ul><li>Visa alla fält i {FIELD_GROUP/CLASS_NAME} som innehåller {GENERAL_FIELD_NAME}.</li><li>Vad är {FIELD_GROUP/CLASS_NAME} för XDM-fältet {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Visa alla fält i fältgruppen som innehåller produktdata.</li><li>Visa alla fält i fältgruppen som innehåller analysdata.</li><li>Vilken klass har XDM-fältet förnamn?</li><li>Vilken klass har XDM-fältets e-postprenumerationer?</li></ul> |
| Fråga om utökade beskrivningar samt fältnamn | {FIELD_DISCOVERY_QUERY}. Inkludera även förbättrade beskrivningar. | <ul><li>Visa mig de XDM-fält som används för att representera data om samtycke. Ta även med den utökade beskrivningen för fältet.</li><li>Visa XDM-fälten för interaktionsinformation. Ta även med den utökade beskrivningen för fältet.</li></ul> |

{style="table-layout:auto"}
