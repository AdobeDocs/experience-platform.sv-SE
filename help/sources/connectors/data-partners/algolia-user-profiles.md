---
title: Algoliet-användarprofiler Source - översikt
description: Läs mer om källan för användarprofiler i Algoliet i Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/) är en kraftfull API-plattform för sökning och identifiering som gör att företag kan leverera snabba, relevanta och anpassningsbara sökupplevelser. Det ger sökmöjligheter i realtid med funktioner som typotolerans, filtrering, faceting och AI-driven relevansjustering. [!DNL Algolia] hjälper företag att förbättra användarinteraktionen, konverteringsgraden och den övergripande kundupplevelsen genom att tillhandahålla högpresterande söklösningar för webbplatser, e-handelsplattformar och applikationer.

Några av fördelarna med [!DNL Algolia]:

* Blixtsnabb sökning med snabba resultat.
* Högrelevanta rekommendationer från AI.
* Anpassningsbar rankning för att prioritera affärsbehoven.
* Skalbarhet för att enkelt hantera höga trafikbelastningar.

Mer information finns i [[!DNL Algolia] produktdokumentationen](https://resources.algolia.com/).

## Arkitektur

Självbetjäningskällor (Batch SDK) innehåller alla nödvändiga funktioner som autentisering, sidnumrering eller både fullständig och partiell datainhämtning. Källan [!DNL Algolia User Profiles] använder dessa funktioner för att slutföra integreringen.

![Arkitektur för integrering mellan Algoliet och Experience Platform](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Förhandskrav {#prerequisites}

Du måste slutföra följande nödvändiga steg innan du kan ansluta ditt [!DNL Algolia]-konto till Experience Platform.

1. Använd [[!DNL Algolia] instrumentpanelen](https://dashboard.algolia.com/users/sign_up) för att logga in på ditt [!DNL Algolia]-konto eller skapa ett nytt konto.
2. [Förbered ditt index](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/).
3. [Konfigurera dina facets](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [Skicka användarhändelser](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [Anpassa ditt index](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Algolia]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/abac/ui/permissions.md).

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till i en tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress i tillåtelselista ](../../ip-address-allow-list.md).

## Anslut ditt [!DNL Algolia]-konto till Experience Platform

När du är klar med kraven kan du fortsätta till nästa steg och [ansluta ditt [!DNL Algolia] konto till Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md).
