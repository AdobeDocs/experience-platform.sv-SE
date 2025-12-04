---
title: onBeforeLinkClickSend
description: Återanrop som körs precis innan data för länkspårning skickas.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Det här återanropet är föråldrat. Använd [`clickCollection.filterClickDetails`](clickcollection.md) i stället.

Med `onBeforeLinkClickSend`-återanropet kan du registrera en JavaScript-funktion som kan ändra länkspårningsdata som du skickar precis innan dessa data skickas till Adobe. Du kan ändra objektet `xdm` eller `data`, inklusive möjligheten att lägga till, redigera eller ta bort element. Du kan också villkorligt avbryta sändningen av data helt och hållet, t.ex. med identifierad robottrafik på klientsidan.

Det här återanropet körs bara om [`clickCollectionEnabled`](clickcollectionenabled.md) är aktiverat och `filterClickDetails` inte innehåller någon registrerad funktion.

Om [`onBeforeEventSend`](onbeforeeventsend.md) och `onBeforeLinkClickSend` båda innehåller registrerade funktioner körs `onBeforeLinkClickSend` först.

>[!WARNING]
>
>Det här återanropet tillåter användning av anpassad kod. Om kod som du inkluderar i återanropet genererar ett ej infångat undantag avbryts bearbetningen för händelsen. Data skickas inte till Adobe.

## `onBeforeLinkClickSend` och `filterClickDetails`

Återanropet [`clickCollection.filterClickDetails`](clickcollection.md) är utformat för att ersätta `onBeforeLinkClickSend`. Adobe rekommenderar starkt att du inte tilldelar återanropsfunktioner till båda samtidigt. Om du tilldelar en återanropsfunktion till både `filterClickDetails` och `onBeforeLinkClickSend` använder biblioteket följande logik:

* Endast `filterClickDetails` körs. Det gör inte `onBeforeLinkClickSend`.
* Händelsegruppering `clickCollection.eventGroupingEnabled` fungerar inte.
