---
keywords: Experience Platform;hem;populära ämnen;PSQL;psql;Query service;query service;metadata;commands;metadata commands;metadata commands;
solution: Experience Platform
title: Metadata PostgreSQL-kommandon i frågetjänsten
description: En lista med PostgreSQL-kommandon som för närvarande stöds för att hämta metadata i Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Metadata [!DNL PostgreSQL]-kommandon i frågetjänsten

För metadata i din datauppsättning stöds följande [!DNL PostgreSQL]-kommandon för frågor:

>[!NOTE]
>
>Kommandona som listas nedan är skiftlägeskänsliga.

| Kommando | Beskrivning |
|------- | ------------|
| `\conninfo` | Visar information om den aktuella databasanslutningen. |
| `\d` | Visar en lista med alla synliga tabeller, vyer, materialiserade vyer, sekvenser och externa tabeller. |
| `\dE` | Visar en lista med externa tabeller. |
| `\df or \df+` | Visar en lista med funktioner. |
| `\di` | Visar en lista med index. |
| `\dm` | Visar en lista med materialiserade vyer. |
| `\dn` | Visar en lista med scheman (namnutrymmen). |
| `\ds` | Visar en lista med sekvenser. |
| `\dS` | Visar en lista med PostgreSQL-definierade tabeller. |
| `\dt` | Visar en lista med tabeller. |
| `\dT` | Visar en lista med datatyper. |
| `\dv` | Visar en lista med vyer. |
| `\encoding` | Visar kodningen för den aktuella klientteckenuppsättningen. |
| `\errverbose` | Upprepar det senaste serverfelmeddelandet med maximal noggrannhet. |
| `\l or \list` | Visar en lista med databaser på servern. |
| `\set` | Visar namn och värden för alla aktuella psql-variabler. |
| `\showtables` | Visar följande information: <br>name: Namnet som tabellen ska refereras till.<br>datasetId: ID:t för datauppsättningen som lagras.<br>datauppsättning: Namnet på den datauppsättning som lagras.<br>description: En beskrivning av datauppsättningen.<br>löste: Ett booleskt värde som anger om datauppsättningen har lösts i den aktuella sessionen eller inte. |
| `\timing` | Växlar visningen mellan av och på. Visningen är i millisekunder. Intervall som är längre än en sekund visas i formatet minuter:sekunder, med fälten timmar och dagar tillagda vid behov. |

Alla kommandon som börjar med `\d` kan kombineras. Du kan till exempel utfärda `\dtsn` för att visa en lista över alla tabeller, sekvenser och scheman. `\d` i sig visar alla synliga tabeller, vyer, materialiserade vyer och sekvenser.

Mer information om de kommandon som listas ovan finns i dokumentationen på [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Observera dock att inte alla alternativ som visas i [!DNL PostgreSQL]-dokumentationen stöds av [!DNL Experience Platform].
