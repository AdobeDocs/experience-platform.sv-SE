---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Felsökningsguide för Adobe Experience Platform Query Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---


# Fel och felsökning

## REST API-fel

| HTTP-statuskod | Beskrivning | Möjliga orsaker |
| ---------------- | ----------- | --------------- |
| 400 | Felaktig begäran | Felaktig eller ogiltig fråga |
| 401 | Autentiseringen misslyckades | Ogiltig autentiseringstoken |
| 500 | Internt serverfel | Internt systemfel |

## PostgreSQL API-fel

| Felkod och anslutningsstatus | Beskrivning | Möjlig orsak |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start-up - authentication | Ogiltigt lösenord | Ogiltig autentiseringstoken |
| **28000** Start-up - authentication | Ogiltig auktoriseringstyp | Ogiltig auktoriseringstyp. Måste vara `AuthenticationCleartextPassword`. |
| **42P12** Start - autentisering | Inga tabeller hittades | Inga tabeller hittades för användning |
| **42601** Fråga | Syntaxfel | Ogiltigt kommando eller syntaxfel |
| **58000** Fråga | Systemfel | Internt systemfel |
| **42P01** -fråga | Tabellen hittades inte | Det gick inte att hitta tabellen som angavs i frågan |
| **42P07** -fråga | Tabellen finns | Tabellen finns redan med samma namn (CREATE TABLE) |
| **53400** Fråga | LIMIT överskrider maxvärdet | Användaren angav en LIMIT-sats som är högre än 100 000 |
| **53400** Fråga | Tidsgräns för instruktion | Den inskickade livebeskrivningen tog mer än maximalt 10 minuter |
| **08P01** Ej tillämpligt | Meddelandetypen stöds inte | Meddelandetypen stöds inte |
