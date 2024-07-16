---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;object;field;
solution: Experience Platform
title: Definiera objektfält i användargränssnittet
description: Lär dig hur du definierar ett objekttypsfält i användargränssnittet i Experience Platform.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Definiera objektfält i användargränssnittet

Med Adobe Experience Platform kan ni helt anpassa strukturen för era anpassade Experience Data Model-klasser (XDM), schemafältgrupper och datatyper. För att kunna ordna och kapsla relaterade fält i anpassade XDM-resurser kan du definiera objekttypsfält som kan innehålla ytterligare underfält.

När du [definierar ett nytt fält](./overview.md#define) i Adobe Experience Platform-användargränssnittet använder du listrutan **[!UICONTROL Type]** och väljer [!UICONTROL Object] i listan.

![](../../images/ui/fields/special/object.png)

Välj **[!UICONTROL Apply]** om du vill lägga till objektet i schemat. Arbetsytan uppdateras för att visa det nya fältet med datatypen [!UICONTROL Object], inklusive kontroller för att redigera och lägga till underfält till objektet.

![](../../images/ui/fields/special/object-applied.png)

Om du vill lägga till ett underfält markerar du ikonen **plus (+)** bredvid objektfältet på arbetsytan. Ett nytt fält visas under objektet, med kontroller för att konfigurera delfältet i den högra listen.

![](../../images/ui/fields/special/object-add-field.png)

När du har konfigurerat underfältet och markerat **[!UICONTROL Apply]** kan du fortsätta lägga till fält i objektet med samma process. Du kan också lägga till underfält som själva är objekt, så att du kan kapsla in fält så djupt du vill.

När du är klar med att skapa objektet kanske du vill återanvända dess struktur i olika klasser och fältgrupper. I det här fallet kan du välja att konvertera objektet till en datatyp. Mer information finns i avsnittet [Konvertera objekt till datatyper](../resources/data-types.md#convert) i användargränssnittsguiden för datatyper.

## Nästa steg

I den här handboken beskrivs hur du definierar ett objektfält i användargränssnittet. Mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor] finns i översikten [Definiera fält i användargränssnittet](./overview.md#special).
