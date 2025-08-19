---
keywords: katalogtjänst; frågor; vanliga frågor; frågor; faq; dataset faq
title: Vanliga frågor och svar
description: Svar på de vanligaste frågorna om tjänsten Adobe Experience Platform Catalog och datauppsättningar.
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: 38f63f1fc985601c53925a529e603f47dc7fb58b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Vanliga frågor och svar {#faq}

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Catalog Service och datauppsättningar. Om du har frågor eller felsökning som rör andra Experience Platform-tjänster, inklusive problem som har uppstått i alla Experience Platform-API:er, kan du läsa [Experience Platform felsökningsguide](../landing/troubleshooting.md).

## Bevarandeprinciper och -regler {#retention-policies-and-rules}

### Vilka typer av datauppsättningar kan jag tillämpa regler för lagringspolicy på?

+++Svar

Du kan ställa in bevarandeprinciper för datauppsättningar som skapats med klassen ExperienceEvent XDM. För profiltjänsten kan bevarandeprinciper bara tillämpas på ExperienceEvent-datauppsättningar när de har aktiverats för profilen.

+++

### Kan jag ange olika bevarandeprinciper för datasjön och profiltjänst?

+++Svar

>[!NOTE]
>
>Kvarhållningsperioden för profiltjänsten kan bara uppdateras en gång var 30:e dag.

Ja, du kan tillämpa olika bevarandeprinciper för datasjön och profiltjänst.

+++

## Körning och timing av kvarhållningsjobb {#retention-job-execution-and-timing}

### Hur snart kommer datamängdens lagringsjobb att ta bort data från datasjötjänster?

+++Svar

Datauppsättningens förfallodatum utvärderas och bearbetas varje vecka och alla poster som har gått ut tas bort. En händelse anses ha upphört att gälla om den har importerats till Experience Platform i mer än 30 dagar (importdatum > 30 dagar) och dess händelsedatum överskrider den definierade kvarhållningsperioden.

+++

### Hur snart tar datauppsättningsarkiveringsjobbet bort data från profiltjänster?

+++Svar

När en kvarhållningsprincip har angetts tas befintliga händelser omedelbart bort från Experience Platform om deras händelsetidsstämpel överskrider kvarhållningsperioden. Nya händelser tas bort när deras tidsstämpel överskrider kvarhållningsperioden.

Om du till exempel tillämpar en 30-dagars förfalloprincip den 15 maj inträffar följande:

- Nya händelser får en 30-dagars förfallotid när de importeras.
- Befintliga händelser med en tidsstämpel som är äldre än 15 april tas omedelbart bort.
- Befintliga händelser med en tidsstämpel efter 15 april förfaller 30 dagar efter tidsstämpeln. En händelse från den 18 april skulle till exempel tas bort den 18 maj.

+++

## Användning och övervakning av datauppsättning

### Hur kan jag kontrollera min aktuella datauppsättningsanvändning?

+++Svar

Du kan visa den senaste lagringsstorleken på datamängdsnivå i datalinje och profil som separata mått på [!UICONTROL Datasets]-lagersidan. Du kan också sortera kolumnerna för att identifiera de största datauppsättningarna och se till att kvarhållningsprinciper tillämpas. Användning på sandlådenivå är tillgängligt på kontrollpanelen för licensanvändning. Mer information finns i [licensanvändningsdokumentationen](../dashboards/guides/license-usage.md).

+++

### Hur verifierar jag om datalagringsjobbet lyckades?

+++Svar

Du kan kontrollera tidsstämpeln för det senaste datalagringsjobbet i [Konfigurationsgränssnittet för datamängdsbevarande](./datasets/user-guide.md#data-retention-policy) och på lagersidan [!UICONTROL Datasets]. Rapporter om användning av tidigare datamängder är för närvarande inte tillgängliga, men är planerade för framtida releaser.

+++

## Dataåterställning {#data-recovery}

### Kan jag återställa borttagna data?

+++Svar

Nej, när lagringsprincipen tillämpas tas alla data som är äldre än kvarhållningsperioden bort permanent och kan inte återställas.

+++
