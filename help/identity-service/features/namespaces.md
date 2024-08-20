---
title: Översikt över namnområde för identitet
description: Lär dig mer om identitetsnamnutrymmen i identitetstjänsten.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 0%

---

# Översikt över namnområde för identitet

Läs följande dokument om du vill veta mer om vad du kan göra med identitetsnamnutrymmen i Adobe Experience Platform Identity Service.

## Komma igång

Identitetsnamnutrymmen kräver förståelse för olika Adobe Experience Platform-tjänster. Innan du börjar arbeta med namnutrymmen bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [[!DNL Privacy Service]](../../privacy-service/home.md): Identitetsnamnutrymmen används i kompatibilitetsbegäranden för juridiska sekretessregler som Allmänna dataskyddsförordningen (GDPR). Varje begäran om integritet görs i förhållande till ett namnutrymme för att identifiera vilka konsumentdata som ska påverkas.

## Identitetsnamnutrymmen {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Identitetsnamnutrymmen"
>abstract="Ett identitetsnamnutrymme är kontexten för en viss identitet. Namnområdet `Email` kan till exempel motsvara **name<span>@acme.com**. På samma sätt kan ett namnutrymme på `Phone` motsvara `555-555-1234`."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Identitetsvärden"
>abstract="Ett identitetsvärde är en identifierare som representerar en unik individ, organisation eller resurs. Kontexten eller typen av identitet som värdet representerar definieras av ett motsvarande identitetsnamnutrymme. När postdata matchas mellan profilfragment måste namnutrymmet och identitetsvärdet matcha. När postdata matchas mellan profilfragment måste namnutrymmet och identitetsvärdet matcha."
>text="Learn more in documentation"

En fullständigt kvalificerad identitet innehåller två komponenter: ett **identitetsvärde** och ett **identitetsnamnområde**. Om värdet för en identitet till exempel är `scott@acme.com`, ger ett namnutrymme kontext till det här värdet genom att det särskiljs som en e-postadress. På samma sätt kan ett namnutrymme skilja `555-123-456` från ett telefonnummer och `3126ABC` som ett CRMID. I princip ger **ett namnutrymme kontext till en given identitet**. När postdata matchas mellan profilfragment, som när [!DNL Real-Time Customer Profile] sammanfogar profildata, måste både identitetsvärdet och namnutrymmet matcha.

Två profilfragment kan t.ex. innehålla olika primära ID:n, men de delar samma värde för namnutrymmet&quot;E-post&quot;. Därför kan Experience Platform se att dessa fragment faktiskt är samma individ och sammanför data i identitetsdiagrammet för individen.

>[!BEGINSHADEBOX]

**Identitetsnamnrymden förklaras**

Ett annat sätt att bättre förstå begreppet namnutrymme är att överväga verkliga exempel som städer och deras motsvarande lägen. Till exempel är Portland, Maine och Portland, Oregon två olika platser i USA. Städerna har samma namn, men läget fungerar som ett namnutrymme och ger nödvändigt sammanhang som skiljer de två städerna från varandra.

Använd samma logik för identitetstjänsten:

* Ett ögonblick kan identitetsvärdet för `1-234-567-8900` se ut som ett telefonnummer. Ur ett systemperspektiv kunde det här värdet dock ha konfigurerats som ett CRMID. Identitetstjänsten skulle inte kunna använda den nödvändiga kontexten för det här identitetsvärdet utan ett motsvarande namnutrymme.
* Ett annat exempel är identitetsvärdet för: `john@gmail.com`. Även om det här identitetsvärdet enkelt kan antas vara ett e-postmeddelande är det helt möjligt att det har konfigurerats som ett anpassat namnområdes-CRMID. Med namnutrymme kan du skilja `Email:john@gmail.com` från `CRMID:john@gmail.com`.

>[!ENDSHADEBOX]

### Komponenter i ett namnutrymme

Ett namnutrymme består av följande komponenter:

* **Visningsnamn**: Det användarvänliga namnet för ett givet namnområde.
* **Identitetssymbol**: En kod som används internt av identitetstjänsten för att representera ett namnutrymme.
* **Identitetstyp**: Klassificeringen av ett givet namnutrymme.
* **Beskrivning**: (Valfritt) All tilläggsinformation som du kan ange för ett givet namnutrymme.

### Identitetstyp {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Ange identitetstyp"
>abstract="Identitetstypen styr om data lagras i identitetsdiagrammet eller inte. Identitetsdiagram genereras inte för följande identitetstyper: icke-personidentifierare och partner-ID."
>text="Learn more in documentation"

