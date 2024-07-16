---
title: Prospekt
description: Lär dig hur du skapar och använder profiler för potentiella kunder för att samla in information om okända kunder med hjälp av tredjepartsinformation.
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Prospekteringsprofiler

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke.

Prospektprofiler används för att representera personer som ännu inte har interagerat med ditt företag men som du vill kontakta. Med profiler för potentiella kunder kan ni komplettera era kundprofiler med attribut från betrodda tredjepartspartners.

## Bläddra {#browse}

Om du vill komma åt profiler för potentiella kunder väljer du **[!UICONTROL Profiles]** i avsnittet **[!UICONTROL Prospects]**.

Sidan **[!UICONTROL Browse]** visas. En lista över alla profiler för potentiella kunder för din organisation visas.

![Knappen [!UICONTROL Profiles] är markerad och visar sidan [!UICONTROL Browse] för profiler för potentiella kunder.](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>Även om de flesta av webbläsarfunktionerna mellan kundprofiler och profiler för potentiella kunder är desamma, kan du **inte** bläddra bland profiler för potentiella kunder genom en sammanslagningsprincip. Detta beror på att profiler för potentiella kunder automatiskt styrs av en systemdesignad, tidsbaserad sammanslagningsprincip. Mer information om sammanfogningsprinciper finns i översikten för [sammanfogningsprincipen](../merge-policies/overview.md).

Mer information om att bläddra bland profiler finns i [bläddringsavsnittet i användarhandboken för profilen](./user-guide.md#browse-identity).

## Information om potentiell profil {#profile-details}

>[!IMPORTANT]
>
>En profil för potentiell kund upphör automatiskt att gälla efter 25 dagars vistelse i Adobe Experience Platform.

Om du vill visa mer information om en viss profil för potentiell kund väljer du en profil på sidan [!UICONTROL Browse].

![En profil för potentiell kund har markerats på bläddringssidan.](../images/prospect-profile/select-specific-profile.png)

Information om den potentiella kundens profil visas, inklusive de attribut som är kopplade till profilen och målgruppsmedlemskapet.

![Informationssidan för den potentiella kundens profil visas.](../images/prospect-profile/profile-details.png)

Mer information om de här flikarna finns i avsnittet [Visa profilinformation i användarhandboken för profilen](./user-guide.md#profile-detail).

Du kan också se alla attribut i JSON-format genom att välja **[!UICONTROL View JSON]**.

![Knappen [!UICONTROL View JSON] är markerad på informationssidan för den potentiella kundens profil.](../images/prospect-profile/profile-select-view-json.png)

Dialogrutan [!UICONTROL View JSON] visas. Attributen för den potentiella kundens profil visas nu i JSON-formulär.

![Den potentiella kundens profilattribut visas i JSON-format.](../images/prospect-profile/profile-view-json.png)

## Föreslagna användningsfall {#use-cases}

Om du vill veta hur du kan använda profilfunktionerna i Experience Platform i kombination med andra plattformsfunktioner läser du följande dokumentation om användningsfall:

- [Engagera och värva nya kunder med prospekteringsfunktionen](../../rtcdp/partner-data/prospecting.md)

## Nästa steg

När du har läst den här guiden får du nu veta hur profiler för potentiella kunder kan användas i Adobe Experience Platform. Om du vill veta hur dessa profiler för potentiella kunder kan användas i målgrupper kan du läsa [guiden för potentiella målgrupper](../../segmentation/ui/prospect-audience.md).
