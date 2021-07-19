---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmentmatchning;segmentmatchning
solution: Experience Platform
title: Översikt över segmentmatchning
topic-legacy: overview
description: Segmentmatchning är en segmentdelningstjänst i Adobe Experience Platform som gör det möjligt för två eller flera plattformsanvändare att utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# (Alfa) [!DNL Segment Match] - översikt

>[!IMPORTANT]
>
>[!DNL Segment Match] är alfavärdet. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform Segment Match är en segmentdelningstjänst som gör det möjligt för två eller flera plattformsanvändare att utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt. [!DNL Segment Match] använder sekretessstandarder för plattformer och personliga identifierare som hash-kodade e-postmeddelanden, hashade telefonnummer och enhetsidentifierare som IDFA och GAID.

Med [!DNL Segment Match] kan du:

* Hantera processen för identitetsöverlappning.
* Visa uppskattningar före delning.
* Använd etiketter för dataanvändning för att kontrollera om data kan delas med partners.
* Bibehåll livscykelhanteringen för delade målgrupper efter att ha publicerat en feed och fortsätt ett dynamiskt datautbyte genom att lägga till, ta bort och ta bort delning.

[!DNL Segment Match] använder en process för identitetsöverlappning för att säkerställa att segmentdelning sker på ett säkert och sekretessfokuserat sätt. En **överlappad identitet** är en identitet som matchar både ditt segment och den valda partnerns segment. Innan ett segment delas mellan en avsändare och en mottagare kontrolleras om namnutrymmen överlappar varandra och om det finns godkännandekontroller mellan avsändaren och mottagaren/mottagarna. Båda överlappningskontrollerna måste skickas för att ett segment ska kunna delas.

I följande avsnitt finns mer information om [!DNL Segment Match], inklusive information om konfiguration och arbetsflöde från början till slut.

## Inställningar

I följande avsnitt beskrivs hur du konfigurerar och konfigurerar [!DNL Segment Match]:

### Konfigurera identitetsdata och namnutrymmen {#namespaces}

Det första steget för att komma igång med [!DNL Segment Match] är att se till att du importerar data mot de identitetsnamnutrymmen som stöds.

Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../identity-service/home.md). Varje kundidentitet innehåller ett associerat namnutrymme som anger identitetsens kontext. Ett namnutrymme kan till exempel skilja ett värde på&quot;name<span>@email.com&quot; från en e-postadress eller&quot;443522&quot; från ett numeriskt CRM-ID.

En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. När postdata matchas mellan profilfragment (till exempel när [!DNL Real-time Customer Profile] sammanfogar profildata) måste både identitetsvärdet och namnutrymmet matcha.

I sammanhanget [!DNL Segment Match] används namnutrymmen i överlappningsprocessen när data delas.

Nedan följer en lista över namnutrymmen som stöds:

