---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metadata-kommandon
topic: metadata
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Metadata-kommandon

För metadata i din datauppsättning stöds följande PSQL-kommandon för frågor:

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
| `\showtables` | Visar följande information: <br>namn: Namnet som tabellen ska refereras till.<br>datasetId: ID:t för den datauppsättning som lagras.<br>datauppsättning: Namnet på den datauppsättning som lagras.<br>beskrivning: En beskrivning av datauppsättningen.<br>lösta: Ett booleskt värde som anger om datauppsättningen har lösts i den aktuella sessionen eller inte. |
| `\timing` | Växlar visningen mellan av och på. Visningen är i millisekunder. Intervall som är längre än en sekund visas i formatet minuter:sekunder, med fälten timmar och dagar tillagda vid behov. |

Alla kommandon som börjar med `\d` kan kombineras. Du kan t.ex. skapa en lista `\dtsn` med alla tabeller, sekvenser och scheman. `\d` i sig visar alla synliga tabeller, vyer, materialiserade vyer och sekvenser.

Mer information om de kommandon som listas ovan finns i dokumentationen på [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Observera dock att inte alla alternativ som visas i PostgreSQL-dokumentationen stöds av [!DNL Experience Platform].

