---
keywords: Experience Platform;hemmabruk;populära ämnen;
title: Felsökningsguide för dataprep
topic-legacy: troubleshooting
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Data Prep.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: 4bb21ce5861419964b80a827269e40ef3e6483f8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# [!DNL Data Prep] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Data Prep]samt en felsökningsguide för vanliga fel. Om du har frågor och felsökningsinformation om plattforms-API:er i allmänhet kan du läsa [Felsökningsguide för Adobe Experience Platform API](../landing/troubleshooting.md).

## Vanliga frågor och svar 

Nedan följer en lista med vanliga frågor och svar om [!DNL Data Prep] och deras svar.

### Hur åtgärdas transformeringsfel?

[!DNL Data Prep] lokaliserar alla omformningsfel till den kolumn där de inträffade. Det innebär att kolumnen har värdet null och att resten av raden kommer att fortsätta att bearbetas. Dessa transformeringsproblem loggas som **Varningar**. Vi rekommenderar att du granskar varningarna med jämna mellanrum och justerar omformningslogiken för att ta hänsyn till omformningsproblemen. Detta kommer att öka kvaliteten på de data som hämtas in till Experience Platform.

Om kolumnerna är markerade som **Obligatoriskt** har upphävts på grund av transformeringsproblem, så kommer raden inte att kapslas in. När partiell datainmatning är aktiverat kan du ange tröskelvärdet för sådana avvisningar innan hela flödet misslyckas. Om attributet null inte påverkade några valideringar på schemanivå kommer raden att fortsätta att kapslas.

Alla rader som är ogiltiga, även utan omformningsfel, kommer också att refuseras. Ett datainmatningsflöde kan till exempel ha en genomströmningsmappning (ingen omformningslogik) till ett obligatoriskt fält och det finns inget inkommande värde för det attributet. Den här raden kommer att refuseras.

### Hur kan jag undgå specialtecken i ett fält?

Du kan undvika specialtecken i ett fält genom att använda `${...}`. JSON-filer som innehåller fält med punkt (`.`) stöds inte av den här mekanismen. Vid interaktion med hierarkier, om ett underordnat attribut har en punkt (`.`) måste du använda ett omvänt snedstreck (`\`) för att undvika specialtecken. Till exempel: `address` är ett objekt som innehåller attributet `street.name`kan det sedan kallas `address.street\.name` i stället för `address.street.name`.
