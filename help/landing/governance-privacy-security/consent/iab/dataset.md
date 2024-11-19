---
keywords: Experience Platform;home;IAB;IAB 2.0;medgivande;Samtycke
solution: Experience Platform
title: Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata
description: Det här dokumentet innehåller steg för hur du konfigurerar de två datauppsättningar som krävs för att samla in IAB TCF 2.0-medgivandedata.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata

För att Adobe Experience Platform ska kunna behandla kundmedgivandedata i enlighet med IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, måste dessa data skickas till datauppsättningar vars scheman innehåller TCF 2.0-tillståndsfält.

Två datauppsättningar krävs för att hämta TCF 2.0-medgivandedata:

* En datauppsättning som baseras på klassen [!DNL XDM Individual Profile] och som har aktiverats för användning i [!DNL Real-Time Customer Profile].
* En datauppsättning baserad på klassen [!DNL XDM ExperienceEvent].

>[!IMPORTANT]
>
>Plattformen använder bara de TCF-strängar som samlats in i datauppsättningen för den enskilda profilen. En ExperienceEvent-datauppsättning krävs fortfarande för att skapa ett datastream som en del av det här arbetsflödet, men du behöver bara importera data till profildatauppsättningen. ExperienceEvent-datauppsättningen kan fortfarande användas om du vill spåra händelser om samtyckesändringar över tiden, men dessa värden används inte i när segmentaktivering används.

Det här dokumentet innehåller steg för hur du konfigurerar de här två datauppsättningarna. En översikt över det fullständiga arbetsflödet för att konfigurera plattformsdataåtgärder för TCF 2.0 finns i [IAB TCF 2.0-kompatibilitetsöversikt](./overview.md).

## Förhandskrav

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grunderna i schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om grundläggande byggstenar i XDM-scheman.
* [Adobe Experience Platform identitetstjänst](../../../../identity-service/home.md): Gör att du kan kombinera kundidentiteter från olika datakällor på olika enheter och system.
   * [Identitetsnamnområden](../../../../identity-service/features/namespaces.md): Kundidentitetsdata måste anges under ett specifikt ID-namnområde som känns igen av identitetstjänsten.
* [Kundprofil i realtid](../../../../profile/home.md): utnyttjar [!DNL Identity Service] för att du ska kunna skapa detaljerade kundprofiler utifrån dina datauppsättningar i realtid. [!DNL Real-Time Customer Profile] hämtar data från datasjön och behåller kundprofiler i sitt eget separata datalager.

## TCF 2.0-fältgrupper {#field-groups}

Schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent Details] innehåller fält för kundgodkännande som krävs för TCF 2.0-stöd. Det finns två versioner av den här fältgruppen: en som är kompatibel med klassen [!DNL XDM Individual Profile] och den andra med klassen [!DNL XDM ExperienceEvent].

I avsnitten nedan förklaras strukturen för var och en av dessa fältgrupper, inklusive de data som förväntas vid intag.

### Profilfältgrupp {#profile-field-group}

För scheman baserade på [!DNL XDM Individual Profile] innehåller fältgruppen [!UICONTROL IAB TCF 2.0 Consent Details] ett enda mappningsfält, `identityPrivacyInfo`, som mappar kundidentiteter till deras TCF-medgivandeinställningar. Den här fältgruppen måste inkluderas i ett postbaserat schema som är aktiverat för kundprofil i realtid för att automatisk tillämpning ska kunna utföras.

Se [referenshandboken](../../../../xdm/field-groups/profile/iab.md) för den här fältgruppen om du vill veta mer om dess struktur och användningsfall.

### Fältgrupp för händelse {#event-field-group}

Om du vill spåra händelser för ändring av samtycke över tiden kan du lägga till fältgruppen [!UICONTROL IAB TCF 2.0 Consent Details] i ditt [!UICONTROL XDM ExperienceEvent]-schema.

