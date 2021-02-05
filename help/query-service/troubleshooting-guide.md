---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;felsökningsguide;faq;felsökning;
solution: Experience Platform
title: Felsökningsguide för frågetjänst
topic: troubleshooting
description: Det här dokumentet innehåller information om vanliga felkoder som du stöter på och möjliga orsaker.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 2%

---


# [!DNL Query Service] Felsökningsguide

## REST API-fel

| HTTP-statuskod | Beskrivning | Möjliga orsaker |
| ---------------- | ----------- | --------------- |
| 400 | Felaktig begäran | Felaktig eller ogiltig fråga |
| 401 | Autentiseringen misslyckades | Ogiltig autentiseringstoken |
| 500 | Internt serverfel | Internt systemfel |

## PostgreSQL API-fel

| Felkod och anslutningsstatus | Beskrivning | Möjlig orsak |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start - autentisering | Ogiltigt lösenord | Ogiltig autentiseringstoken |
| **28000** Start - autentisering | Ogiltig auktoriseringstyp | Ogiltig auktoriseringstyp. Måste vara `AuthenticationCleartextPassword`. |
| **42P12** Start - autentisering | Inga tabeller hittades | Inga tabeller hittades för användning |
| **42601** Fråga | Syntaxfel | Ogiltigt kommando eller syntaxfel |
| **58000** Fråga | Systemfel | Internt systemfel |
| **42P01** Query | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P07** Query | Tabellen finns | Tabellen finns redan med samma namn (CREATE TABLE) |
| **53400** Fråga | LIMIT överskrider maxvärdet | Användaren angav en LIMIT-sats som är högre än 100 000 |
| **53400** Fråga | Tidsgräns för instruktion | Den inskickade livebeskrivningen tog mer än maximalt 10 minuter |
| **08P01** Ej tillämpligt | Meddelandetypen stöds inte | Meddelandetypen stöds inte |
