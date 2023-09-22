---
title: Prospekt
description: Lär dig hur du skapar och använder profiler för potentiella kunder för att samla in information om okända kunder med hjälp av tredjepartsinformation.
type: Documentation
source-git-commit: 1973fbe858fc0a266936faf6060e467c108fedf6
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---


# Prospekteringsprofiler

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke.

Prospektprofiler används för att representera personer som ännu inte har interagerat med ditt företag men som du vill kontakta. Med profiler för potentiella kunder kan ni komplettera era kundprofiler med attribut från betrodda tredjepartspartners.

## Bläddra {#browse}

Om du vill komma åt profiler för potentiella kunder väljer du **[!UICONTROL Profiles]** i **[!UICONTROL Prospects]** -avsnitt.

Sidan **[!UICONTROL Browse]** visas. En lista över alla profiler för potentiella kunder för din organisation visas.

![The [!UICONTROL Profiles] knappen är markerad och visar [!UICONTROL Browse] sida för profiler för potentiella kunder.](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>Även om de flesta surffunktionerna mellan kundprofiler och profiler för potentiella kunder är desamma, är du **inte** Bläddra bland profiler för potentiella kunder genom att slå samman principer. Detta beror på att profiler för potentiella kunder automatiskt styrs av en systemdesignad, tidsbaserad sammanslagningsprincip. Mer information om sammanfogningsprinciper finns i [översikt över sammanfogningsprincip](../merge-policies/overview.md).

Mer information om webbläsarprofiler finns i [bläddra i avsnittet i användarhandboken för profilen](./user-guide.md#browse-identity).

## Information om potentiell profil {#profile-details}

>[!IMPORTANT]
>
>En profil för potentiell kund upphör automatiskt att gälla efter 25 dagars vistelse i Adobe Experience Platform.

Om du vill visa mer information om en viss profil för potentiella kunder väljer du en profil på [!UICONTROL Browse] sida.

![En profil för potentiell kund markeras på bläddringssidan.](../images/prospect-profile/select-specific-profile.png)

Information om den potentiella kundens profil visas, inklusive de attribut som är kopplade till profilen och målgruppsmedlemskapet.

![Sidan med information om profil för potentiell kund visas.](../images/prospect-profile/profile-details.png)

Mer information finns på [visa profilinformationsdelen i användarhandboken för profilen](./user-guide.md#profile-detail).

Du kan också se alla attribut i JSON-format genom att välja **[!UICONTROL View JSON]**.

![The [!UICONTROL View JSON] knappen markeras på informationssidan för den potentiella kundens profil.](../images/prospect-profile/profile-select-view-json.png)

The [!UICONTROL View JSON] visas. Attributen för den potentiella kundens profil visas nu i JSON-formulär.

![Profilens attribut för potentiell kund visas i JSON-formulär.](../images/prospect-profile/profile-view-json.png)

## Föreslagna användningsfall {#use-cases}

Om du vill veta hur du kan använda profilfunktionerna i Experience Platform i kombination med andra plattformsfunktioner läser du följande dokumentation om användningsfall:

- [Engagera och värva nya kunder med prospekteringsfunktionen](../../rtcdp/partner-data/prospecting.md)

## Nästa steg

När du har läst den här guiden får du nu veta hur profiler för potentiella kunder kan användas i Adobe Experience Platform. Läs mer om hur dessa profiler för potentiella kunder kan användas i [guide för potentiella målgrupper](../../segmentation/ui/prospect-audience.md).
