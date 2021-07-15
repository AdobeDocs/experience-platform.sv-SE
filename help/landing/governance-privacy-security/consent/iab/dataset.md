---
keywords: Experience Platform;home;IAB;IAB 2.0;medgivande;Samtycke
solution: Experience Platform
title: Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata
topic-legacy: privacy events
description: Det här dokumentet innehåller steg för hur du konfigurerar de två datauppsättningar som krävs för att samla in IAB TCF 2.0-medgivandedata.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata

För att Adobe Experience Platform ska kunna behandla kundmedgivandedata i enlighet med IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, måste dessa data skickas till datauppsättningar vars scheman innehåller TCF 2.0-medgivandefält.

Två datauppsättningar krävs för att hämta TCF 2.0-medgivandedata:

* En datauppsättning som baseras på klassen [!DNL XDM Individual Profile], som är aktiverad för användning i [!DNL Real-time Customer Profile].
* En datauppsättning som baseras på klassen [!DNL XDM ExperienceEvent].

>[!IMPORTANT]
>
>Plattformen använder bara de TCF-strängar som samlats in i datauppsättningen för den enskilda profilen. En ExperienceEvent-datauppsättning krävs fortfarande för att skapa ett datastream som en del av det här arbetsflödet, men du behöver bara importera data till profildatauppsättningen. ExperienceEvent-datauppsättningen kan fortfarande användas om du vill spåra händelser om samtyckesändringar över tiden, men dessa värden används inte i när segmentaktivering används.

Det här dokumentet innehåller steg för hur du konfigurerar de här två datauppsättningarna. En översikt över det fullständiga arbetsflödet för att konfigurera plattformsdataåtgärder för TCF 2.0 finns i [IAB TCF 2.0-kompatibilitetsöversikt](./overview.md).

## Förutsättningar

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Gör att ni kan kombinera kundidentiteter från olika datakällor på olika enheter och system.
   * [Identitetsnamnutrymmen](../../../../identity-service/namespaces.md): Kundidentitetsdata måste anges under ett specifikt ID-namnområde som identifieras av identitetstjänsten.
* [Kundprofil](../../../../profile/home.md) i realtid: Tack vare  [!DNL Identity Service] detta kan ni skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från Data Lake och behåller kundprofiler i sitt eget separata datalager.

## TCF 2.0-fältgrupper {#field-groups}

Schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent] innehåller fält för kundgodkännande som krävs för TCF 2.0-stöd. Det finns två versioner av den här fältgruppen: en som är kompatibel med klassen [!DNL XDM Individual Profile] och den andra med klassen [!DNL XDM ExperienceEvent].

I avsnitten nedan förklaras strukturen för var och en av dessa fältgrupper, inklusive de data som förväntas vid intag.

### Profilfältgrupp {#profile-field-group}

För scheman som baseras på [!DNL XDM Individual Profile] innehåller fältgruppen [!UICONTROL IAB TCF 2.0 Consent] ett enda mappningsfält, `identityPrivacyInfo`, som mappar kundidentiteter till deras TCF-medgivandeinställningar. Den här fältgruppen måste inkluderas i ett postbaserat schema som är aktiverat för kundprofil i realtid för att automatisk tillämpning ska kunna utföras.

Se [referenshandboken](../../../../xdm/field-groups/profile/iab.md) för den här fältgruppen om du vill veta mer om dess struktur och hur den används.

### Fältgrupp för händelse {#event-field-group}

Om du vill spåra händelser för ändring av samtycke över tiden kan du lägga till fältgruppen [!UICONTROL IAB TCF 2.0 Consent] i ditt [!UICONTROL XDM ExperienceEvent]-schema.

