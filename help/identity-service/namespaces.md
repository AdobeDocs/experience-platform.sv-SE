---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: 'Identitetsnamnutrymmen är en komponent i identitetstjänsten som fungerar som indikatorer för det sammanhang som en identitet relateras till. De skiljer till exempel på värdet"name@email.com" som e-postadress eller"443522" som ett numeriskt CRM-ID. '
translation-type: tm+mt
source-git-commit: 0547c33e831fe1ac684f55a0e79978cd7f191e65
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 1%

---


# Översikt över namnområde för identitet

Identitetsnamnutrymmen är en komponent i [[!DNL Identity Service]](./home.md) som fungerar som indikatorer för det sammanhang som en identitet relateras till. De skiljer till exempel på värdet&quot;name<span>@email.com&quot; som e-postadress eller&quot;443522&quot; som ett numeriskt CRM-ID.

## Komma igång

Att arbeta med identitetsnamnutrymmen kräver förståelse för de olika Adobe Experience Platform-tjänsterna. Innan du börjar arbeta med namnutrymmen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Identity Service]](./home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
- [[!DNL Privacy Service]](../privacy-service/home.md): Identitetsnamnutrymmen används för att uppfylla den allmänna dataskyddsförordningen (GDPR), där GDPR-begäranden kan göras i förhållande till ett namnutrymme.

## Identitetsnamnutrymmen

En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. När postdata matchas mellan profilfragment, som när [!DNL Real-time Customer Profile] sammanfogar profildata, måste både identitetsvärdet och namnutrymmet matcha.

Två profilfragment kan t.ex. innehålla olika primära ID:n, men de delar samma värde för namnutrymmet&quot;E-post&quot;. [!DNL Platform] kan därför se att dessa fragment faktiskt är samma individ och sammanför data i identitetsdiagrammet för den enskilda personen.

![](images/identity-service-stitching.png)

### Identitetstyper

Data kan identifieras av flera olika identitetstyper. Identitetstypen anges när identitetsnamnutrymmet skapas och kontrollerar om data bevaras i identitetsdiagrammet och eventuella specialinstruktioner för hur data ska hanteras.

Följande identitetstyper är tillgängliga i [!DNL Platform]:

| Identitetstyp | Beskrivning |
| --- | --- |
| Cookie-ID | Cookie-ID:n identifierar webbläsare. Dessa identiteter är viktiga för expansion och utgör huvuddelen av identitetsdiagrammet. Av naturen sjunker de dock snabbt och förlorar sitt värde över tiden. |
| Enhets-ID | Enhetsoberoende ID:n identifierar en individ och knyter vanligtvis samman andra ID:n. Exempel är inloggnings-ID, CRM-ID och lojalitets-ID. Detta är en indikation på att [!DNL Identity Service] ska hantera värdet känsligt. |
| Enhets-ID | Enhets-ID:n identifierar maskinvaruenheter som IDFA (iPhone och iPad), GAID (Android) och RIDA (Roku) och kan delas av flera personer i hushåll. |
| E-postadress | E-postadresser är ofta kopplade till en person och kan därför användas för att identifiera den personen i olika kanaler. Identiteter av den här typen omfattar personligt identifierbar information (PII). Detta är en indikation på att [!DNL Identity Service] ska hantera värdet känsligt. |
| Identifierare för icke-personer | ID:n som inte är personer används för att lagra identifierare som kräver namnutrymmen men som inte är anslutna till ett personkluster. Till exempel en produkt-SKU, data relaterade till produkter, organisationer eller butiker. |
| Telefonnummer | Telefonnummer är ofta associerade med en person och kan därför användas för att identifiera den personen i olika kanaler. Identiteter av den här typen är PII. Detta indikerar att [!DNL Identity Service] ska hantera värdet känsligt. |

### Standardnamnutrymmen

I Experience Platform finns flera identitetsnamnutrymmen som är tillgängliga för alla organisationer. Dessa kallas standardnamnutrymmen och visas med API:t [!DNL Identity Service] eller med hjälp av användargränssnittet för plattformen.

Följande standardnamnutrymmen kan användas av alla organisationer på plattformen:

| Visningsnamn | Beskrivning |
| ------------ | ----------- |
| AdCloud | Ett namnutrymme som representerar Adobe AdCloud. |
| Adobe Analytics (äldre ID) | Ett namnutrymme som representerar Adobe Analytics. Mer information finns i följande dokument på [Adobe Analytics-namnutrymmen](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces). |
| Apple IDFA (ID för annonsörer) | Ett namnutrymme som representerar Apple ID för annonsörer. Mer information finns i följande dokument om [intressebaserade annonser](https://support.apple.com/en-us/HT202074). |
| Apple Push Notification-tjänst | Ett namnutrymme som representerar identiteter som samlats in med Apple Push Notification-tjänsten. Mer information finns i följande dokument på [Apple Push Notification service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1). |
| CORE | Ett namnutrymme som representerar Adobe Audience Manager. Det här namnutrymmet kan även refereras till med det äldre namnet: &quot;Adobe AudienceManager&quot;. Mer information finns i följande dokument på [Audience Manager ID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids). |
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](./ecid.md). |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |
| E-post (SHA256, nedsänkt) | Ett namnutrymme för förhasrad e-postadress. Värden som anges i det här namnutrymmet konverteras till gemener innan de hash-kodas med SHA256. Radavståndsavstånd måste trimmas innan en e-postadress normaliseras. Den här inställningen kan inte ändras retroaktivt. Mer information finns i följande dokument om [SHA256 hashing support](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support). |
| Firebase Cloud Messaging | Ett namnutrymme som representerar identiteter som samlats in med Google Firebase Cloud Messaging för push-meddelanden. Mer information finns i följande dokument på [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging). |
| Google Ad ID (GAID) | Ett namnutrymme som representerar ett Google Advertising ID. Mer information finns i följande dokument om [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en). |
| Google Click ID | Ett namnutrymme som representerar ett Google Click-ID. Mer information finns i följande dokument om [Klicka på spårning i Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking). |
| Telefon | Ett namnutrymme som representerar ett telefonnummer. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |
| Telefon (E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas i E.164-format. E.164-formatet innehåller ett plustecken (`+`), en internationell landskod, en lokal områdeskod och ett telefonnummer. Exempel: `(+)(country code)(area code)(phone number)`. |
| Telefon (SHA256) | Ett namnutrymme som representerar telefonnummer som behöver hashas med SHA256. Du måste ta bort symboler, bokstäver och eventuella inledande nollor. Du måste också lägga till landskoden som prefix. |
| Telefon (SHA256_E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas med formaten SHA256 och E.164. |
| TNTID | Ett namnutrymme som representerar Adobe Target. Mer information finns i följande dokument på [Mål](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en). |
| Windows AID | Ett namnutrymme som representerar ett Windows Advertising ID. Mer information finns i följande dokument om [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041). |

Om du vill visa standardnamnutrymmen i användargränssnittet väljer du **[!UICONTROL Identities]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Browse]** för att visa en lista med standardnamnutrymmen för identiteter som är tillgängliga för din organisation. Du kan sortera namnutrymmena i bokstavsordning efter deras **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]** eller **[!UICONTROL Owner]**. Du kan också sortera namnutrymmen kronologiskt efter deras senaste uppdateringsdatum.

Välj ett namnutrymme om du vill visa mer specifik information på den högra listen.

>[!NOTE]
>
>Plattformen har även namnutrymmen för integration. Dessa namnutrymmen döljs som standard eftersom de används för att ansluta till andra system och inte för att fästa identiteter. Om du vill visa integreringsnamnutrymmen väljer du **[!UICONTROL View integration identities]**.

![](./images/browse-namespaces.png)

## Hantera anpassade namnutrymmen

Beroende på dina organisationsdata och användningsfall kan du behöva anpassade namnutrymmen. Du kan skapa anpassade namnutrymmen med API:t [[!DNL Identity Service]](./api/create-custom-namespace.md) eller med gränssnittet.

Om du vill skapa ett anpassat namnutrymme med hjälp av användargränssnittet går du till arbetsytan **[!UICONTROL Identities]**, väljer **[!UICONTROL Browse]** och väljer sedan **[!UICONTROL Create identity namespace]**.

![](./images/create.png)

Dialogrutan **[!UICONTROL Create identity namespace]** visas. Ange en unik **[!UICONTROL Display name]** och **[!UICONTROL Identity symbol]** och välj sedan den identitetstyp som du vill skapa. Du kan också lägga till en valfri beskrivning för mer information om namnutrymmet. När du är klar väljer du **[!UICONTROL Create]**.

>[!IMPORTANT]
>
>Namnutrymmen som du definierar är privata för din organisation och kräver en unik identitetssymbol för att de ska kunna skapas.

![](./images/create-namespace.png)

På samma sätt som vanliga namnutrymmen kan du välja ett anpassat namnutrymme på fliken **[!UICONTROL Browse]** för att visa information om det. Men med ett anpassat namnutrymme kan du även redigera dess visningsnamn och beskrivning från informationsfältet.

>[!NOTE]
>
>När ett namnutrymme har skapats kan det inte tas bort och dess identitetssymbol och typ kan inte ändras.

## Namnutrymmen i identitetsdata

Om du anger namnutrymmet för en identitet beror på vilken metod du använder för att ange identitetsdata. Mer information om att tillhandahålla data om identitetsuppgifter finns i avsnittet [som anger identitetsdata](./home.md#supplying-identity-data-to-identity-service) i översikten [!DNL Identity Service].

## Nästa steg

Nu när du förstår de viktigaste begreppen för identitetsnamnutrymmen kan du börja lära dig hur du arbetar med identitetsdiagrammet med [identitetsdiagramvisningsprogrammet](./ui/identity-graph-viewer.md).
