---
description: Om du vill använda mål-SDK måste partnerföretaget uppfylla de krav som anges i det här dokumentet.
title: Krav för integrering
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Krav för integrering

Om du vill använda mål-SDK kontrollerar du att du uppfyller de tekniska kraven och villkoren för partnerskap som anges i avsnitten nedan.

## Tekniska krav/API-krav

1. Du har en REST API-slutpunkt som Adobe Experience Platform kan använda för att leverera följande typer av data till:
   * Information om segmentmedlemskap;
   * Profilidentitetsinformation.
   * (Valfritt) Ytterligare attribut för profilberikning.
2. REST API-slutpunkten stöder autentisering av API-tokenbärare eller OAuth 2.0-autentiseringsprotokollet.
3. (Valfritt) Du har ett segment för att skapa/uppdatera/ta bort API eller API-slutpunkt för programmatisk metadatahantering.

## Partnerskapskrav

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) och vill använda mål-SDK läser du Partnerkraven för ISV och SI i [avsnittet Hämta åtkomst](./overview.md#get-access).