Ett element i ett identitetsnamnområde är **identitetstypen**. Identitetstypen bestämmer:

* Om ett identitetsdiagram ska genereras:
   * Identitetsdiagram genereras inte för följande identitetstyper: icke-personidentifierare och partner-ID.
   * Identitetsdiagram genereras för alla andra identitetstyper.
* Vilka identiteter som tas bort från identitetsdiagrammet när systemgränserna nås. Mer information finns i [skyddsjournalerna för identitetsdata](../guardrails.md).

Följande identitetstyper är tillgängliga i Experience Platform:

| Identitetstyp | Beskrivning |
| --- | --- |
| Cookie-ID | Cookie-ID:n identifierar webbläsare. Dessa identiteter är viktiga för expansion och utgör huvuddelen av identitetsdiagrammet. Av naturen sjunker de dock snabbt och förlorar sitt värde över tiden. |
| Enhets-ID | Enhetsoberoende ID:n identifierar en individ och knyter vanligtvis samman andra ID:n. Exempel är inloggnings-ID, CRMID och lojalitets-ID. Detta är en indikation till [!DNL Identity Service] att hantera värdet känsligt. |
| Enhets-ID | Enhets-ID:n identifierar maskinvaruenheter som IDFA (iPhone och iPad), GAID (Android) och RIDA (Roku) och kan delas av flera personer i hushåll. |
| E-postadress | E-postadresser är ofta kopplade till en person och kan därför användas för att identifiera den personen i olika kanaler. Identiteter av den här typen omfattar personligt identifierbar information (PII). Detta är en indikation till [!DNL Identity Service] att hantera värdet känsligt. |
| Identifierare för icke-personer | ID:n som inte är personer används för att lagra identifierare som kräver namnutrymmen men som inte är anslutna till ett personkluster. Till exempel en produkt-SKU, data relaterade till produkter, organisationer eller butiker. |
| Partner-ID | <ul><li>Partner-ID:n är identifierare som används av datapartners för att representera människor. Partners-ID:n är ofta pseudonyma så att de inte avslöjar en persons sanna identitet och kan vara sannolika. I Real-time Customer Data Platform används partner-ID:n i första hand för att öka målgruppsaktiveringen och förbättra data, och inte för att skapa länkar till identitetsdiagram.</li><li>Identitetsdiagram genereras inte vid inmatning av en identitet som innehåller ett identitetsnamnområde som har angetts som Partner ID-typ.</li><li>Om partnerdata inte importeras med identitetstypen för partner-ID kan det leda till systemdiagrambegränsningar för identitetstjänsten samt oönskad sammanslagning av profiler.</li><ul> |
| Telefonnummer | Telefonnummer är ofta associerade med en person och kan därför användas för att identifiera den personen i olika kanaler. Identiteter av den här typen är PII. Det här är en indikation till [!DNL Identity Service] att hantera värdet känsligt. |

{style="table-layout:auto"}

### Standardnamnutrymmen {#standard}

I Experience Platform finns flera identitetsnamnutrymmen som är tillgängliga för alla organisationer. Dessa kallas standardnamnutrymmen och visas med API:t [!DNL Identity Service] eller med hjälp av användargränssnittet för plattformen.

Följande standardnamnutrymmen kan användas av alla organisationer på plattformen:

