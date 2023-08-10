---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmentmatchning;segmentmatchning
solution: Experience Platform
title: Översikt över segmentmatchning
description: Segmentmatchning är en segmentdelningstjänst i Adobe Experience Platform som gör det möjligt för två eller flera plattformsanvändare att utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 0%

---

# [!DNL Segment Match] översikt

Adobe Experience Platform Segment Match är en segmentdelningstjänst som gör det möjligt för två eller flera plattformsanvändare att utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt. [!DNL Segment Match] använder sekretessstandarder för plattformer och personliga identifierare som hash-kodade e-postmeddelanden, hashade telefonnummer och enhetsidentifierare som IDFA och GAID.

Med [!DNL Segment Match] du kan:

* Hantera processen för identitetsöverlappning.
* Visa uppskattningar före delning.
* Använd etiketter för dataanvändning för att kontrollera om data kan delas med partners.
* Bibehåll livscykelhanteringen för delade målgrupper efter att ha publicerat en feed och fortsätt ett dynamiskt datautbyte genom att lägga till, ta bort och ta bort delning.

[!DNL Segment Match] använder en process för identitetsöverlappning för att säkerställa att segmentdelning sker på ett säkert och sekretessfokuserat sätt. An **överlappad identitet** är en identitet som matchar både ditt segment och den valda partnerns segment. Innan ett segment delas mellan en avsändare och en mottagare kontrolleras om namnutrymmen överlappar varandra och om det finns godkännandekontroller mellan avsändaren och mottagaren/mottagarna. Båda överlappningskontrollerna måste skickas för att ett segment ska kunna delas.

I följande avsnitt finns mer information om [!DNL Segment Match], inklusive information om konfiguration och hela arbetsflödet.

## Inställningar

I följande avsnitt beskrivs hur du konfigurerar och konfigurerar [!DNL Segment Match]:

### Konfigurera identitetsdata och namnutrymmen {#namespaces}

Det första steget till att komma igång med [!DNL Segment Match] är att kontrollera att du matar in data mot de identitetsnamnutrymmen som stöds.

Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../../identity-service/home.md). Varje kundidentitet innehåller ett associerat namnutrymme som anger identitetsens kontext. Ett namnutrymme kan till exempel skilja på värdet &quot;name&quot;<span>@email.com som e-postadress eller 443522 som ett numeriskt CRM-ID.

En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. Vid matchning av postdata mellan profilfragment (till exempel när [!DNL Real-Time Customer Profile] sammanfogar profildata), måste både identitetsvärdet och namnutrymmet matcha.

I samband med [!DNL Segment Match]används namnutrymmen i överlappningsprocessen när data delas.

Nedan följer en lista över namnutrymmen som stöds:

