---
title: Data Distiller Overview
description: En sammanfattning av användningsgränserna för Data Distiller för Query Service-data i relation till ditt licensieringsberättigande.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Distiller - översikt

Data Distiller är ett paket som innehåller en deluppsättning av funktionerna från Adobe Experience Platform. Med Data Distiller kan du färdigställa data efter intag (t.ex. rengöring, formning och manipulering) för kundprofiler i realtid eller för analytiska syften genom att köra batchfrågor i Query Service. Din användning av Data Distiller är beroende av din behörighet för plattformsbaserade program.

## Licensanvändning {#license-usage}

The  [Kontrollpanel för användning av Distiller-licenser](./license-usage.md) är tillgängligt när du har köpt databearbetningstimmar för Distiller. Kontrollpanelen för licensanvändning hjälper dig att övervaka förbrukningen av berättigade beräkningstimmar. Se [Användningsdokument för Distiller-licenser](./license-usage.md) om du vill visa viktig information om hur din organisations Query Service-licens används.

## Omfångsparametrar {#scoping-parameters}

Omfångsparametrar är användarbegränsningar som relaterar till omfånget i den konfiguration som krävs och definieras av din licenskapacitet. Utan tillägg är Data Distiller parametrar för omfång följande:

* **Beräkna timmar**: Du kan använda PSQL eller API:t för frågetjänsten för att köra batchfrågor som körs i valfri sandlåda (schemalagd eller på annat sätt) för att skanna och skriva data. Detta innebär att dina tilldelade beräkningstimmar per år används, enligt villkoren i licensavtalet. Totalt antal beräkningstimmar ackumuleras för alla sandlådor.
* **Insamlade data**: Data som hämtas in till Adobe Experience Platform och som kan hämtas med Data Distiller omfattas av de begränsningar som beskrivs i din aktuella licens för Adobe Real-time Customer Data Platform, Customer Journey Analytics och/eller Adobe Journey Optimizer.
* **Data Lake-lagring**: Data Lake Storage som ingår i din aktuella licens för Adobe Real-time Customer Data Platform, Customer Journey Analytics och/eller Adobe Journey Optimizer kan också användas med Data Distiller. Data Lake Storage är en delad funktion.
* **Frågetjänstanvändare**: Antalet användare av frågetjänsten som anges i din aktuella licens för Adobe Real-time Customer Data Platform, Customer Journey Analytics och/eller Adobe Journey Optimizer kan också användas med Data Distiller. Query Service-användare är en delad funktion.

## Guardrails

Se [Skyddsutkast för frågetjänst](../guardrails.md) dokument om standardanvändningsgränser för frågetjänstdata i relation till ditt licensberättigande.

## Statiska gränser

En statisk gräns är den gräns som gäller funktionalitetsgränserna för Adobe Experience Platform Activation. [Mer information om Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) finns i hjälpdokumenten för Adobe. En sammanfattning av de statiska gränserna för Data Distiller finns nedan. Mer fullständig information finns i Query Service-skyddsdokumentet.

* **Batchfrågor**: Schemalagda batchfrågor tar slut efter 24 timmar.
* **Frågetjänst**: Du kan använda frågetjänsten för följande syften:
   * Så här kör du SQL-frågor för dataanalys och förberedelse av dataöverföringar efter konsumtion (rengöring, formning och manipulering).
   * Om du vill köra SQL-frågor för att skapa rollup-mätvärden som ska visas direkt i ett BI-verktyg.
   * För att snabbt inspektera data i Adobe Experience Platform.
   * Generera meningsfulla insikter från era data.
* **API-anrop för rapportering**: För att säkerställa att frågor körs på aggregerade data med rapporterings-API:t har tillräckligt med resurser för att kunna köras effektivt. Detta inkluderar frågor som förbättrar befintliga datamodeller, t.ex. de som tillhandahålls av Real-time Customer Data Platform. Rapporterings-API:t spårar resursanvändning genom att tilldela kortplatser för samtidig användning till varje fråga. Högst fyra API-anrop för rapportering är tillgängliga samtidigt. Om du får åtkomst till rapporterings-API:t via ett BI-verktyg och kräver fler kortplatser för samtidig användning, krävs en BI-server.