| Namnutrymme | Beskrivning |
| --------- | ----------- |
| E-post (SHA256, nedsänkt) | Ett namnutrymme för förhasrad e-postadress. Värden som anges i det här namnutrymmet konverteras till gemener innan de hash-kodas med SHA256. Radavståndsavstånd måste trimmas innan en e-postadress normaliseras. Den här inställningen kan inte ändras retroaktivt. Mer information finns i följande dokument om [SHA256 hashing support](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support). |
| Telefon (SHA256_E.164) | Ett namnutrymme som representerar råa telefonnummer som behöver hashas med formaten SHA256 och E.164. |
| ECID | Ett namnutrymme som representerar ett Experience Cloud ID-värde (ECID). Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Mer information finns i [ECID-översikt](../../identity-service/ecid.md). |
| Apple IDFA (ID för annonsörer) | Ett namnutrymme som representerar Apple ID för annonsörer. Mer information finns i följande dokument om [intressebaserade annonser](https://support.apple.com/en-us/HT202074). |
| Google Ad ID | Ett namnutrymme som representerar ett Google Advertising ID. Mer information finns i följande dokument om [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en). |

### Konfigurera samtycke

Du måste ange en medgivandekonfiguration och ange standardvärdet till antingen `opt-in` eller `opt-out` för en medgivandekontroll.

Kontrollen av godkännande av anmälan och avanmälan avgör om du kan arbeta med samtycke att dela användardata som standard. Om standardinställningen för medgivandekonfigurationen är `opt-in` kan användardata delas, såvida inte en användare uttryckligen avanmäler sig. Om standardvärdet är `opt-out` kan användardata inte delas, såvida inte en användare uttryckligen väljer att göra det.

Standardkonfigurationen för medgivande för [!DNL Segment Match] är `opt-out`. Om du vill tillämpa en anmälningsmodell för dina data skickar du en e-postförfrågan till kontohanteraren för Adobe.

Mer information om `share`-attributet som används för att ange medgivandevärde för datadelning finns i följande dokumentation för [fältgruppen ](../../xdm/field-groups/profile/consents.md) sekretess och innehåll. Mer information om den specifika fältgrupp som används för att samla in och använda konsumentens samtycke till insamling och användning av data som rör sekretess, personalisering och marknadsföring finns i följande [GitHub-exempel på godkännande för sekretess, personalisering och marknadsföring](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Konfigurera etiketter för dataanvändning

Den sista förutsättningen du måste ställa är att konfigurera en ny dataanvändningsetikett för att förhindra datadelning. Genom dataanvändningsetiketter kan du hantera vilka data som får delas via [!DNL Segment Match].

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till märkning av data så snart de hämtas till Experience Platform, eller så snart data blir tillgängliga för användning i plattformen.

[!DNL Segment Match] använder etiketten C11, en kontraktsetikett som är specifik för  [!DNL Segment Match] att du manuellt kan lägga till i en datauppsättning eller attribut för att vara säker på att de utesluts från  [!DNL Segment Match] partnerdelningsprocessen. C11-etiketten anger data som inte ska användas i [!DNL Segment Match]-processer. När du har fastställt vilka datauppsättningar och/eller fält du vill utesluta från [!DNL Segment Match] och lagt till C11-etiketten i enlighet med detta, används etiketten automatiskt i arbetsflödet [!DNL Segment Match]. [!DNL Segment Match] aktiverar automatiskt  [!UICONTROL Restrict data sharing] huvudprincipen. Specifika anvisningar om hur du använder dataanvändningsetiketter på datauppsättningar finns i självstudiekursen om att [hantera dataanvändningsetiketter i användargränssnittet](../../data-governance/labels/user-guide.md).

En lista över dataanvändningsetiketter och definitioner finns i [ordlistan för dataanvändningsetiketter](../../data-governance/labels/reference.md). Mer information om dataanvändningsprinciper finns i översikten över [dataanvändningsprinciper](../../data-governance/policies/overview.md).

## [!DNL Segment Match] från början till slut

När du har konfigurerat dina identitetsdata och namnutrymmen, konfiguration för samtycke och etikett för dataanvändning kan du börja arbeta med [!DNL Segment Match] och dess funktioner.

### Hantera partner

Välj **[!UICONTROL Segments]** i vänster navigering i plattformsgränssnittet och välj sedan **[!UICONTROL Feeds]** i den övre rubriken.

![segment-feed.png](../images/ui/segment-match/segments-feed.png)

Sidan [!UICONTROL Feeds] innehåller en lista över feeds som tagits emot från partner samt feeds som du har delat. Välj **[!UICONTROL Manage partners]** om du vill visa en lista över befintliga partner eller skapa en anslutning till en ny partner.

![manage-partners.png](../images/ui/segment-match/manage-partners.png)

En anslutning mellan två partner är en&quot;tvåvägshandskakning&quot; som fungerar som en självbetjäningsmetod för användare som vill koppla samman sina plattformsorganisationer på sandlådenivå. Anslutningen krävs för att informera plattformen om att ett avtal har upprättats och att plattformen kan underlätta delning av tjänster mellan dig och din partner.

>[!NOTE]
>
>&quot;Tvåvägshandskakningen&quot; mellan dig och din partner är helt enkelt en koppling. Inga data utbyts under denna process.

Du kan visa en lista över anslutningar med befintliga partners i huvudgränssnittet på [!UICONTROL Manage partners]-skärmen. På den högra listen finns panelen [!UICONTROL Share setting] där du kan välja att generera en ny [!UICONTROL connect ID] samt en inmatningsruta där du kan ange en partners [!UICONTROL connect ID].

![create-connection.png](../images/ui/segment-match/establish-connection.png)

Om du vill skapa ett nytt [!UICONTROL connect ID] väljer du **[!UICONTROL Regenerate]** under [!UICONTROL Share setting] och sedan kopieringsikonen bredvid det nyligen genererade ID:t.

![share-setting.png](../images/ui/segment-match/share-setting.png)

Om du vill ansluta en partner med hjälp av deras [!UICONTROL connect ID] anger du deras unika ID-värde i inmatningsrutan under [!UICONTROL Connect partner] och väljer sedan **[!UICONTROL Request]**.

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### Skapa feed

En **feed** är en gruppering av data (segment), reglerna för hur data kan exponeras eller användas och konfigurationerna som bestämmer hur data matchas mot dina partners data. En feed kan hanteras oberoende av varandra och utbytas med andra plattformsanvändare via [!DNL Segment Match].

Om du vill skapa en ny feed väljer du **[!UICONTROL Create feed]** på kontrollpanelen [!UICONTROL Feeds].

![create-feed.png](../images/ui/segment-match/create-feed.png)

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

Välj sedan lämpliga identitetsnamnutrymmen för din feed. Mer information om de namnutrymmen som stöds av [!DNL Segment Match] finns i tabellen [identitetsdata och namnutrymmen](#namespaces). När du är klar väljer du **[!UICONTROL Next]**.

![audiens-sharing.png](../images/ui/segment-match/audience-sharing.png)

När du har fastställt inställningarna för din feed väljer du de segment som du vill dela i listan över förstapartssegment. Du kan markera mer av ett segment i listan och du kan använda den högra listen för att hantera listan över valda segment. När du är klar väljer du **[!UICONTROL Next]**.

![select-segments.png](../images/ui/segment-match/select-segments.png)

Sidan [!UICONTROL Share] visas med ett gränssnitt där du kan välja vilka partners du vill dela din feed med. Under det här steget kan du även visa uppskattningsrapporten för överlappning före delning och se antalet överlappande identiteter per namnutrymme mellan dig och din partner, antalet överlappande identiteter som har samtycke till att dela data.

Välj **[!UICONTROL Analyze by segment]** om du vill visa uppskattningsrapporten.

![analyze.png](../images/ui/segment-match/analyze.png)

Med hjälp av överlappningsuppskattningsrapporten kan du hantera överlappnings- och godkännandekontroller per partner och per segment innan du delar din feed.

| Mätvärden | Beskrivning |
| ------- | ----------- |
| Uppskattade identiteter med samtycke | Det totala antalet överlappande identiteter som uppfyller de krav för samtycke som konfigurerats för din organisation. |
| Uppskattad överlappande identiteter | Antalet identiteter som är kvalificerade för det valda segmentet och som också matchar den valda partnern. Dessa identiteter visas med namnutrymme och representerar inte enskilda profilidentiteter. Överlappningsuppskattningarna baseras på profilskisser. |

När du är klar väljer du **[!UICONTROL Close]**.

![overlap-report.png](../images/ui/segment-match/overlap-report.png)

När du har valt dina partners och visat din rapport över överlappande uppskattningar väljer du **[!UICONTROL Next]** för att fortsätta.

![share.png](../images/ui/segment-match/share.png)

[!UICONTROL Review]-steget visas, så att du kan granska din nya feed innan den delas och publiceras. I det här steget finns information om den identitetsinställning du har använt samt information om de användningsfall, segment och partners du har valt.

Välj **[!UICONTROL Finish]** för att fortsätta.

![review.png](../images/ui/segment-match/review.png)

### Uppdatera feed

Om du vill lägga till eller ta bort segment väljer du **[!UICONTROL Create feed]** på sidan [!UICONTROL Feeds] och väljer sedan **[!UICONTROL Existing feed]**. Markera den feed som du vill uppdatera i listan över befintliga feeds som visas och välj sedan **[!UICONTROL Next]**.

![feed-list](../images/ui/segment-match/feed-list.png)

Listan med segment visas. Härifrån kan du lägga till nya segment i din feed och du kan använda högerspåret för att ta bort segment som du inte längre behöver. När du är klar med att hantera segmenten i din feed väljer du **[!UICONTROL Next]** och följer sedan instruktionerna ovan för att slutföra den uppdaterade feeden.

![uppdatera](../images/ui/segment-match/update.png)

>[!NOTE]
>
>När du lägger till eller tar bort ett segment från en delad feed, måste den mottagande partnern bekräfta ändringen genom att aktivera alternativet [!DNL Profile] igen i sin lista över mottagna feeds.

### Acceptera en inkommande feed

Om du vill visa en inkommande feed väljer du **[!UICONTROL Received]** i sidhuvudet på [!UICONTROL Feeds]-sidan och väljer sedan den feed du vill visa från listan. Om du vill acceptera feeden väljer du **[!UICONTROL Enable for profile]** och tillåter att statusen uppdateras från [!UICONTROL Pending] till [!UICONTROL Enabled].

![receive.png](../images/ui/segment-match/received.png)

När du har accepterat en delad feed kan du börja använda delade data för att skapa nya segment.

## Nästa steg

Genom att läsa det här dokumentet har du fått en förståelse för [!DNL Segment Match], dess funktioner och hela arbetsflödet. Läs följande dokument om du vill veta mer om andra plattformstjänster:

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] översikt](../../profile/home.md)
