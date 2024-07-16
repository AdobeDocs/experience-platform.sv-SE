---
title: Åtkomst till ECID
description: Lär dig hur du får åtkomst till Experience Cloud-ID från Data Prep eller Taggar
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Åtkomst till ECID

[!DNL Experience Cloud Identity (ECID)] är en beständig identifierare som tilldelas en användare när de besöker din webbplats. Under vissa omständigheter kanske du föredrar att komma åt [!DNL ECID] (till exempel för att skicka det till en tredje part). Ett annat användningsfall är att ange [!DNL ECID] i ett anpassat XDM-fält, förutom att det finns i identitetskartan.

Du kan komma åt ECID antingen via [Dataprep för datainsamling](../../../../datastreams/data-prep.md) (rekommenderas) eller via taggar.

## Åtkomst till ECID via Data Prep (föredragen metod) {#accessing-ecid-data-prep}

Om du vill ställa in ECID i ett anpassat XDM-fält kan du göra detta genom att ställa in `source` på följande sökväg, utöver att ha det i identitetskartan:

```js
xdm.identityMap.ECID[0].id
```

Ange sedan målet till en XDM-sökväg där fältet är av typen `string`.

![](./assets/access-ecid-data-prep.png)

## Taggar

Om du behöver komma åt [!DNL ECID] på klientsidan använder du taggarna enligt nedan.

1. Kontrollera att din egenskap är konfigurerad med [regelkomponentsekvensering](../../../ui/managing-resources/rules.md#sequencing) aktiverad.
1. Skapa en ny regel. Den här regeln ska endast användas för att hämta [!DNL ECID] utan några andra viktiga åtgärder.
1. Lägg till en [!UICONTROL Library Loaded]-händelse i regeln.
1. Lägg till en [!UICONTROL Custom Code]-åtgärd i regeln med följande kod (förutsatt att namnet som du har konfigurerat för SDK-instansen är `alloy` och att det inte redan finns ett dataelement med samma namn):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Spara regeln.

Du bör sedan kunna komma åt [!DNL ECID] i efterföljande regler med hjälp av `%ECID%` eller `_satellite.getVar("ECID")`, precis som du kan komma åt andra dataelement.
