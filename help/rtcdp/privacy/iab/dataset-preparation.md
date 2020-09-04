---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: Stöd för IAB TCF 2.0 i kunddataplattformen i realtid
topic: privacy events
description: Det här dokumentet innehåller steg för hur du konfigurerar de två datauppsättningar som krävs för att samla in IAB TCF 2.0-medgivandedata.
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 0%

---


# Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata

För [!DNL Real-time Customer Data Platform] att kunna behandla kundmedgivandedata i enlighet med IAB [!DNL Transparency & Consent Framework] (TCF) 2.0 måste dessa data skickas till datauppsättningar vars scheman innehåller TCF 2.0-tillståndsfält.

Två datauppsättningar krävs för att hämta TCF 2.0-medgivandedata:

* En datamängd som baseras på [!DNL XDM Individual Profile] klassen, som är aktiverad för användning i [!DNL Real-time Customer Profile].
* En datauppsättning som baseras på [!DNL XDM ExperienceEvent] klassen.

Det här dokumentet innehåller steg för hur du konfigurerar dessa två datauppsättningar för att samla in IAB TCF 2.0-medgivandedata. En översikt över det fullständiga arbetsflödet för att konfigurera [!DNL Real-time CDP] för TCF 2.0 finns i [IAB TCF 2.0-kompatibilitetsöversikt](./overview.md).

## Förutsättningar

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman.
   * [Skapa ett schema i användargränssnittet](../../../xdm/tutorials/create-schema-ui.md): En självstudiekurs som beskriver grunderna i att arbeta med Schemaredigeraren.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Gör att ni kan kombinera kundidentiteter från olika datakällor på olika enheter och system.
* [Kundprofil](../../../profile/home.md)i realtid: Tack vare [!DNL Identity Service] detta kan ni skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från Data Lake och behåller kundprofiler i sitt eget separata datalager.

## Schemastruktur för samtycke {#structure}

Det finns två XDM-mixiner som tillhandahåller medgivandefält som krävs för TCF 2.0-stöd: en för postbaserade data ([!DNL XDM Individual Profile]) och en annan för tidsseriebaserade data ([!DNL XDM ExperienceEvent]):

| Schema | Beskrivning |
| --- | --- |
| Blanda profiler | Den här mixinen fångar upp en kunds aktuella medgivandepreferenser. När de används i ett [!DNL Profile]aktiverat schema, används de värden som anges i den här mixinen som en källa till sanning för hur genomdrivandet av samtycke ska gälla för en kunds data. |
| [!DNL Experience Event] integritetsmixin | Den här mixinen fångar upp en kunds medgivandepreferenser vid en viss tidpunkt. De data som samlas in i dessa fält kan användas för att spåra ändringar i en kunds medgivandeinställningar över tid. |

Även om varje blandning används på olika sätt är de specifika fält som de tillhandahåller ungefär likadana. Dessa fält förklaras närmare i följande avsnitt.

### Samtyckesfält {#privacy-mixin}

Varje sekretessblandning varierar i struktur och de typer av fält som de innehåller, men båda innehåller attributet, vars underfält krävs för att TCF 2.0 ska kunna användas. `xdm:consentString` Strukturen för dessa fält visas nedan tillsammans med de typer av värden som de förväntar sig:

```json
{
  "xdm:consentString": {
    "xdm:consentStandard": "IAB TCF",
    "xdm:consentStandardVersion": "2.0",
    "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
    "xdm:gdprApplies": true,
    "xdm:containsPersonalData": false
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:consentString` | Innehåller kundens uppdaterade data för samtycke och annan sammanhangsbaserad information. |
| `xdm:consentStandard` | Samtyckesramverket som uppgifterna gäller för. För TCF-kompatibilitet ska värdet vara &quot;IAB TCF&quot;. |
| `xdm:consentStandardVersion` | Versionsnumret för medgivanderamverket som anges av `xdm:consentStandard`. För TCF 2.0-kompatibilitet ska värdet vara &quot;2.0&quot;. |
| `xdm:consentStringValue` | Den medgivandesträng som genererades baserat på kundens valda medgivandeinställningar. |
| `xdm:gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den här kunden eller inte. Värdet måste vara true för att TCF 2.0 ska kunna användas. Standardvärdet är &quot;false&quot; om det inte ingår. |
| `xdm:containsPersonalData` | Ett booleskt värde som anger om medgivandeuppdateringen innehåller personuppgifter eller inte. Standardvärdet är &quot;false&quot; om det inte ingår. |

## Skapa kundmedgivandescheman {#create-schemas}

Klicka i det vänstra navigeringsfältet **[!UICONTROL Schemas]** i Plattformsgränssnittet för att öppna *[!UICONTROL Schemas]arbetsytan*. Härifrån följer du stegen i avsnitten nedan för att skapa varje obligatoriskt schema.

>[!NOTE]
>
>Om du har befintliga XDM-scheman som du vill använda för att hämta medgivandedata i stället, kan du redigera dessa scheman i stället för att skapa nya. När du redigerar befintliga scheman är det dock viktigt att följa [principerna för schemautveckling](../../../xdm/schema/composition.md#evolution) för att undvika att ändringarna bryts.

### Skapa ett postbaserat medgivandeschema {#profile-schema}

Skapa ett nytt schema baserat på **[!UICONTROL Browse]** klassen **[!UICONTROL Schemas]från fliken på** arbetsytan **[!DNL XDM Individual Profile]**. När du har öppnat schemat i Schemaredigeraren klickar du **[!UICONTROL Add]** under **[!UICONTROL Mixins]** avsnittet till vänster på arbetsytan.

![](../assets/iab/add-mixin-profile.png)

Dialogrutan **[!UICONTROL Add mixin]** visas. Välj **[!UICONTROL Profile privacy]** från listan. Du kan även använda sökfältet för att begränsa resultatet och enklare hitta mixen. När du har valt mixen klickar du på **[!UICONTROL Add mixin]**.

![](../assets/iab/add-profile-privacy.png)

Arbetsytan i Schemaredigeraren visas igen, så att du kan granska strukturen för de tillagda medgivandesträngfälten.

![](../assets/iab/profile-privacy-structure.png)

Upprepa stegen ovan om du vill lägga till följande ytterligare blandningar i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Profile person details]
* [!UICONTROL Profile personal details]

![](../assets/iab/profile-all-mixins.png)

Om du redigerar ett befintligt schema som redan har aktiverats för användning i [!DNL Real-time Customer Profile], klickar du på **[!UICONTROL Save]** för att bekräfta ändringarna innan du går vidare till avsnittet om [att skapa en datauppsättning baserat på ditt medgivandeschema](#dataset). Om du skapar ett nytt schema fortsätter du med de steg som beskrivs i underavsnittet nedan.

#### Aktivera schemat för användning i [!DNL Real-time Customer Profile]

För [!DNL Real-time CDP] att kunna koppla de medgivandedata de får till specifika kundprofiler måste medgivandeschemat aktiveras för användning i [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Exempelschemat som visas i det här avsnittet använder sitt `identityMap` fält som primär identitet. Om du vill ange ett annat fält som primär identitet måste du se till att du använder en indirekt identifierare, som ett cookie-ID, och inte ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, som en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>Steg om hur du anger ett primärt identitetsfält för ett schema finns i självstudiekursen [för att skapa](../../../xdm/tutorials/create-schema-ui.md#identity-field)schema.

Om du vill aktivera schemat för [!DNL Profile]klickar du på schemats namn i den vänstra listen för att öppna **[!UICONTROL Schema properties]** dialogrutan i den högra listen. Klicka på **[!UICONTROL Profile]** växlingsknappen härifrån.

![](../assets/iab/profile-enable-profile.png)

En pover visas, vilket anger att en primär identitet saknas. Markera kryssrutan för att använda en alternativ primär identitet, eftersom den primära identiteten kommer att finnas i fältet identityMap.

<img src="../assets/iab/missing-primary-identity.png" width="600" /><br>

Klicka slutligen på **[!UICONTROL Save]** för att bekräfta ändringarna.

![](../assets/iab/profile-save.png)

### Skapa ett tidsseriebaserat medgivandeschema {#event-schema}

Skapa ett nytt schema baserat på **[!UICONTROL Browse]** klassen **[!UICONTROL Schemas]från fliken på** arbetsytan **[!DNL XDM ExperienceEvent]**. När du har öppnat schemat i Schemaredigeraren klickar du **[!UICONTROL Add]** under **[!UICONTROL Mixins]** avsnittet till vänster på arbetsytan.

![](../assets/iab/add-mixin-event.png)

Dialogrutan **[!UICONTROL Add mixin]** visas. Välj **[!UICONTROL Experience event privacy mixin]** från listan. Du kan även använda sökfältet för att begränsa resultatet och enklare hitta mixen. När du har valt mixen klickar du på **[!UICONTROL Add mixin]**.

![](../assets/iab/add-event-privacy.png)

Arbetsytan i Schemaredigeraren visas igen och de tillagda medgivandesträngsfälten visas.

![](../assets/iab/event-privacy-structure.png)

Upprepa stegen ovan om du vill lägga till följande ytterligare blandningar i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL ExperienceEvent environment details]
* [!UICONTROL ExperienceEvent web details]
* [!UICONTROL ExperienceEvent implementation details]

När du har lagt till mixarna avslutar du genom att klicka **[!UICONTROL Save]**.

![](../assets/iab/event-all-mixins.png)

## Skapa datauppsättningar baserat på dina medgivandescheman {#datasets}

För vart och ett av de obligatoriska scheman som beskrivs ovan måste du skapa en datauppsättning som i slutändan kommer att innehålla kundernas samtycke. Datauppsättningen som baseras på [!DNL XDM Individual Profile] schemat måste aktiveras för [!DNL Real-time Customer Profile], medan datauppsättningen som baseras på [!DNL XDM ExperienceEvent] schemat inte ska [!DNL Profile]aktiveras.

Börja med att markera **[!UICONTROL Datasets]** i den vänstra navigeringen och klicka sedan **[!UICONTROL Create dataset]** i det övre högra hörnet.

![](../assets/iab/dataset-create.png)

På nästa sida väljer du **[!UICONTROL Create dataset from schema]**.

![](../assets/iab/dataset-create-from-schema.png)

Arbetsflödet **[!UICONTROL Create dataset from schema]** visas med början i **[!UICONTROL Select schema]** steget. Leta reda på ett av de medgivandescheman som du skapade tidigare i listan. Du kan även använda sökfunktionen för att begränsa resultaten och enklare hitta ditt schema. Klicka på alternativknappen bredvid schemat för att markera det och klicka sedan på **[!UICONTROL Next]** för att fortsätta.

![](../assets/iab/dataset-select-schema.png)

Steget **[!UICONTROL Configure dataset]** visas. Ange ett unikt, enkelt identifierbart namn och en beskrivning för datauppsättningen innan du klickar på **[!UICONTROL Finish]**.

![](../assets/iab/dataset-configure.png)

Informationssidan för den nya datauppsättningen visas. Om datauppsättningen baseras på ditt [!DNL XDM ExperienceEvent] schema är processen slutförd. Om datauppsättningen baseras på ditt [!DNL XDM Individual Profile] schema är det sista steget i processen att aktivera datauppsättningen för användning i [!DNL Real-time Customer Profile]. Klicka på växlingsknappen till höger om du vill aktivera datauppsättningen. **[!UICONTROL Profile]**

![](../assets/iab/dataset-enable-profile.png)

Följ stegen ovan igen för att skapa den andra nödvändiga datauppsättningen för TCF 2.0-kompatibilitet.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat två datauppsättningar som nu kan användas för att samla in data om kundens samtycke:

* En [!DNL Profile]aktiverad datauppsättning baserad på ditt [!DNL XDM Individual Profile] schema.
* En datauppsättning baserad på ditt [!DNL XDM ExperienceEvent] schema som inte är aktiverat för [!DNL Profile].

Du kan nu gå tillbaka till [IAB TCF 2.0-översikten](./overview.md#merge-policies) för att fortsätta konfigurera [!DNL Real-time CDP] för TCF 2.0-kompatibilitet.