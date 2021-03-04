---
keywords: Experience Platform;home;IAB;IAB 2.0;medgivande;Samtycke
solution: Experience Platform
title: Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata
topic: sekretesshändelser
description: Det här dokumentet innehåller steg för hur du konfigurerar de två datauppsättningar som krävs för att samla in IAB TCF 2.0-medgivandedata.
translation-type: tm+mt
source-git-commit: a845ade0fc1e6e18c36b5f837fe7673a976f01c7
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---


# Skapa datauppsättningar för att hämta IAB TCF 2.0-medgivandedata

För att Adobe Experience Platform ska kunna behandla kundmedgivandedata i enlighet med IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, måste dessa data skickas till datauppsättningar vars scheman innehåller TCF 2.0-medgivandefält.

Två datauppsättningar krävs för att hämta TCF 2.0-medgivandedata:

* En datauppsättning som baseras på klassen [!DNL XDM Individual Profile], som är aktiverad för användning i [!DNL Real-time Customer Profile].
* En datauppsättning som baseras på klassen [!DNL XDM ExperienceEvent].

Det här dokumentet innehåller steg för hur du konfigurerar dessa två datauppsättningar för att samla in IAB TCF 2.0-medgivandedata. En översikt över det fullständiga arbetsflödet för att konfigurera plattformsdataåtgärder för TCF 2.0 finns i [IAB TCF 2.0-kompatibilitetsöversikt](./overview.md).

## Förutsättningar

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Gör att ni kan kombinera kundidentiteter från olika datakällor på olika enheter och system.
   * [Identitetsnamnutrymmen](../../../../identity-service/namespaces.md): Kundidentitetsdata måste anges under ett specifikt ID-namnområde som identifieras av identitetstjänsten.
* [Kundprofil](../../../../profile/home.md) i realtid: Tack vare  [!DNL Identity Service] detta kan ni skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från Data Lake och behåller kundprofiler i sitt eget separata datalager.

## [!UICONTROL Privacy Details] blandstruktur  {#structure}

[!UICONTROL Privacy Details]-mixinen innehåller tillståndsfält som krävs för TCF 2.0-stöd. Det finns två versioner av den här blandningen: en som är kompatibel med klassen [!DNL XDM Individual Profile] och den andra med klassen [!DNL XDM ExperienceEvent].

Avsnitten nedan förklarar strukturen för var och en av dessa blandningar, inklusive de data som förväntas vid intag.

### Profilblandning {#profile-mixin}

För scheman som baseras på [!DNL XDM Individual Profile] innehåller blandningen [!UICONTROL Privacy Details] ett enda mappningsfält, `xdm:identityPrivacyInfo`, som mappar kundidentiteter till deras TCF-medgivandeinställningar. Följande JSON är ett exempel på den typ av data som `xdm:identityPrivacyInfo` förväntar sig vid datainmatning:

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

Som exemplet visar motsvarar varje rotnivånyckel på `xdm:identityPrivacyInfo` ett identitetsnamnutrymme som identifieras av identitetstjänsten. Varje namespace-egenskap måste i sin tur ha minst en underegenskap vars nyckel matchar kundens motsvarande identitetsvärde för namnutrymmet. I det här exemplet identifieras kunden med ett Experience Cloud-ID (`ECID`)-värde på `13782522493631189`.

>[!NOTE]
>
>I exemplet ovan används ett namnutrymmes-/värdepar för att representera kundens identitet, men du kan lägga till ytterligare nycklar för andra namnutrymmen, och varje namnområde kan ha flera identitetsvärden, var och en med sin egen uppsättning inställningar för TCF-medgivande.

