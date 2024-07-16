---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;adobe admin admin console
solution: Experience Platform
feature: Attribution AI
title: Åtkomstkontroll för Attribution AI
description: Det här dokumentet innehåller information om attributbaserad åtkomstkontroll för Attribution AI.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Åtkomstkontroll i Attribution AI

Åtkomstkontroll för Attribution AI tillhandahålls via Adobe Experience Platform i [Adobe Admin Console](https://adminconsole.adobe.com/). Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.

Mer information om åtkomstkontroll finns i [åtkomstkontrollsöversikten](../../../access-control/home.md).

## Attributbaserad åtkomstkontroll

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll är för närvarande endast tillgänglig i en begränsad version.

[Attributbaserad åtkomstkontroll](../../../access-control/abac/overview.md) är en funktion i Adobe Experience Platform som gör att administratörer kan styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Med den här funktionen kan du etikettera XDM-schemafält (Experience Data Model) med etiketter som definierar användningsområde för organisationen eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper runt XDM-schemafält och bättre hantera åtkomsten som ges till användare eller grupper av användare (interna, externa eller externa användare). Dessutom gör attributbaserad åtkomstkontroll det möjligt för administratörer att hantera åtkomsten till specifika segment.

Genom attributbaserad åtkomstkontroll kan administratörer styra användarnas tillgång till både känsliga personuppgifter (SPD) och personligt identifierbar information (PII) i alla plattformsarbetsflöden och -resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

På grund av den attributbaserade åtkomstkontrollen kan vissa fält och funktioner ha begränsad åtkomst och vara otillgängliga för vissa Attribution AI-tjänstmodeller. Exempel: &quot;Identitet&quot;, &quot;Scores Definition&quot; och &quot;Clone&quot;.

Högst upp på arbetsytan **insikter** på Attribution AI har informationen som visas i sidofältet begränsad åtkomst.

![Arbetsytan i Attribution AI med begränsade schemafält markerade.](../images/user-guide/access-restricted.png)

Om du väljer datauppsättningar med begränsade scheman på sidan **[!UICONTROL Create model workflow]** visas ett varningsmeddelande bredvid datauppsättningsnamnet med meddelandet: [!UICONTROL Restricted information is excluded].

![Arbetsytan i Attribution AI med begränsade datamängdsfält markerade.](../images/user-guide/restricted-info-excluded.png)

När du förhandsgranskar datauppsättningar med begränsat schema på sidan **[!UICONTROL Create model workflow]** visas en varning om att [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![Arbetsytan i Attribution AI med resultaten av begränsade förhandsvisade schemafält markerade.](../images/user-guide/restricted-dataset-preview.png)

När du har skapat en modell med begränsad information och fortsätter till steget **[!UICONTROL Define goal]** visas en varning högst upp: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![Arbetsytan i Attribution AI med begränsade fält för modellresultaten markerade.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Nästa steg

Genom att läsa den här guiden har du lagts till i huvudprinciperna för åtkomstkontroll i [!DNL Experience Platform]. Du kan nu fortsätta till användarhandboken för [åtkomstkontrollen](../overview.md) för detaljerade steg om hur du använder [!DNL Admin Console] för att skapa produktprofiler och tilldela behörigheter för [!DNL Platform].
