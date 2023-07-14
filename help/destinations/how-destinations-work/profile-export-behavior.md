---
title: Beteende vid export av profiler
description: Lär dig hur beteendet vid export av profiler varierar mellan de olika integreringsmönster som stöds i Experience Platform-mål.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 0%

---

# Profilexportbeteende för olika måltyper

Det finns flera destinationstyper i Experience Platform, vilket visas i diagrammet nedan. Dessa destinationer har något annorlunda exportmönster vad gäller vilka som utlöser en destinationsexport och vad som ingår i en export, vilket beskrivs i avsnitten längre fram nedan.

>[!IMPORTANT]
>
>På den här dokumentationssidan beskrivs endast hur profilexporten fungerar för de anslutningar som markeras längst ned i diagrammet.

![Diagram över destinationstyper](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Microbatching and aggregation policy

Innan man börjar gå in på specifik information per måltyp är det viktigt att förstå begreppen mikrobatchering och aggregeringspolicy för *mål för direktuppspelning*.

Experience Platform mål exporterar data till API-baserade integreringar som HTTPS-anrop. När destinationstjänsten har meddelats av andra tjänster i föregående led att profiler har uppdaterats som ett resultat av batchinmatning, direktuppspelning, batchsegmentering, direktuppspelningssegmentering eller förändringar i identitetsdiagram, exporteras data och skickas till direktuppspelningsdestinationer.

Den process som används för att samla profiler i HTTPS-meddelanden innan de skickas till mål-API-slutpunkter anropas *mikrobatchbearbetning*.

Ta [Facebook](/help/destinations/catalog/social/facebook.md) med *[konfigurerbar aggregering](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* som exempel - data skickas på ett aggregerat sätt, där destinationstjänsten tar alla inkommande data från profiltjänsten uppströms och samlar in dem med något av följande, innan de skickas till Facebook:

* Antal poster (högst 10 000) eller
* Tidsfönsterintervall (30 minuter)

Vilken tröskel som helst som uppnås först utlöser en export till Facebook. Så i [!DNL Facebook Custom Audiences] på kontrollpanelen kan ni se målgrupper som kommer från Experience Platform i 10 000 rekordsteg. Du kanske ser 10 000 poster var 10-15:e minut eftersom data bearbetas och slås samman snabbare än 30 minuters exportintervall och skickas snabbare, så ungefär var 10-15:e minut tills alla poster har bearbetats. Om det inte finns tillräckligt med poster för att kunna skapa en 10 000-sats, skickas det aktuella antalet poster som det är när tidsfönstrets tröskelvärde uppnås, så du kan se även mindre grupper skickade till Facebook.

Som ett annat exempel kan du titta på [HTTP API-mål](/help/destinations/catalog/streaming/http-destination.md), som har *[bästa ansträngningsaggregering](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* profil, med `maxUsersPerRequest: 10`. Detta innebär att högst tio profiler slås samman innan ett HTTP-anrop utlöses till det här målet, men Experience Platform försöker skicka profiler till målet så fort som måltjänsten får uppdaterad information om omvärdering från en tjänst i det övre flödet.

Aggingsprincipen kan konfigureras och målutvecklare kan bestämma hur aggregeringsprincipen ska konfigureras så att den bäst uppfyller hastighetsbegränsningarna för API-slutpunkterna längre fram i kedjan. Läs mer om [aggregeringsprincip](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) i Destinationens SDK dokumentation.

## Exportmål för direktuppspelningsprofil (företag) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Företagsmål är bara tillgängliga för [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder.

The [företagsmål](/help/destinations/destination-types.md#streaming-profile-export) i Experience Platform är Amazon Kinesis, Azure Event Hubs och HTTP API.

Experience Platform optimerar beteendet för profilexport till företagets mål, så att endast data exporteras till API-slutpunkten när relevanta uppdateringar av en profil har gjorts efter målgruppskvalifikation eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen bestäms av en ändring i [målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) för minst en av de målgrupper som är mappade till målet. Profilen har till exempel kvalificerats för en av de målgrupper som är mappade till målet eller har avslutat en av de målgrupper som är mappade till målet.
* Profiluppdateringen bestäms av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för en av de målgrupper som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen bestäms av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om en målgrupp som mappats till målflödet till exempel har hundra medlemmar och fem nya profiler kvalificerar sig för segmentet, kommer exporten till målplatsen att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

### Vad avgör en dataexport och vad som ingår i exporten

När det gäller data som exporteras för en viss profil är det viktigt att förstå de två olika begreppen i *vad som avgör dataexport till ditt företags mål* och *vilka data som inkluderas i exporten*.

| Vad avgör en målexport | Vad som ingår i målexporten |
|---------|----------|
| <ul><li>Kopplade attribut och målgrupper fungerar som referens för en målexport. Det innebär att om någon mappad publik ändrar tillstånd (från `null` till `realized` eller från `realized` till `exiting`) eller om mappade attribut uppdateras, kommer en målexport att startas.</li><li>Eftersom identiteter för närvarande inte kan mappas till företagsmål, bestäms även målexporter av ändringar i identiteter i en viss profil.</li><li>En ändring för ett attribut definieras som en uppdatering för attributet, oavsett om det är samma värde eller inte. Det innebär att en överskrivning av ett attribut betraktas som en ändring även om värdet i sig inte har ändrats.</li></ul> | <ul><li>The `segmentMembership` -objektet innehåller den målgrupp som mappas i aktiveringsdataflödet, för vilket profilens status har ändrats efter en kvalificerings- eller målgruppsavslutningshändelse. Observera att andra omappade målgrupper som profilen är kvalificerad för kan ingå i målexporten om dessa målgrupper tillhör samma [sammanfogningsprincip](/help/profile/merge-policies/overview.md) som målgruppen mappas i aktiveringsdataflödet. </li><li>Alla identiteter i `identityMap` -objekt ingår också (Experience Platform stöder för närvarande inte identitetsmappning i företagsmålet).</li><li>Endast mappade attribut inkluderas i målexporten.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Enterprise-destinationer strömmar data om bakåtfyllnad när profiler aktiveras till ett mål. Detta innebär att den första dataexporten efter att ha konfigurerat ett aktiveringsarbetsflöde till ett mål kommer att innehålla profiler som är kvalificerade för den aktiverade målgruppen innan målgruppen mappas till målet.

>[!BEGINSHADEBOX]

Tänk dig till exempel det här dataflödet till ett HTTP-mål där tre målgrupper har valts i dataflödet och fyra attribut mappas till målet.

![företagsmåldataflöde](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

En profilexport till målet kan bestämmas av en profil som kvalificerar för eller avslutar en av *tre mappade segment*. I dataexporten kan du dock `segmentMembership` kan andra omappade målgrupper visas om den aktuella profilen är medlem av dem och om dessa delar samma sammanfogningsprincip som den målgrupp som utlöste exporten. Om en profil kvalificerar sig för **Kund med DeLorean Cars** , men är även medlem i **Bevakade filmen&quot;Tillbaka till framtiden&quot;** och **Science fiction fans** segment, så kommer dessa två andra målgrupper också att vara närvarande i `segmentMembership` dataexportens objekt, även om dessa inte är mappade i dataflödet, om dessa delar samma sammanfogningsprincip med **Kund med DeLorean Cars** segment.

När det gäller profilattribut kommer alla ändringar av de fyra attribut som mappas ovan att avgöra målexporten och alla de fyra mappade attributen som finns i profilen kommer att finnas i dataexporten.

>[!ENDSHADEBOX]

>[!TIP]
>
> Du kan se exempel på exporterade data till olika företagsmål i [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)och [HTTP-API](/help/destinations/catalog/streaming/http-destination.md#exported-data) dokumentationssidor för mål.

## API-baserade mål för direktuppspelning {#streaming-api-based-destinations}

Profilexportbeteendet för direktuppspelningsmål som Facebook, Trade Desk och andra API-baserade integreringar liknar beteendet som beskrivs ovan för företagsmål.

Exempel på direktuppspelningsdestinationer är de destinationer som tillhör [kategorier för sociala medier och reklam](/help/destinations/destination-types.md#categories) i katalogen.

Experience Platform optimerar beteendet för profilexport till ditt mål för direktuppspelning, så att endast data exporteras till API-baserade mål för direktuppspelning när relevanta uppdateringar av en profil har gjorts efter målgruppskvalifikation eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen bestäms av en ändring i [målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) för minst en av de målgrupper som är mappade till målet. Profilen har till exempel kvalificerats för en av de målgrupper som är mappade till målet eller har avslutat en av de målgrupper som är mappade till målet.
* Profiluppdateringen bestäms av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md) för ett identitetsnamnutrymme som har markerats för export för den här destinationsinstansen. En profil som redan är kvalificerad för en av de målgrupper som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen bestäms av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.
* Godkännandeändringar för en profil när automatisk tillämpning av medgivande har konfigurerats och en profil avanmäler sig. Automatiserad indrivning av samtycke skickar en målgruppshändelse till destinationen så att profilen inte inkluderas i någon målgruppsanpassning på destinationen.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om en målgrupp som mappats till målflödet till exempel har hundra medlemmar och fem nya profiler kvalificerar sig för segmentet, kommer exporten till målplatsen att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

### Vad avgör en dataexport och vad som ingår i exporten

När det gäller data som exporteras för en viss profil är det viktigt att förstå de två olika begreppen för vad som bestämmer en dataexport till API-målet för direktuppspelning och vilka data som inkluderas i exporten.

| Vad avgör en målexport | Vad som ingår i målexporten |
|---------|----------|
| <ul><li>Kopplade attribut och målgrupper fungerar som referens för en målexport. Det innebär att om någon mappad publik ändrar tillstånd (från `null` till `realized` eller från `realized` till `exiting`) eller om mappade attribut uppdateras, kommer en målexport att startas.</li><li>En ändring i identitetskartan definieras som en identitet som läggs till/tas bort för [identitetsdiagram](/help/identity-service/ui/identity-graph-viewer.md) för profilen, för identitetsnamnutrymmen som mappas för export.</li><li>En ändring för ett attribut definieras som en uppdatering för attributet, för attribut som mappas till målet.</li></ul> | <ul><li>De målgrupper som är mappade till målet och har ändrats inkluderas i `segmentMembership` -objekt. I vissa fall kan de exporteras med flera anrop. I vissa scenarier kan även vissa målgrupper som inte har ändrats inkluderas i samtalet. I vilket fall som helst exporteras bara mappade målgrupper.</li><li>Alla identiteter från de namnutrymmen som är mappade till målet i `identityMap` -objekt tas också med.</li><li>Endast mappade attribut inkluderas i målexporten.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>API-destinationer för direktuppspelning strömmar data för bakåtfyllnad när profiler aktiveras till ett mål. Detta innebär att den första dataexporten efter att ha konfigurerat ett aktiveringsarbetsflöde till ett mål kommer att innehålla profiler som är kvalificerade för den aktiverade målgruppen innan målgruppen mappas till målet.

>[!BEGINSHADEBOX]

Ta till exempel det här dataflödet till ett mål för direktuppspelning där tre målgrupper väljs i dataflödet.

![dataflöde för direktuppspelningsmål](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

En profilexport till målet kan bestämmas av en profil som kvalificerar för eller avslutar ett av de tre mappade segmenten. Om en profil är kvalificerad för **Kund med DeLorean Cars** -segmentet kommer att utlösa en export. Övriga målgrupper (**City - Dallas** och **Grundläggande webbplats aktiv**) kan också exporteras om profilen har den målgruppen med en av de möjliga statusvärdena (`realized` eller `exited`). Omappade målgrupper (som **Science fiction fans**) exporteras inte.

Om du ändrar något av de tre attribut som är mappade ovan för ett profilattribut bestäms en målexport.

>[!ENDSHADEBOX]

## Batchmål (filbaserade) {#file-based-destinations}

När profiler exporteras till [filbaserade mål](/help/destinations/destination-types.md#file-based) i Experience Platform finns det tre typer av scheman (som visas nedan) och två alternativ för filexport (fullständiga eller stegvisa filer) som du kan använda. Alla dessa inställningar ställs in på en målgruppsnivå, även när flera målgrupper mappas till ett enda måldataflöde.

* Schemalagd export: Konfigurera ett mål, lägg till ett eller flera segment, markera om du vill exportera fullständiga eller stegvisa filer och markera en angiven tid varje dag eller flera gånger per dag när filer ska exporteras. En 5 PM-exporttid innebär till exempel att de profiler som är kvalificerade för målgruppen kommer att exporteras kl. 17.00.
* Efter segmentutvärdering: Exporten utlöses omedelbart efter att det dagliga utvärderingsjobbet för målgruppen har körts. Det innebär att de exporterade profilnumren i filen är så nära som möjligt den senaste utvärderade populationen i segmentet.
* On demand-export ([exportera filen nu](/help/destinations/ui/export-file-now.md)): Baserat på det senaste målgruppsutvärderingsjobbet exporteras en fullständig fil en gång utöver vanlig schemalagd export.

I någon av exportsituationerna ovan innehåller de exporterade filerna de profiler som är kvalificerade för exporten, tillsammans med de kolumner som du valde som XDM-attribut för export.

>[!TIP]
>
>När en målgrupp för direktuppspelning mappas till ett gruppmål är sannolikheten större att antalet profiler i den exporterade filen är närmare antalet användare i segmentet. Det beror på att det finns en större risk att den senaste publikutvärderingen har närmar sig exporttiden.

### Inkrementell filexport {#incremental-file-exports}

Alla uppdateringar av en profil berättigar inte till att en profil inkluderas i stegvis filexport. Om till exempel ett attribut har lagts till i eller tagits bort från en profil, inkluderas inte profilen i exporten. Endast profiler som `segmentMembership` attributet har ändrats och inkluderas i exporterade filer. Det är alltså bara om profilen blir en del av publiken eller tas bort från publiken som den inkluderas i den stegvisa filexporten.

Om en ny identitet (ny e-postadress, telefonnummer, ECID o.s.v.) läggs till i en profil i [identitetsdiagram](/help/identity-service/ui/identity-graph-viewer.md), som inte representerar någon anledning att inkludera profilen i en ny stegvis filexport.

Om en ny målgrupp läggs till i en målmappning påverkar detta inte kvalifikationer och export för ett annat segment. Exportscheman konfigureras individuellt per målgrupp och filer exporteras separat för varje segment, även om målgrupperna har lagts till i samma måldataflöde.

>[!BEGINSHADEBOX]

I exportinställningen som visas nedan, där en användare exporterar stegvisa filuppdateringar, ska du tänka på följande omständigheter där en profil ingår i en stegvis filexport eller inte:

![Exportinställning med flera valda attribut.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* En profil inkluderas i en stegvis filexport när den kvalificerar eller diskvalificerar för segmentet.
* En profil är *not* ingår i en stegvis filexport när ett nytt telefonnummer läggs till i identitetsdiagrammet.
* En profil är *not* ingår i en stegvis filexport när värdet i något av de mappade XDM-fälten, som `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` uppdateras på en profil.
* När `segmentMembership.status` XDM-fältet mappas i arbetsflödet för målaktivering, profiler som avslutar målgruppen inkluderas även i exporterade inkrementella filer, med `exited` status.

>[!ENDSHADEBOX]

### Vad avgör en dataexport och vad som ingår i exporten

Baserat på informationen i avsnittet ovan kan du sammanfatta beteendet för export av profiler till filbaserade mål enligt beskrivningen nedan:

**Fullständig filexport**

Den fullständiga aktiva populationen exporteras varje dag.

| Vad avgör en målexport | Vad som ingår i den exporterade filen |
|---------|----------|
| <ul><li>Det exportschema som anges i gränssnittet eller API:t och användaråtgärden (välja [Exportera filen nu](/help/destinations/ui/export-file-now.md) i användargränssnittet eller med [ad hoc-aktiverings-API](/help/destinations/api/ad-hoc-activation-api.md)) bestämmer början på en målexport.</li></ul> | Vid fullständig filexport ingår hela den aktiva profilpopulationen i ett segment, baserat på den senaste publikutvärderingen, i varje filexport. De senaste värdena för varje XDM-attribut som valts för export inkluderas också som kolumner i varje fil. Observera att profiler med statusen Avslutad inte inkluderas i filexporten. |

{style="table-layout:fixed"}

**Inkrementell filexport**

När du har konfigurerat aktiveringsarbetsflödet exporteras hela målgruppspopulationen i den första filexporten. I efterföljande exporter exporteras bara de ändrade profilerna.

| Vad avgör en målexport | Vad som ingår i den exporterade filen |
|---------|----------|
| <ul><li>Det exportschema som anges i gränssnittet eller API avgör början på en målexport.</li><li>Om en profils målgruppsmedlemskap ändras, oavsett om det kvalificerar eller inte kvalificerar sig för segmentet, kvalificerar du en profil som ska inkluderas i den stegvisa exporten. Ändringar i attribut eller i identitetskartor för en profil *inte* kvalificera en profil som ska inkluderas i stegvis export.</li></ul> | <p>De profiler för vilka målgruppsmedlemskapet har ändrats, tillsammans med den senaste informationen för varje XDM-attribut som har valts för export.</p><p>Profiler med statusen Avslutad inkluderas i målexporter, om `segmentMembership.status` XDM-fältet väljs i mappningssteget.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Som en påminnelse kan ändringar i attributvärden eller i identitetskartor för en profil inte innebära att en profil inkluderas i en stegvis filexport.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu vad du kan förvänta dig vid export av profiler till direktuppspelnings-, företags- och filbaserade mål.

Nu kan du läsa om hur [identiteter hanteras](/help/destinations/how-destinations-work/identity-handling.md) i aktiveringsarbetsflödet.