I identitetsvärdeobjektet finns ett enda fält, `xdm:identityIABConsent`. Det här objektet hämtar kundens TCF-medgivandevärden för det angivna identitetsnamnutrymmet och det angivna identitetsvärdet. Underegenskaperna i det här fältet visas nedan:

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:consentTimestamp` | En [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt)-tidsstämpel som anger när TCF-medgivandevärdena har ändrats. |
| `xdm:consentString` | Ett objekt som innehåller kundens uppdaterade godkännandedata och annan sammanhangsbaserad information. Mer information om objektets obligatoriska underegenskaper finns i avsnittet [egenskaper för medgivandesträng](#consent-string). |

### Händelseblandning i {#event-mixin}

För scheman som baseras på [!DNL XDM ExperienceEvent] ger blandningen [!UICONTROL Privacy Details] ett enskilt fält av arraytyp: `xdm:consentStrings`. Varje objekt i den här arrayen måste vara ett objekt som innehåller de nödvändiga egenskaperna för en TCF-medgivandesträng, som liknar fältet `xdm:consentString` i profilmixen. Mer information om dessa underegenskaper finns i [nästa avsnitt](#consent-string).

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### Egenskaper för godkännandesträng {#consent-string}

Båda versionerna av blandningen [!UICONTROL Privacy Details] kräver minst ett objekt som fångar de fält som behövs och som beskriver kundens TCF-medgivandesträng. Dessa egenskaper förklaras nedan:

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:consentStandard` | Samtyckesramverket som uppgifterna gäller för. För TCF-kompatibilitet måste värdet vara `IAB TCF`. |
| `xdm:consentStandardVersion` | Versionsnumret för medgivanderamverket som anges av `xdm:consentStandard`. För TCF 2.0-kompatibilitet måste värdet vara `2.0`. |
| `xdm:consentStringValue` | Medgivandesträngen som genererades av medgivandehanteringsplattformen (CMP) baserat på kundens valda inställningar. |
| `xdm:gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den här kunden eller inte. Värdet måste anges till `true` för att TCF 2.0 ska kunna användas. Standardvärdet är `true` om det inte ingår. |
| `xdm:containsPersonalData` | Ett booleskt värde som anger om medgivandeuppdateringen innehåller personuppgifter eller inte. Standardvärdet är `false` om det inte ingår. |

## Skapa kundmedgivandescheman {#create-schemas}

Om du vill skapa datauppsättningar som hämtar medgivandedata måste du först skapa XDM-scheman som baserar dessa datauppsättningar på.

I plattformsgränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen för att öppna arbetsytan [!UICONTROL Schemas]. Härifrån följer du stegen i avsnitten nedan för att skapa varje obligatoriskt schema.

>[!NOTE]
>
>Om du har befintliga XDM-scheman som du vill använda för att hämta medgivandedata i stället, kan du redigera dessa scheman i stället för att skapa nya. Men om ett befintligt schema har aktiverats för användning i kundprofilen i realtid, kan dess primära identitet inte vara ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, till exempel en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>När du redigerar befintliga scheman kan du dessutom bara göra additiva (fasta) ändringar. Mer information finns i avsnittet om [principerna för schemautveckling](../../../../xdm/schema/composition.md#evolution).

### Skapa ett postbaserat medgivandeschema {#profile-schema}

Välj **[!UICONTROL Create schema]** på arbetsytan **[!UICONTROL Schemas]** och välj sedan **[!UICONTROL XDM Individual Profile]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

[!DNL Schema Editor] visas och visar schemats struktur på arbetsytan. Använd den högra listen för att ange ett namn och en beskrivning av schemat och välj sedan **[!UICONTROL Add]** under **[!UICONTROL Mixins]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-profile.png)

Dialogrutan **[!UICONTROL Add mixin]** visas. Här väljer du **[!UICONTROL Privacy Details]** i listan. Du kan även använda sökfältet för att begränsa resultatet och enklare hitta mixen. Välj **[!UICONTROL Add mixin]** när du har valt mixen.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Arbetsytan visas igen och visar att fältet `identityPrivacyInfo` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Upprepa stegen ovan om du vill lägga till följande ytterligare blandningar i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Demographic Details]
* [!UICONTROL Personal Contact Details]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-mixins.png)

Om du redigerar ett befintligt schema som redan har aktiverats för användning i [!DNL Real-time Customer Profile] väljer du **[!UICONTROL Save]** för att bekräfta dina ändringar innan du går vidare till avsnittet [skapa en datauppsättning baserat på ditt medgivandeschema](#dataset). Om du skapar ett nytt schema fortsätter du med de steg som beskrivs i underavsnittet nedan.

#### Aktivera schemat för användning i [!DNL Real-time Customer Profile]

För att Platform ska kunna koppla de medgivandedata som den får till specifika kundprofiler måste medgivandeschemat aktiveras för användning i [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Exempelschemat som visas i det här avsnittet använder fältet `identityMap` som sin primära identitet. Om du vill ange ett annat fält som primär identitet måste du se till att du använder en indirekt identifierare, som ett cookie-ID, och inte ett direkt identifierbart fält som är förbjudet att använda i intressebaserad annonsering, som en e-postadress. Kontakta ditt juridiska ombud om du är osäker på vilka fält som är begränsade.
>
>Steg om hur du anger ett primärt identitetsfält för ett schema finns i [självstudiekursen för att skapa schema](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Om du vill aktivera schemat för [!DNL Profile] markerar du schemats namn i den vänstra listen för att öppna dialogrutan **[!UICONTROL Schema properties]** i den högra listen. Här väljer du alternativknappen **[!UICONTROL Profile]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

En pover visas, vilket anger att en primär identitet saknas. Markera kryssrutan för att använda en alternativ primär identitet, eftersom den primära identiteten kommer att finnas i fältet `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Slutligen väljer du **[!UICONTROL Save]** för att bekräfta ändringarna.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Skapa ett tidsseriebaserat medgivandeschema {#event-schema}

Välj **[!UICONTROL Create schema]** på arbetsytan **[!UICONTROL Schemas]** och välj sedan **[!UICONTROL XDM ExperienceEvent]** i listrutan.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

[!DNL Schema Editor] visas och visar schemats struktur på arbetsytan. Använd den högra listen för att ange ett namn och en beskrivning av schemat och välj sedan **[!UICONTROL Add]** under **[!UICONTROL Mixins]** till vänster på arbetsytan.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-event.png)

Dialogrutan **[!UICONTROL Add mixin]** visas. Här väljer du **[!UICONTROL Privacy Details]** i listan. Du kan även använda sökfältet för att begränsa resultatet och enklare hitta mixen. När du har valt en blandning väljer du **[!UICONTROL Add mixin]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Arbetsytan visas igen och visar att matrisen `consentStrings` har lagts till i schemastrukturen.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Upprepa stegen ovan om du vill lägga till följande ytterligare blandningar i schemat:

* [!UICONTROL IdentityMap]
* [!UICONTROL Environment Details]
* [!UICONTROL Web Details]
* [!UICONTROL Implementation Details]

När mixarna har lagts till slutför du genom att välja **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-mixins.png)

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

I den högra listen väljer du alternativet **[!UICONTROL Profile]** och sedan **[!UICONTROL Enable]** i bekräftelseporten för att aktivera schemat för [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Följ stegen ovan igen för att skapa den andra nödvändiga datauppsättningen för TCF 2.0-kompatibilitet.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat två datauppsättningar som nu kan användas för att samla in data om kundens samtycke:

* En postbaserad datauppsättning som är aktiverad för användning i kundprofilen i realtid.
* En tidsseriebaserad datauppsättning som inte är aktiverad för [!DNL Profile].

Du kan nu gå tillbaka till översikten [IAB TCF 2.0](./overview.md#merge-policies) om du vill fortsätta konfigurera plattformen för TCF 2.0-kompatibilitet.