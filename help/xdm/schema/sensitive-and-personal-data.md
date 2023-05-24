---
title: Känslig och personlig information i XDM
description: Läs om viktiga aspekter av känslig personlig information (SPI) och personligt identifierbar information (PII) i Experience Data Model (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 9785b252b7c9cb3513858476753b6b4f71277ed7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Känslig och personlig information i XDM

Experience Data Model (XDM) innehåller standarddatastrukturer för användning i Adobe Experience Platform, så att ni kan samla in data om kundupplevelser. Dessa data kan innehålla känslig personlig information (SPI) och personligt identifierbar information (PII), t.ex. kundens e-postadress, namn, konto-ID och andra datafält.

Organisationsregler och juridiska sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR) tillämpar begränsningar för hur SPI och PII kan samlas in, lagras, användas och delas. Därför är det viktigt att tänka på vilka fält som representerar känslig eller personlig information i datamodellen och se till att åtgärderna följer organisatoriska och juridiska riktlinjer.

Det här dokumentet beskriver viktiga aspekter av känsliga och personuppgifter i XDM.

## Bestämma vilka fält som innehåller känsliga eller personuppgifter

Vad som utgör SPI och PII är mycket sammanhangsberoende, och det är därför upp till er att förstå er datamodell, er affärsverksamhet och tillämpliga bestämmelser för att avgöra vilka schemafält som representerar känsliga eller personuppgifter.

Kundernas juridiska behörighet påverkar till exempel direkt vilken information som anses vara känslig. Den allmänna dataskyddsförordningen innehåller kraftfulla definitioner för SPI och PII, men kunder utanför Europeiska ekonomiska samarbetsområdet (EES) kan omfattas av olika definitioner och begränsningar.

## Hantera känsliga och personuppgifter

På samma sätt som definitionerna för känsliga och personuppgifter är begränsningarna för att hantera dessa data också sammanhangsspecifika.

Kundens samtycke är ofta en viktig faktor när det gäller vilka data som kan samlas in och behandlas, och för vilka syften. Beroende på vilken juridisk behörighet dina kunder har kan uttryckligt samtycke krävas för att deras känsliga och personuppgifter ska kunna samlas in. Även i de fall där explicit samtycke inte krävs gäller fortfarande begränsningar för datahantering beroende på vad sekretessmeddelandet säger till kunden.

Kontakta ditt juridiska team för att få reda på hur känsliga och personliga uppgifter ska hanteras i era affärssituationer.

## Begränsa användningen av känsliga och personuppgifter

XDM har en mängd standardfältgrupper och datatyper som beskriver relevanta, ofta använda datastrukturer som stärker kundupplevelserna. Om en rekommenderad standardresurs innehåller begränsade fält som du inte vill inkludera i dina scheman behöver du dock inte använda den resursen.

Med Platform kan ni definiera egna fältgrupper och datatyper, vilket ger er full kontroll över hur data är strukturerade om några tillgängliga standardresurser inte uppfyller era behov. Mer information om hur du definierar anpassade resurser finns i följande dokumentation:

* [Skapa en anpassad fältgrupp](../ui/resources/field-groups.md#create)
* [Skapa en anpassad datatyp](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## Nästa steg

Det här dokumentet innehöll viktiga överväganden om känsliga och personuppgifter i XDM. Mer information om hur du utformar dina scheman så att de bäst passar ditt företag finns i guiden på [bästa praxis för datamodellering](./best-practices.md).

Mer information om datastyrning och sekretesskapacitet i Experience Platform finns i översikten på [styrning, integritet och säkerhet](../../landing/governance-privacy-security/overview.md).
