---
title: Konfigurationsguide för länkning av identitetsdiagram
description: Lär dig de rekommenderade stegen som ska följas när du implementerar data med länkningsregler för identitetsdiagram.
badge: Beta
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Konfigurationsguide för länkning av identitetsdiagram

Läs det här dokumentet för att få en stegvis handledning som du kan följa när du implementerar dina data med Adobe Experience Platform Identity Service.

Stegvisa dispositioner:

1. [Skapa nödvändiga identitetsnamnutrymmen](#namespace)
2. [Använd verktyget för diagramsimulering för att bekanta dig med algoritmen för identitetsoptimering](#graph-simulation)
3. [Använd identitetsinställningsverktyget för att ange unika namnutrymmen och konfigurera prioritetsklassificeringar för dina namnutrymmen](#identity-settings)
4. [Skapa ett XDM-schema (Experience Data Model)](#schema)
5. [Skapa en datauppsättning](#dataset)
6. [Importera data till Experience Platform](#ingest)

## Förutsättningar för implementering

Innan du kan komma igång måste du se till att autentiserade händelser i systemet alltid innehåller en personidentifierare.

## Ange behörigheter {#set-permissions}

Det första steget i implementeringsprocessen för identitetstjänsten är att se till att ditt Experience Platform-konto läggs till i en roll som har de behörigheter som krävs. Administratören kan konfigurera behörigheter för ditt konto genom att gå till behörighetsgränssnittet i Adobe Experience Cloud. Därifrån måste ditt konto läggas till i en roll med följande behörigheter:

* [!UICONTROL View Identity Settings]: använd den här behörigheten för att kunna visa unika namnutrymmen och namnområdesprioritet på ID-namnutrymmets bläddringssida.
* [!UICONTROL Edit Identity Settings]: använd den här behörigheten för att kunna redigera och spara dina identitetsinställningar.

Mer information om behörigheter finns i [behörighetshandboken](../../access-control/abac/ui/permissions.md).

## Skapa dina identitetsnamnutrymmen {#namespace}

Om dina data kräver det måste du först skapa lämpliga namnutrymmen för din organisation. Anvisningar om hur du skapar ett anpassat namnutrymme finns i handboken [Skapa ett anpassat namnutrymme i användargränssnittet](../features/namespaces.md#create-custom-namespaces).

## Använda diagramsimuleringsverktyget {#graph-simulation}

Gå sedan till [diagramsimuleringsverktyget](./graph-simulation.md) på arbetsytan för identitetstjänstens användargränssnitt. Du kan använda verktyget för diagramsimulering för att simulera identitetsdiagram, som har skapats med olika konfigurationer av unika namnutrymmes- och namnområdesprioriteter.

Genom att skapa olika konfigurationer kan du använda verktyget för diagramsimulering för att lära dig och förstå hur identitetsoptimeringsalgoritmen och vissa konfigurationer kan påverka hur diagrammet fungerar.

## Konfigurera identitetsinställningar {#identity-settings}

När du har fått en bättre uppfattning om hur du vill att diagrammet ska fungera går du till [identitetsinställningsverktyget](./identity-settings-ui.md) på arbetsytan för identitetstjänstens gränssnitt.

Använd verktyget för identitetsinställningar för att ange unika namnutrymmen och konfigurera namnutrymmen efter prioritetsordning. När du är klar med att använda inställningarna måste du vänta minst sex timmar innan du kan fortsätta att importera data, eftersom det tar minst sex timmar innan nya inställningar återspeglas i identitetstjänsten.

## Skapa ett XDM-schema {#schema}

När dina unika namnutrymmen och namnområdesprioriteter har fastställts kan du nu fortsätta med den nödvändiga konfigurationen för att kunna importera dina data. Först måste du skapa ett XDM-schema. Beroende på dina data kan du behöva skapa ett schema för både XDM Individual Profile och XDM ExperienceEvent.

Om du vill importera data till kundprofilen i realtid måste du se till att schemat innehåller minst ett fält som har angetts som primär identitet. Genom att ställa in en primär identitet kan du aktivera ett givet schema för profilinmatning.

Instruktioner om hur du skapar ett schema finns i guiden om att [skapa ett XDM-schema i användargränssnittet](../../xdm/tutorials/create-schema-ui.md).

## Skapa en datauppsättning {#dataset}

Skapa sedan en datauppsättning som ger en struktur för de data som du ska importera. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar fungerar tillsammans med scheman, och om du vill importera data till kundprofilen i realtid måste datauppsättningen aktiveras för profilinmatning. För att din datauppsättning ska kunna aktiveras för profilen måste den referera till ett schema som är aktiverat för profilinmatning.

Instruktioner om hur du skapar en datauppsättning finns i [användargränssnittsguiden för datauppsättningar](../../catalog/datasets/user-guide.md).

## Infoga era data {#ingest}

Nu bör du ha följande:

* Nödvändiga behörigheter för att komma åt identitetstjänstens funktioner.
* Namnutrymmen för dina data.
* Utformade unika namnutrymmen och konfigurerade prioriteter för dina namnutrymmen.
* Minst ett XDM-schema. (Beroende på dina data och specifika användningsfall kan du behöva skapa både profil- och upplevelsehändelsescheman.)
* En datauppsättning som baseras på ditt schema.

När du har alla objekt som listas ovan kan du börja importera dina data till Experience Platform. Du kan utföra dataöverföring på flera olika sätt. Du kan använda följande tjänster för att skicka data till Experience Platform:

* [Inmatning av gruppbearbetning och direktuppspelning](../../ingestion/home.md)
* [Datainsamling i Experience Platform](../../collection/home.md)
* [Experience Platform Källor](../../sources/home.md)

>[!TIP]
>
>När data har importerats ändras inte nyttolasten för XDM-rådata. Du kan fortfarande se dina primära identitetskonfigurationer i användargränssnittet. Dessa konfigurationer åsidosätts dock av identitetsinställningarna.

Använd alternativet **[!UICONTROL Beta feedback]** på identitetstjänstens arbetsyta för att få feedback.