---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control
title: Attributbaserad åtkomstkontroll Hantera etiketter
description: Hantera etiketter via gränssnittet Behörigheter i Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# Hantera etiketter

Du kan använda etiketter för att kategorisera datauppsättningar och fält utifrån dataanvändning och attributbaserade åtkomstkontrollprinciper. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. De bästa sätten är att uppmuntra märkningsdata så snart de har importerats till Adobe Experience Platform, eller så snart data blir tillgängliga för användning. Läs det här dokumentet för att lära dig hur du kan hantera etiketter i gränssnittet Behörigheter.

En omfattande lista över etiketter och deras motsvarande styrningsprinciper finns i guiden om [etiketter för kärndataanvändning](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Om du vill skapa eller visa [beräknade attribut](../../../profile/computed-attributes/overview.md){target="_blank"} med fält som innehåller en viss etikett måste du ha tillgång till den etiketten.

## Utforska etiketter {#explore-labels}

Om du vill visa alla tillgängliga etiketter går du till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Välj **[!UICONTROL Labels]** i den vänstra panelen.

![Arbetsytan Etiketter i Behörigheter med etiketter är markerad i den vänstra panelen.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Etiketter kategoriseras efter typ och tillhör en av följande kategorier:

| Typ | Beskrivning |
| --- | --- |
| [Kontrakt](../../../data-governance/labels/reference.md#contract){target="_blank"} | Den här kategorin används för att kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till organisationens policyer för datastyrning. |
| [Identitet](../../../data-governance/labels/reference.md#identity){target="_blank"} | Den här kategorin används för att kategorisera data som direkt eller indirekt kan identifiera en person. |
| [Känslig](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Den här kategorin används för att kategorisera data som din organisation anser vara känsliga. |
| [Partnerekosystem](../../../data-governance/labels/reference.md#partner){target="_blank"} | Den här kategorin används för att kategorisera data som hämtats från externa källor för din organisation. |
| Ansvarigt engagemang | Den här kategorin innehåller en enda etikett, **[!UICONTROL Potential for Bias]**, som reflekterar data som kan ge upphov till fördomar. |
| Egen | Den här kategorin innehåller etiketter som har skapats av din organisation. |

Om du vill filtrera etiketter markerar du filterikonen (![filterikonen](/help/images/icons/filter.png)) och väljer önskad etiketttyp i listrutan **[!UICONTROL Type]** .

![Arbetsytan Etiketter med filteralternativet utökat och listrutan med text markerad.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Om du vill visa en enskild etikett markerar du etikettens namn i listan. Etikettens detaljsida visas. Adobe kärnetiketter kan **inte** redigeras.

![Detaljsida för en enskild etikett.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Skapa en egen etikett {#create-custom-label}

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
>Om du vill skapa en anpassad etikett måste du ha en roll som innehåller behörigheterna **[!UICONTROL Manage Usage Labels]** och sandlådan `Prod`.

Om du vill skapa en ny etikett väljer du **[!UICONTROL Labels]** på den vänstra panelen på arbetsytan i **[!UICONTROL Permissions]** och sedan **[!UICONTROL Create label]**.

![Arbetsytan Etiketter med alternativet Skapa etikett markerat.](../../images/ui/labels/create-label.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Create new label]** visas och du uppmanas att ange **[!UICONTROL Name]**, **[!UICONTROL Friendly name]** och **[!UICONTROL Description]**.

>[!IMPORTANT]
>
> Etikettens [!UICONTROL Name] kan inte ändras efter att etiketten har skapats och det går inte att ta bort etiketter för tillfället.

Välj **[!UICONTROL Confirm]** för att slutföra skapandet av etiketten.

![Dialogrutan Skapa ny etikett med namnet, det egna namnet och beskrivningen ifyllda och alternativet Bekräfta markerat.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Redigera en egen etikett {#edit-custom-label}

Du kan inte redigera **[!UICONTROL Name]** för en anpassad etikett, men du kan redigera **[!UICONTROL Friendly name]** och **[!UICONTROL Description]**. Om du vill redigera en anpassad etikett väljer du den i listan på arbetsytan **[!UICONTROL Labels]**.

![Arbetsytan Etiketter med etiketten markerad.](../../images/ui/labels/select-label.png){zoomable="yes"}

Redigera något av fälten och klicka sedan var som helst utanför textrutan för att spara ändringarna. Ett bekräftelsemeddelande visas på skärmen och **[!UICONTROL Modified by]**-namnet och **[!UICONTROL Modified]**-datumet ändras.

![Etikettens detaljsida med ett meddelande om att det har uppdaterats visas.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Nästa steg

Nu när du har en djupare förståelse för etiketter kan du börja [använda dem i scheman](../../../xdm/tutorials/labels.md).
