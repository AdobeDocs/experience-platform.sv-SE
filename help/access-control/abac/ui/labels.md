---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Attributbaserad åtkomstkontroll Hantera etiketter
description: Det här dokumentet innehåller information om hur du hanterar etiketter via gränssnittet Behörigheter i Adobe Experience Cloud
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Hantera etiketter

>[!NOTE]
>
>Om du vill skapa eller visa beräknade attribut med fält som innehåller en viss etikett måste du ha tillgång till den etiketten.

Med etiketter kan du kategorisera datauppsättningar och fält utifrån de användnings- och åtkomstprinciper som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. De bästa sätten är att uppmuntra märkningsdata så snart de har importerats till Experience Platform, eller så snart data finns tillgängliga för användning i Experience Platform.

## Skapa en ny etikett {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Användning av etiketter"
>abstract="Du kan använda anpassade etiketter för att använda datastyrning och åtkomstkontrollskonfigurationer på dina data."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Skapa ny etikett"
>abstract="Du kan skapa egna etiketter som passar organisationens behov. Anpassade etiketter kan användas för att tillämpa både datastyrning och åtkomstkontrollskonfigurationer på dina data."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=sv-SE#manage-labels" text="Hantera anpassade etiketter"

>[!NOTE]
>
>Det finns en enda lista med etiketter för en hel organisation. Om du vill skapa en anpassad etikett måste du ha **[!UICONTROL Manage Usage Labels]** behörigheter i produktionssandlådan. Etikettborttagning stöds för närvarande inte.

Om du vill skapa en ny etikett väljer du fliken **[!UICONTROL Labels]** i sidofältet och väljer **[!UICONTROL Create Label]**.

![flac-new-label](../../images/flac-ui/create-label.png)

Dialogrutan **[!UICONTROL Create a new label]** visas och du uppmanas att ange ett namn, ett valfritt eget namn och en valfri beskrivning.

![new-label-info](../../images/flac-ui/new-label-info.png)

När du är klar väljer du **[!UICONTROL Confirm]**.