| Namnutrymme | Beskrivning |
| --------- | ----------- |
| E-post (SHA256, nedsänkt) | Ett namnutrymme för förhasrad e-postadress. Värden som anges i det här namnutrymmet konverteras till gemener innan de hash-kodas med SHA256. Radavståndsavstånd måste trimmas innan en e-postadress normaliseras. Den här inställningen kan inte ändras retroaktivt. Platform erbjuder två metoder som stöder hashning vid datainsamling, via [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) och via [dataprestation](../../../data-prep/functions.md#hashing). |
| Telefon (SHA256_E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas med formaten SHA256 och E.164. |
| ECID | Ett namnutrymme som representerar ett Experience Cloud ID-värde (ECID). Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Se [ECID - översikt](../../../identity-service/ecid.md) för mer information. |
| Apple IDFA (ID för annonsörer) | Ett namnutrymme som representerar Apple ID för annonsörer. Se följande dokument på [räntebaserade annonser](https://support.apple.com/en-us/HT202074) för mer information. |
| Google Ad ID | Ett namnutrymme som representerar ett Google Advertising ID. Se följande dokument på [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) för mer information. |

### Konfigurera samtycke

Du måste ange en medgivandekonfiguration och ange standardvärdet till antingen `opt-in` eller `opt-out` för en godkännandekontroll.

Kontrollen av godkännande av anmälan och avanmälan avgör om du kan arbeta med samtycke att dela användardata som standard. Om standardinställningen för medgivandekonfigurationen är inställd på `opt-out`kan användardata delas, såvida inte användaren uttryckligen avanmäler sig. Om standardvärdet är `opt-in`kan användardata inte delas, såvida inte användaren uttryckligen väljer att göra det.

Standardkonfiguration för samtycke för [!DNL Segment Match] är inställd på `opt-out`. Om du vill tillämpa en anmälningsmodell för dina data skickar du en e-postförfrågan till ditt Adobe-kontoteam.

Mer information om `share` det attribut som används för att ange medgivandevärde för datadelning finns i följande dokumentation om [sekretess- och innehållsfältgrupp](../../../xdm/field-groups/profile/consents.md). Mer information om den specifika fältgrupp som används för att samla in och använda konsumentens samtycke till insamling och användning av data som rör sekretess, personalisering och marknadsföring finns i följande [Godkännande av GitHub för inställningar för sekretess, personalisering och marknadsföring](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Konfigurera etiketter för dataanvändning

Den sista förutsättningen du måste ställa är att konfigurera en ny dataanvändningsetikett för att förhindra datadelning. Genom dataanvändningsetiketter kan du hantera vilka data som får delas via [!DNL Segment Match].

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till märkning av data så snart de hämtas till Experience Platform, eller så snart data blir tillgängliga för användning i plattformen.

[!DNL Segment Match] använder etiketten C11, en kontraktsetikett som är specifik för [!DNL Segment Match] som du manuellt kan lägga till i datauppsättningar eller attribut för att vara säker på att de inte tas med i [!DNL Segment Match] partnerdelningsprocess. C11-etiketten anger data som inte ska användas i [!DNL Segment Match] -processer. När du har fastställt vilka datauppsättningar och/eller fält du vill utesluta från [!DNL Segment Match] och lägger till etiketten C11 i enlighet med detta, kommer etiketten att framtvingas automatiskt av [!DNL Segment Match] arbetsflöde. [!DNL Segment Match] aktiverar automatiskt [!UICONTROL Restrict data sharing] grundpolicy. Specifika anvisningar om hur du använder dataetiketter på datauppsättningar finns i självstudiekursen om [hantera dataanvändningsetiketter i användargränssnittet](../../../data-governance/labels/user-guide.md).

En lista över dataanvändningsetiketter och definitioner av dessa finns i [ordlista för etiketter för dataanvändning](../../../data-governance/labels/reference.md). Information om dataanvändningsprinciper finns i [dataanvändningsprinciper - översikt](../../../data-governance/policies/overview.md).

### Förstå [!DNL Segment Match] behörigheter

Det finns två behörigheter som är associerade med [!DNL Segment Match]:

| Behörighet | Beskrivning |
| --- | --- |
| Hantera anslutningar för målgruppsdelning | Med den här behörigheten kan du slutföra partnerhandskakningsprocessen, som kopplar samman två organisationer för att aktivera [!DNL Segment Match] flöden. |
| Hantera målgruppsresurser | Med denna behörighet kan du skapa, redigera och publicera feeds (det datapaket som används för [!DNL Segment Match]) med aktiva partners (partners som administratörsanvändaren har anslutit till **[!UICONTROL Audience Share Connections]** åtkomst). |

Se [åtkomstkontroll - översikt](../../../access-control/home.md) för mer information om åtkomstkontroll och behörigheter.

## [!DNL Segment Match] från början till slut

När du har konfigurerat dina identitetsdata och namnutrymmen, konfiguration för samtycke och etikett för dataanvändning kan du börja arbeta med [!DNL Segment Match] och dess funktioner.

### Hantera partner

Välj **[!UICONTROL Segments]** i den vänstra navigeringen och välj **[!UICONTROL Feeds]** i det övre sidhuvudet.

![segment-feed.png](./images/segments-feed.png)

The [!UICONTROL Feeds] sidan innehåller en lista med feeds som du har delat med dig av både partner och feeds. Om du vill visa en lista över befintliga partner eller skapa en anslutning till en ny partner väljer du **[!UICONTROL Manage partners]**.

![manage-partners.png](./images/manage-partners.png)

En anslutning mellan två partner är en&quot;tvåvägshandskakning&quot; som fungerar som en självbetjäningsmetod för användare som vill koppla samman sina plattformsorganisationer på sandlådenivå. Anslutningen krävs för att informera plattformen om att ett avtal har upprättats och att plattformen kan underlätta delning av tjänster mellan dig och din partner.

>[!NOTE]
>
>&quot;Tvåvägshandskakningen&quot; mellan dig och din partner är helt enkelt en koppling. Inga data utbyts under denna process.

Du kan visa en lista över anslutningar med befintliga partners i huvudgränssnittet i [!UICONTROL Manage partners] skärm. På den högra listen är [!UICONTROL Share setting] som ger dig möjlighet att skapa en ny [!UICONTROL connect ID] samt en inmatningsruta där du kan ange en partners [!UICONTROL connect ID].

![create-connection.png](./images/establish-connection.png)

Så här skapar du en ny [!UICONTROL connect ID], markera **[!UICONTROL Regenerate]** under [!UICONTROL Share setting] och välj sedan kopieringsikonen bredvid det nyligen genererade ID:t.

![share-setting.png](./images/share-setting.png)

Så här ansluter du en partner med deras [!UICONTROL connect ID]anger du deras unika ID-värde i inmatningsrutan under [!UICONTROL Connect partner] och sedan **[!UICONTROL Request]**.

![connect-partner.png](./images/connect-partner.png)

### Skapa feed {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Begränsade användningsfall för marknadsföring"
>abstract="Begränsade användningsexempel för marknadsföring hjälper er att ge vägledning till era partner för att säkerställa att delade segment används korrekt enligt era begränsningar för datastyrning."
>text="Learn more in documentation"

A **feed** är en gruppering av data (segment), regler för hur data kan exponeras eller användas och konfigurationer som bestämmer hur data matchas mot dina partners data. En feed kan hanteras oberoende och utbytas med andra plattformsanvändare via [!DNL Segment Match].

Om du vill skapa en ny feed väljer du **[!UICONTROL Create feed]** från [!UICONTROL Feeds] kontrollpanel.

![create-feed.png](./images/create-feed.png)

Den grundläggande konfigurationen av en feed innehåller ett namn, en beskrivning och konfigurationer för användningsfall för marknadsföring och identitetsinställningar. Ange ett namn och en beskrivning för din feed och använd sedan de användningsfall för marknadsföring som du vill att dina data ska uteslutas från. Du kan välja mer än ett användningsfall i en lista som innehåller:

* [!UICONTROL Analytics]
* [!UICONTROL Combine with PII]
* [!UICONTROL Cross-site targeting]
* [!UICONTROL Data Science]
* [!UICONTROL Email targeting]
* [!UICONTROL Export to third party]
* [!UICONTROL Onsite advertising]
* [!UICONTROL Onsite personalization]
* [!UICONTROL Segment Match]
* [!UICONTROL Single identity personalization]

Välj sedan lämpliga identitetsnamnutrymmen för din feed. Mer information om de namnutrymmen som stöds av [!DNL Segment Match], se [ID-data och namnutrymmesregister](#namespaces). När du är klar väljer du **[!UICONTROL Next]**.

![audiens-sharing.png](./images/audience-sharing.png)

När du har fastställt inställningarna för din feed väljer du de segment som du vill dela i listan över förstapartssegment. Du kan markera mer än ett segment i listan och du kan använda den högra listen för att hantera listan över valda segment. När du är klar väljer du **[!UICONTROL Next]**.

![select-segments.png](./images/select-segments.png)

The [!UICONTROL Share] visas med ett gränssnitt där du kan välja vilka partners du vill dela din feed med. Under det här steget kan du även visa uppskattningsrapporten för överlappning före delning och se antalet överlappande identiteter per namnutrymme mellan dig och din partner, antalet överlappande identiteter som har samtycke till att dela data.

Välj **[!UICONTROL Analyze by segment]** för att se rapporten med uppskattningar.

![analyze.png](./images/analyze.png)

Med hjälp av överlappningsuppskattningsrapporten kan du hantera överlappnings- och godkännandekontroller per partner och per segment innan du delar din feed.

| Mätvärden | Beskrivning |
| ------- | ----------- |
| Uppskattade identiteter med samtycke | Det totala antalet överlappande identiteter som uppfyller de krav för samtycke som konfigurerats för din organisation. |
| Uppskattad överlappande identiteter | Antalet identiteter som är kvalificerade för det valda segmentet och som också matchar den valda partnern. Dessa identiteter visas med namnutrymme och representerar inte enskilda profilidentiteter. Överlappningsuppskattningarna baseras på profilskisser. |

När du är klar väljer du **[!UICONTROL Close]**.

![overlap-report.png](./images/overlap-report.png)

När du har valt dina partners och visat din rapport över överlappande uppskattningar väljer du **[!UICONTROL Next]** för att fortsätta.

![share.png](./images/share.png)

The [!UICONTROL Review] visas så att du kan granska din nya feed innan den delas och publiceras. I det här steget finns information om den identitetsinställning du har använt samt information om de användningsfall, segment och partners du har valt.

Välj **[!UICONTROL Finish]** för att fortsätta.

![review.png](./images/review.png)

### Uppdatera feed

Om du vill lägga till eller ta bort segment väljer du **[!UICONTROL Create feed]** från [!UICONTROL Feeds] sida och sedan markera **[!UICONTROL Existing feed]**. Markera den feed som du vill uppdatera i listan över befintliga feed som visas och välj sedan **[!UICONTROL Next]**.

![feed-list](./images/feed-list.png)

Listan med segment visas. Härifrån kan du lägga till nya segment i din feed och du kan använda högerspåret för att ta bort segment som du inte längre behöver. När du är klar med att hantera segmenten i din feed väljer du **[!UICONTROL Next]** och följ sedan de steg som beskrivs ovan för att slutföra den uppdaterade feeden.

![update](./images/update.png)

>[!NOTE]
>
>När du lägger till eller tar bort ett segment från en delad feed måste den mottagande partnern bekräfta ändringen genom att aktivera om [!DNL Profile] i sin lista över mottagna feeds.

### Acceptera en inkommande feed

Om du vill visa en inkommande feed väljer du **[!UICONTROL Received]** i sidhuvudet på [!UICONTROL Feeds] och välj sedan den feed du vill visa från listan. Om du vill acceptera flödet väljer du **[!UICONTROL Enable for profile]** och kan uppdatera från [!UICONTROL Pending] till [!UICONTROL Enabled].

![receive.png](./images/received.png)

När du har accepterat en delad feed kan du börja använda delade data för att skapa nya segment.

## Nästa steg

Genom att läsa det här dokumentet har du fått en förståelse för [!DNL Segment Match], dess funktioner och hela arbetsflödet. Läs följande dokument om du vill veta mer om andra plattformstjänster:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] översikt](../../../profile/home.md)