Om du inte har för avsikt att spåra händelser för tillståndsändringar över tid, behöver du inte inkludera den här fältgruppen i ditt händelseschema. När TCF-medgivandevärden används automatiskt, använder Experience Platform endast den senaste medgivandeinformationen som är inskickad i [profilfältgruppen](#profile-field-group). Medgivandevärden som fångas av händelser deltar inte i automatiska arbetsflöden för verkställighet.

Se [referenshandboken](../../../../xdm/field-groups/event/iab.md) för den här fältgruppen för mer information om dess struktur och användningsfall.

## Skapa kundmedgivandescheman {#create-schemas}

För att kunna skapa datauppsättningar som samlar in medgivandedata måste du först skapa XDM-scheman som baserar dessa datauppsättningar på.

I plattformsgränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna arbetsytan [!UICONTROL Schemas]. Härifrån följer du stegen i avsnitten nedan för att skapa varje obligatoriskt schema.

>[!NOTE]
>
>Om du har befintliga XDM-scheman som du vill använda för att hämta medgivandedata i stället, kan du redigera dessa scheman i stället för att skapa nya. Men om ett befintligt schema har aktiverats för användning i kundprofilen i realtid, kan dess primära identitet inte vara ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, till exempel en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>När du redigerar befintliga scheman kan du dessutom bara göra additiva (fasta) ändringar. Mer information finns i avsnittet om [principerna för schemautveckling](../../../../xdm/schema/composition.md#evolution).

### Skapa ett schema för profilgodkännande {#profile-schema}

Välj **[!UICONTROL Create schema]** och välj sedan **[!UICONTROL XDM Individual Profile]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Dialogrutan **[!UICONTROL Add field groups]** visas så att du kan börja lägga till fältgrupper i schemat direkt. Här väljer du **[!UICONTROL IAB TCF 2.0 Consent]** i listan. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta fältgruppen. När fältgruppen är markerad väljer du **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Arbetsytan visas igen och visar att fältet `identityPrivacyInfo` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Innan du lägger till fler fält i schemat markerar du rotfältet så att **[!UICONTROL Schema properties]** visas i den högra listen, där du kan ange ett namn och en beskrivning för schemat.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

När du har angett ett namn och en beskrivning väljer du **[!UICONTROL Add]** under **[!UICONTROL Field groups]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Här kan du lägga till följande fältgrupper i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Demographic Details]
* [!UICONTROL Personal Contact Details]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

Om du redigerar ett befintligt schema som redan har aktiverats för användning i [!DNL Real-time Customer Profile] väljer du **[!UICONTROL Save]** för att bekräfta dina ändringar innan du går vidare till avsnittet [skapa en datauppsättning baserat på ditt medgivandeschema](#dataset). Om du skapar ett nytt schema fortsätter du med de steg som beskrivs i underavsnittet nedan.

#### Aktivera schemat för användning i [!DNL Real-time Customer Profile]

För att Platform ska kunna koppla de medgivandedata som den får till specifika kundprofiler måste medgivandeschemat aktiveras för användning i [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Exempelschemat som visas i det här avsnittet använder fältet `identityMap` som sin primära identitet. Om du vill ange ett annat fält som primär identitet måste du se till att du använder en indirekt identifierare, som ett cookie-ID, och inte ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, som en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>Steg om hur du anger ett primärt identitetsfält för ett schema finns i [självstudiekursen för att skapa schema](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Om du vill aktivera schemat för [!DNL Profile] markerar du schemats namn i den vänstra listen för att öppna avsnittet **[!UICONTROL Schema properties]**. Här väljer du alternativknappen **[!UICONTROL Profile]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

En pover visas, vilket anger att en primär identitet saknas. Markera kryssrutan för att använda en alternativ primär identitet, eftersom den primära identiteten kommer att finnas i fältet `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Slutligen väljer du **[!UICONTROL Save]** för att bekräfta ändringarna.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Skapa ett schema för godkännande av händelse {#event-schema}

Välj **[!UICONTROL Create schema]** på arbetsytan **[!UICONTROL Schemas]** och välj sedan **[!UICONTROL XDM ExperienceEvent]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Dialogrutan **[!UICONTROL Add field groups]** visas. Här väljer du **[!UICONTROL IAB TCF 2.0 Consent]** i listan. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta fältgruppen. När du har valt fältgruppen väljer du **[!UICONTROL Add field groups]**.

>[!NOTE]
>
>Det är bara nödvändigt att inkludera den här fältgruppen i ditt händelseschema om du planerar att spåra händelser om medgivandeändringar över tiden. Om du inte vill spåra dessa händelser kan du använda ett händelseschema utan dessa fält i stället när du konfigurerar Web SDK.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Arbetsytan visas igen och visar att fältet `consentStrings` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Innan du lägger till fler fält i schemat markerar du rotfältet så att **[!UICONTROL Schema properties]** visas i den högra listen, där du kan ange ett namn och en beskrivning för schemat.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

När du har angett ett namn och en beskrivning väljer du **[!UICONTROL Add]** under **[!UICONTROL Field groups]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Upprepa stegen ovan för att lägga till följande ytterligare fältgrupper i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL Environment Details]
* [!UICONTROL Web Details]
* [!UICONTROL Implementation Details]

När fältgrupperna har lagts till slutför du genom att välja **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Skapa datauppsättningar baserat på dina medgivandescheman {#datasets}

För vart och ett av de obligatoriska scheman som beskrivs ovan måste du skapa en datauppsättning som i slutändan kommer att innehålla kundernas medgivandedata. Datauppsättningen som baseras på postschemat måste aktiveras för [!DNL Real-time Customer Profile], medan datauppsättningen som baseras på tidsseriens schema **inte ska vara**-aktiverad.[!DNL Profile]

Börja med att välja **[!UICONTROL Datasets]** i den vänstra navigeringen och välj sedan **[!UICONTROL Create dataset]** i det övre högra hörnet.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

På nästa sida väljer du **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Arbetsflödet **[!UICONTROL Create dataset from schema]** visas med början i steget **[!UICONTROL Select schema]**. Leta reda på ett av de medgivandescheman som du skapade tidigare i listan. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta ditt schema. Markera alternativknappen bredvid önskat schema och välj sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

**[!UICONTROL Configure dataset]**-steget visas. Ange ett unikt, enkelt identifierbart namn och en beskrivning för datauppsättningen innan du väljer **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Informationssidan för den nya datauppsättningen visas. Om datauppsättningen baseras på ditt tidsserieschema är processen slutförd. Om datauppsättningen baseras på ditt postschema är det sista steget i processen att aktivera datauppsättningen för användning i [!DNL Real-time Customer Profile].

I den högra listen väljer du alternativet **[!UICONTROL Profile]** och sedan **[!UICONTROL Enable]** i bekräftelsepovern för att aktivera schemat för [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Följ stegen ovan igen för att skapa den andra nödvändiga datauppsättningen för TCF 2.0-kompatibilitet.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat två datauppsättningar som nu kan användas för att samla in data om kundens samtycke:

* En postbaserad datauppsättning som är aktiverad för användning i kundprofilen i realtid.
* En tidsseriebaserad datauppsättning som inte är aktiverad för [!DNL Profile].

Du kan nu gå tillbaka till översikten [IAB TCF 2.0](./overview.md#merge-policies) om du vill fortsätta konfigurera plattformen för TCF 2.0-kompatibilitet.