Om du inte har för avsikt att spåra händelser för tillståndsändringar över tid, behöver du inte inkludera den här fältgruppen i ditt händelseschema. När TCF-medgivandevärden används automatiskt, använder Experience Platform endast den senaste medgivandeinformationen som har angetts i [profilfältgruppen](#profile-field-group). Medgivandevärden som fångas av händelser deltar inte i automatiska arbetsflöden för verkställighet.

Se [referenshandboken](../../../../xdm/field-groups/event/iab.md) för den här fältgruppen för mer information om dess struktur och användningsfall.

## Skapa kundmedgivandescheman {#create-schemas}

För att kunna skapa datauppsättningar som samlar in medgivandedata måste du först skapa XDM-scheman som baserar dessa datauppsättningar på.

Som nämndes i föregående avsnitt krävs ett schema som använder klassen [!UICONTROL XDM Individual Profile] för att framtvinga samtycke i arbetsflöden för efterföljande plattformar. Du kan också skapa ett separat schema baserat på [!UICONTROL XDM ExperienceEvent] om du vill spåra medgivandeändringar över tiden. Båda scheman måste innehålla ett `identityMap`-fält och en lämplig TCF 2.0-fältgrupp.

I plattformsgränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna arbetsytan i [!UICONTROL Schemas]. Härifrån följer du stegen i avsnitten nedan för att skapa varje obligatoriskt schema.

>[!NOTE]
>
>Om du har befintliga XDM-scheman som du vill använda för att hämta medgivandedata i stället, kan du redigera dessa scheman i stället för att skapa nya. Men om ett befintligt schema har aktiverats för användning i kundprofilen i realtid, kan dess primära identitet inte vara ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, till exempel en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>När du redigerar befintliga scheman kan du dessutom bara göra additiva (fasta) ändringar. Mer information finns i avsnittet [Principer för schemautveckling](../../../../xdm/schema/composition.md#evolution).

### Skapa ett schema för profilgodkännande {#profile-schema}

Välj **[!UICONTROL Create schema]** och välj sedan **[!UICONTROL XDM Individual Profile]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Dialogrutan **[!UICONTROL Add field groups]** visas så att du kan börja lägga till fältgrupper i schemat direkt. Välj **[!UICONTROL IAB TCF 2.0 Consent Details]** i listan härifrån. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta fältgruppen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Leta sedan reda på fältgruppen **[!UICONTROL IdentityMap]** i listan och markera den också. Välj **[!UICONTROL Add field groups]** när båda fältgrupperna är listade i den högra listen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

Arbetsytan visas igen och visar att fälten `identityPrivacyInfo` och `identityMap` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Innan du lägger till fler fält i schemat markerar du rotfältet så att **[!UICONTROL Schema properties]** visas i den högra listen, där du kan ange ett namn och en beskrivning för schemat.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

När du har angett ett namn och en beskrivning kan du lägga till fler fält i schemat genom att välja **[!UICONTROL Add]** under avsnittet **[!UICONTROL Field groups]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Om du redigerar ett befintligt schema som redan har aktiverats för användning i [!DNL Real-Time Customer Profile] väljer du **[!UICONTROL Save]** för att bekräfta dina ändringar innan du går vidare till avsnittet [skapa en datauppsättning baserat på ditt medgivandeschema](#dataset). Om du skapar ett nytt schema fortsätter du med de steg som beskrivs i underavsnittet nedan.

#### Aktivera schemat för användning i [!DNL Real-Time Customer Profile]

För att Platform ska kunna associera de medgivandedata som den får till specifika kundprofiler måste medgivandeschemat aktiveras för användning i [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>Exempelschemat som visas i det här avsnittet använder fältet `identityMap` som sin primära identitet. Om du vill ange ett annat fält som primär identitet måste du se till att du använder en indirekt identifierare, som ett cookie-ID, och inte ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, som en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>Steg om hur du anger ett primärt identitetsfält för ett schema finns i [[!UICONTROL Schemas] gränssnittshandboken ](../../../../xdm/ui/fields/identity.md).

Om du vill aktivera schemat för [!DNL Profile] markerar du schemats namn i den vänstra listen för att öppna avsnittet **[!UICONTROL Schema properties]**. Välj växlingsknappen **[!UICONTROL Profile]** härifrån.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

En pover visas, vilket anger att en primär identitet saknas. Markera kryssrutan för att använda en alternativ primär identitet, eftersom den primära identiteten kommer att finnas i fältet `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Slutligen väljer du **[!UICONTROL Save]** för att bekräfta dina ändringar.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Skapa ett schema för godkännande av händelse {#event-schema}

>[!NOTE]
>
>Scheman för godkännande av händelser används bara för att spåra händelser om godkännande över tiden, och deltar inte i arbetsflöden för tillsyn längre fram. Om du inte vill spåra ändringar av ditt samtycke över tiden kan du gå vidare till nästa avsnitt om att [skapa medgivandedatauppsättningar](#datasets).

Välj **[!UICONTROL Create schema]** på arbetsytan **[!UICONTROL Schemas]** och välj sedan **[!UICONTROL XDM ExperienceEvent]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Dialogrutan **[!UICONTROL Add field groups]** visas. Välj **[!UICONTROL IAB TCF 2.0 Consent Details]** i listan härifrån. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta fältgruppen.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Leta sedan reda på fältgruppen **[!UICONTROL IdentityMap]** i listan och markera den också. Välj **[!UICONTROL Add field groups]** när båda fältgrupperna är listade i den högra listen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

Arbetsytan visas igen och visar att fälten `consentStrings` och `identityMap` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Innan du lägger till fler fält i schemat markerar du rotfältet så att **[!UICONTROL Schema properties]** visas i den högra listen, där du kan ange ett namn och en beskrivning för schemat.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

När du har angett ett namn och en beskrivning kan du lägga till fler fält i schemat genom att välja **[!UICONTROL Add]** under avsnittet **[!UICONTROL Field groups]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

När fältgrupperna som du vill använda har lagts till avslutar du med att välja **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Skapa datauppsättningar baserat på dina medgivandescheman {#datasets}

För vart och ett av de obligatoriska scheman som beskrivs ovan måste du skapa en datauppsättning som i slutändan kommer att innehålla kundernas medgivandedata. Datauppsättningen som baseras på postschemat måste aktiveras för [!DNL Real-Time Customer Profile], medan datauppsättningen som baseras på tidsserieschemat **inte** ska vara [!DNL Profile]-aktiverad.

Börja med att välja **[!UICONTROL Datasets]** i den vänstra navigeringen och sedan **[!UICONTROL Create dataset]** i det övre högra hörnet.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Välj **[!UICONTROL Create dataset from schema]** på nästa sida.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Arbetsflödet **[!UICONTROL Create dataset from schema]** visas med början i steget **[!UICONTROL Select schema]**. Leta reda på ett av de medgivandescheman som du skapade tidigare i listan. Du kan även använda sökfältet för att begränsa resultaten och enklare hitta ditt schema. Markera alternativknappen bredvid önskat schema och välj sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

**[!UICONTROL Configure dataset]**-steget visas. Ange ett unikt, enkelt identifierbart namn och en beskrivning för datauppsättningen innan du väljer **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Informationssidan för den nya datauppsättningen visas. Om datauppsättningen baseras på ditt tidsserieschema är processen slutförd. Om datauppsättningen baseras på ditt postschema är det sista steget i processen att aktivera datauppsättningen för användning i [!DNL Real-Time Customer Profile].

Markera växlingsknappen **[!UICONTROL Profile]** i den högra listen och välj sedan **[!UICONTROL Enable]** i bekräftelseporten för att aktivera schemat för [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Följ stegen ovan igen för att skapa en händelsebaserad datauppsättning om du skapade ett schema för den.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat minst en datauppsättning som nu kan användas för att samla in data om kundens samtycke:

* En postbaserad datauppsättning som är aktiverad för användning i kundprofilen i realtid. **(Obligatoriskt)**
* En tidsseriebaserad datauppsättning som inte har aktiverats för [!DNL Profile]. (Valfritt)

Du kan nu gå tillbaka till översikten [IAB TCF 2.0](./overview.md#merge-policies) för att fortsätta konfigurera plattformen för TCF 2.0-kompatibilitet.