| Visningsnamn | Beskrivning |
| ------------ | ----------- |
| AdCloud | Ett namnutrymme som representerar Adobe AdCloud. |
| Adobe Analytics (äldre ID) | Ett namnutrymme som representerar Adobe Analytics. Mer information finns i följande dokument om [Adobe Analytics-namnutrymmen](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces). |
| Apple IDFA (ID för annonsörer) | Ett namnutrymme som representerar Apple ID för annonsörer. Mer information finns i följande dokument om [intressebaserade annonser](https://support.apple.com/en-us/HT202074). |
| Tjänsten Apple Push Notification | Ett namnutrymme som representerar identiteter som samlats in med tjänsten Apple Push Notification. Mer information finns i följande dokument på [tjänsten Apple Push Notification](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1). |
| ECID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](./ecid.md). |
| E-post | Ett namnutrymme som representerar en e-postadress. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |
| E-post (SHA256, nedsänkt) | Ett namnutrymme för förhasrad e-postadress. Värden som anges i det här namnutrymmet konverteras till gemener innan de hash-kodas med SHA256. Radavståndsavstånd måste trimmas innan en e-postadress normaliseras. Den här inställningen kan inte ändras retroaktivt. Mer information finns i följande dokument om [SHA256-hash-stöd](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support). |
| Firebase Cloud Messaging | Ett namnutrymme som representerar identiteter som samlats in med Google Firebase Cloud Messaging för push-meddelanden. Mer information finns i följande dokument om [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging). |
| Google Ad ID (GAID) | Ett namnutrymme som representerar ett Google Advertising ID. Mer information finns i följande dokument på [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en). |
| Telefon | Ett namnutrymme som representerar ett telefonnummer. Den här typen av namnutrymme är ofta kopplad till en person och kan därför användas för att identifiera den personen i olika kanaler. |
| Telefon (E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas i E.164-format. E.164-formatet innehåller ett plustecken (`+`), en internationell landskod, en lokal områdeskod och ett telefonnummer. Till exempel: `(+)(country code)(area code)(phone number)`. |
| Telefon (SHA256) | Ett namnutrymme som representerar telefonnummer som behöver hashas med SHA256. Du måste ta bort symboler, bokstäver och eventuella inledande nollor. Du måste också lägga till landskoden som prefix. |
| Telefon (SHA256_E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas med formaten SHA256 och E.164. |
| TNTID | Ett namnutrymme som representerar Adobe Target. Mer information finns i följande dokument på [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html). |
| Windows AID | Ett namnutrymme som representerar ett Advertising-ID för Windows. Mer information finns i följande dokument på [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041). |

### Visa ID-namnutrymmen {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Visa integreringsidentiteter"
>abstract="Integreringsidentiteter är namnutrymmen som används för att ansluta till andra system och som inte används i identitetsupplösning eller för att sätta ihop identiteter. <br> Dessa identiteter är dolda som standard. Använd växlingsknappen för att visa integreringsnamnutrymmen."

Om du vill visa identitetsnamnutrymmen i användargränssnittet väljer du **[!UICONTROL Identities]** i den vänstra navigeringen och sedan **[!UICONTROL Browse]**.

En katalog med namnutrymmen i organisationen visas med information om namn, identitetssymboler, senaste uppdaterade datum, motsvarande identitetstyper och beskrivning.

![En katalog med anpassade identitetsnamnutrymmen i din organisation.](../images/namespace/browse.png)

## Skapa anpassade namnutrymmen {#create-namespaces}

Beroende på dina organisationsdata och användningsfall kan du behöva anpassade namnutrymmen. Du kan skapa anpassade namnutrymmen med API:t [[!DNL Identity Service]](../api/create-custom-namespace.md) eller med gränssnittet.

Om du vill skapa ett anpassat namnområde väljer du **[!UICONTROL Create identity namespace]**.

>[!TIP]
>
>Integreringsidentiteter är namnutrymmen som används för att ansluta till andra system. De används inte i identitetsupplösning och används inte heller för att sätta ihop identiteter. Välj **[!UICONTROL View integration identities]** om du vill uppdatera listan och inkludera integreringsidentiteter. Integreringsidentiteter döljs som standard eftersom de är skrivskyddade och du inte behöver konfigurera dem.

![Knappen Skapa ID-namnområde på identitetsytan.](../images/namespace/create-identity-namespace.png)

Fönstret [!UICONTROL Create identity namespace] visas. Först måste du ange ett visningsnamn och en identitetssymbol för det anpassade namnutrymmet som du vill skapa. Du kan också ange en beskrivning för att lägga till mer kontext i det anpassade namnutrymmet som du skapar.

![Ett popup-fönster där du kan ange information om ditt anpassade identitetsnamnutrymme.](../images/namespace/name-and-symbol.png)

Välj sedan den identitetstyp som du vill tilldela det anpassade namnutrymmet. När du är klar väljer du **[!UICONTROL Create]**.

![Ett urval identitetstyper som du kan välja mellan och tilldela till ditt anpassade identitetsnamnområde.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Namnutrymmen som du definierar är privata för din organisation och kräver en unik identitetssymbol för att de ska kunna skapas.
>
>* När ett namnutrymme har skapats kan det inte tas bort och dess identitetssymbol och typ kan inte ändras.
>
>* Duplicerade namnutrymmen stöds inte. Du kan inte använda ett befintligt visningsnamn och en identitetssymbol när du skapar ett nytt namnutrymme.

## Namnutrymmen i identitetsdata

Om du anger namnutrymmet för en identitet beror på vilken metod du använder för att ange identitetsdata. Mer information om hur du tillhandahåller data-ID-data finns i [[!DNL Identity Service] implementeringsguiden](../implementation.md).

## Nästa steg

Nu när du förstår de viktigaste begreppen för identitetsnamnutrymmen kan du börja lära dig hur du arbetar med identitetsdiagrammet med [identitetsdiagramvisningsprogrammet](../features/identity-graph-viewer.md).
