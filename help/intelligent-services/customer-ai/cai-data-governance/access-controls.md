---
keywords: Experience Platform;användarhandbok;kundhandbok;populära ämnen;åtkomstkontroller;skapa modell;
solution: Experience Platform
feature: Customer AI
title: Åtkomstkontroll för kundens AI
description: Det här dokumentet innehåller information om attributbaserad åtkomstkontroll för kundens AI.
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Attributbaserad åtkomstkontroll

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll är för närvarande endast tillgänglig i en begränsad version.

[Attributbaserad åtkomstkontroll](../../../access-control/abac/overview.md) är en funktion i Adobe Experience Platform som gör det möjligt för administratörer att styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Med den här funktionen kan du etikettera XDM-schemafält (Experience Data Model) med etiketter som definierar användningsområde för organisationen eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper runt XDM-schemafält och bättre hantera åtkomsten som ges till användare eller grupper av användare (interna, externa eller externa användare). Dessutom gör attributbaserad åtkomstkontroll det möjligt för administratörer att hantera åtkomsten till specifika segment.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas tillgång till både känsliga personuppgifter (SPD) och personligt identifierbar information (PII) i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

På grund av den attributbaserade åtkomstkontrollen skulle vissa fält och funktioner ha begränsad åtkomst och vara otillgängliga för vissa AI-tjänstmodeller. Exempel: &quot;Identitet&quot;, &quot;Scores Definition&quot; och &quot;Clone&quot;.

![Kundens AI-arbetsyta med begränsade fält i servicemodellens resultat markerade.](../images/user-guide/unavailable-functionalities.png)

Överst på kundens AI-arbetsyta **insikter** Lägg märke till att informationen i sidofältet, poängdefinitionen, identiteten och profilattributen visar &quot;Åtkomst begränsad&quot;.

![Kundens AI-arbetsyta med de begränsade fälten i schemat markerade.](../images/user-guide/access-restricted.png)

När du förhandsgranskar datauppsättningar med begränsat schema på **[!UICONTROL Create model workflow]** visas en varning om att [!UICONTROL Due to access restrictions, certain information isn't displayed in the dataset preview.]

![Kundens AI-arbetsyta med begränsade fält för förhandsgranskningsdatauppsättningar med begränsade schemaresultat markerade.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

När du har skapat en modell med begränsad information och fortsätter till **[!UICONTROL Define goal]** visas en varning högst upp: [!UICONTROL Due to access restrictions, certain information isn't displayed in the configuration.]

![Kundens AI-arbetsyta med begränsade fält i servicemodellens resultat markerade.](../images/user-guide/information-not-displayed-save-and-exit.png)

När du använder åtkomstkontroll **Visa kund-AI** och **Hantera kund-AI** ger åtkomst till olika funktioner i Customer AI. The **Hantera kund-AI** behörighet ger dig **skapa**,**uppdatera**, **delete**, **enable**, eller **disable** en modell **Visa kund-AI** gör att du kan läsa eller visa den. The **skapa**, **uppdatera** och **delete** åtgärder registreras av granskningsloggar.

Läs dokumentationen för att lära dig mer [tilldela behörigheter för åtkomstkontroll](../../../help/access-control/home.md) eller hur [använda granskningsloggar för att övervaka åtkomst och aktivitet](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nästa steg

Genom att läsa den här guiden har du lagts till i huvudprinciperna för åtkomstkontroll i [!DNL Experience Platform]. Du kan nu fortsätta till [användarhandbok för åtkomstkontroll](./ui/overview.md) för detaljerade steg om hur du använder [!DNL Admin Console] för att skapa produktprofiler och tilldela behörigheter för [!DNL Platform].