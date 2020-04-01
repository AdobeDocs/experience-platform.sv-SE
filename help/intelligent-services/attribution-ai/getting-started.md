---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Komma igång med Attribution AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Komma igång med Attribution AI

Följande handledningar kräver förståelse av de olika Adobe Experience Platform-tjänsterna som används för att använda Attribution AI. Innan du börjar med självstudiekurserna bör du läsa följande dokument:

- [Experience Data Model (XDM) - systemöversikt](../../xdm/home.md): XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som bygger på Experience Platform, kan leverera rätt budskap till rätt person i rätt kanal vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, XDM System, används för att driva Experience Data Model-scheman för användning av plattformstjänster.
- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Det här dokumentet innehåller en introduktion till XDM-scheman (Experience Data Model) och de byggstenar, principer och bästa metoderna för att sammanställa scheman som ska användas i Adobe Experience Platform.
- [Byggscheman](../../xdm/tutorials/create-schema-ui.md): I den här självstudiekursen beskrivs stegen för hur du skapar ett schema med Schemaredigeraren i Experience Platform.

Attribution AI kräver att datauppsättningar följer CEE-schemat (Consumer Experience Events), som är en blandning i [Experience Data Model](../../xdm/home.md) (XDM). Kontakta Adobes support på attributionai-support@adobe.com för att implementera eller göra ändringar i dessa data. Om det finns uppgifter om medieleveranser kan du göra ytterligare analyser, till exempel inkrementella intäkter och avkastning. Om det finns tillgängliga kundprofildata kan du attribuera krediter till kundprofilnivån ytterligare.

## Terminologi

- **Konverteringshändelse:** Digitala event eller digital interaktion som kunderna gör för att ange en milstolpe i riktning mot ett mål, som konferensregistreringar. Ytterligare exempel är betalda konverteringar, kostnadsfria kontoregistreringar eller kvalificering för en egenskap.

- **Pekpunkt:** Alla digitala händelser eller digitala interaktioner som kunderna gör på vägen mot ett mål. Exemplen omfattar tidigare köprelaterade marknadsföringssatsningar, visningar av webbannonsering och betalda sökklick.

## Få åtkomst till och fråga efter bakgrundsmusik

>[!NOTE] Om du inte behöver fråga eller komma åt bakgrundsmusik kan du hoppa över det här steget och fortsätta till [användargränssnittshandboken](./user-guide.md).

Åtkomst till och frågor om poäng för Attribution AI görs via Snowflake. För närvarande måste du skicka e-post till Adobes support på attributionai-support@adobe.com för att kunna konfigurera och ta emot inloggningsuppgifterna till ditt läsarkonto för Snowflake eller för att massexportera rådata.

När Adobes support har bearbetat din begäran får du en URL för läsarkontot till Snowflake och motsvarande uppgifter nedan:

- Snöflinga URL
- Användarnamn
- Lösenord

## Nästa steg

När du är klar och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa guiden [för användargränssnittet för](./user-guide.md)Attribution AI. I den här guiden får du hjälp med att skapa en instans och skicka in den för utbildning och poängsättning.