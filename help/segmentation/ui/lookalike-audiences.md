---
solution: Experience Platform
title: Look-Alike Audiences
description: Lär dig målinrikta nya värdefulla målgrupper i Adobe Experience Platform med lookalike-målgrupper.
badgeLimitedAvailability: label="Begränsad tillgänglighet" type=Caution
hide: true
hidefromtoc: true
source-git-commit: d0b839dfc35ff9f8b4db34c61d2cdd820bfd448b
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 0%

---


# Look-Alike Audiences guide

>[!IMPORTANT]
>
>Observera att lookalike-insikter och lookalike-målgrupper finns i **begränsad tillgänglighet**.

I Adobe Experience Platform ger lookalike-målgrupper intelligenta insikter om var och en av era målgrupper och utnyttjar maskininlärningsbaserade insikter för att identifiera och inrikta sig på värdefulla kunder med era marknadsföringskampanjer.

Med Look-Alike Audiences kan ni skapa expanderade målgrupper som riktar sig till kunder som liknar era högpresterande målgrupper eller målgrupper som liknar de tidigare konverterade målgrupperna.

## Terminologi {#terminology}

Innan du börjar med stilliknande målgrupper måste du förstå följande koncept:

- **Basera målgrupp**: Baskåpubliken är den målgrupp som du vill få mer information om. Det är den målgrupp som lookalike-modellen är **baserad** på.
- **Look-alike model**: En look-alike-modell är en maskininlärningsmodell som är utbildad på alla berättigade grundmålgrupper utan några indata från kunderna. Varje look-alike-modell skapar inflytelserika faktorer och likhetsdiagram. En lookalike-modell gör **not** få poäng.
- **Look-Alike Audience**: En Look-Alike Audience är den målgrupp som skapas när en look-alike-modell med ett valt likhetströskelvärde tillämpas på basmålgruppen. Du kan skapa flera lookalike-målgrupper med samma look-alike-modell. Den lookantliga målgruppen är det som får poäng.
- **Total adresserbar målgrupp**: Den totala adresserbara målgruppsstorleken är det totala antalet profiler under de senaste 30 dagarna minus basmålgruppspopulationen under de senaste 30 dagarna. Om en kund t.ex. har 10 miljoner profiler under de senaste 30 dagarna, och den allmänna målgruppen har 1 miljon profiler under de senaste 30 dagarna, är den totala adresserbara storleken 9 miljoner profiler.

## Liknande modellinformation {#details}

I Adobe Experience Platform förbrukar lookalike-modellen tre olika typer av datapunkter:

- Målgruppsmedlemskap de senaste 30 dagarna
- Upplev händelser under de senaste 30 dagarna som har importerats i kundprofilen i realtid
- Profilattribut under de senaste 30 dagarna som har importerats i kundprofilen i realtid

Alla dessa datapunkter omvandlas till nyckelvärdepar som matas in i lookalike-modellen. Endast nyckelvärdepar med en betydande procentandel av profilmatchningen behålls.

Den lookalike-modellen körs ofta och skapar och återskapar de inflytelserika faktorerna och likhetsgraferna för de grundläggande målgrupperna. Du kan även göra poängbedömningar för lookalike-målgrupper ofta.

## Berättiganden {#entitlements}

Följande berättiganden gäller för användning av lookalike-målgrupper:

- Real-Time CDP Prime-kunder har rätt att **5** aktiv Look-Alike Audiences i produktionssandlådor
- Real-Time CDP Ultimate-kunder har rätt till **20** aktiv Look-Alike Audiences i produktionssandlådor
- Utvecklingssandlådor är begränsade till **5** Look-Alike Audiences för alla Real-Time CDP-kunder

Det finns tilläggspaket som ökar berättigandena för produktionssandlådor med 20 Look-Alike Audiences per pack.

Om du vill bekräfta att du har tillgång till stilliknande målgrupper kontaktar du din Adobe-representant.

## Visa lookalike-insikter {#view}

Insikter som ser likadana ut är inbyggda i sidan med målgruppsinformation. Om du vill titta på lookalike-insikterna för en viss målgrupp väljer du **[!UICONTROL Audiences]** i det vänstra navigeringsfältet, följt av **[!UICONTROL Browse]** och den målgrupp ni vill visa insikterna för.

![Knappen Publiker är markerad, liksom den baspublik som används för modellering av look-alike.](../images/ui/lookalike-audiences/browse.png)

Sidan med målgruppsinformation visas. Välj **[!UICONTROL Look-alike insights]** för att visa målgruppens look-alike-insikter. Sidan **[!UICONTROL Look-alike insights]** visas. Den här sidan har tre huvudelement - likhets- och räckvidd-diagram, lookalike-målgrupper och inflytelserika faktorer.

![Fliken för lookalike-insikter är markerad och visar de utseendeliknande insikterna för den grundläggande målgruppen.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Likhet och räckvidd {#similarity-and-reach}

<!-- >[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Similarity and reach"
>abstract="" -->

Avsnittet Likhet och räckvidd visar ett diagram som ritar upp den förväntade räckvidden för en Look-Alike Audience som består av profiler över ett givet likhetspoäng. Likhetspoängen representerar **avstånd** likheter mellan basmålgruppens profil och den lookalike-liknande insiktens profil.

![Likhets- och målgrafen markeras.](../images/ui/lookalike-audiences/similarity-and-reach.png)

I det här diagrammet mäter x-axeln andelen likhet i procent mellan en profil och medlemmar i den valda publiken. Likhetspoängen varierar mellan 0 % och 100 %, med ett högre likhetspoäng som anger att en profil är närmare medlemmar i den valda publiken vad gäller värden för inflytelserika faktorer.

På y-axeln visas det förväntade antalet profiler med den likhet i procent som motsvarar det matchande värdet för x-axeln. Det förväntade antalet profiler varierar mellan 0 och den totala adresserbara målgruppen eller 25 miljoner profiler, beroende på vilken som är lägst. Denna axel mäts på en **logaritmisk skala** för att förbättra diagrammets läsbarhet.

Observera att diagrammet **kumulativ** från höger till vänster. Det innebär att värdet för y-axeln vid varje punkt i diagrammet är antalet profiler som har en likhet **ovan** likhetströskeln. Om x-axeln till exempel är 60 % och y-axeln är 10 miljoner innebär det att det finns 10 miljoner profiler som är lika med eller mer än 60 % jämfört med baspubliken.

Du kan hålla pekaren över en viss punkt i diagrammet om du vill visa procentandelen likhet och det förväntade antalet profiler för den markerade punkten.

### Look-Alike Audiences {#list}

I avsnittet lookalike-målgrupper visas en lista med alla Look-Alike Audiences som tidigare har skapats för den valda basmålgruppen.

![Avsnittet om lookalike-målgrupper är markerat.](../images/ui/lookalike-audiences/select-laa.png)

### Influensafaktorer {#influential-factors}

<!-- >[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Influential factors"
>abstract="Influential factors are attributes, events and audience memberships that are important in explaining similarity of a profile to members of the base audience. Data usage labels and policies can be used to exclude certain data from being considered as influential factors in look-alike models."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=en#exclude" text="Exclude data" -->

I avsnittet Inflytelserika faktorer visas de 100 viktigaste faktorerna som påverkar den look-alike-modellen för den valda baspubliken. Dessa inflytelserika faktorer är profilattribut, upplevelsehändelser och målgruppsmedlemskap som är de viktigaste när det gäller att förklara likheter hos den grundläggande målgruppen. Genom att förstå de viktigaste inflytelserika faktorerna kan ni personalisera ert marknadsföringsinnehåll bättre för den här målgruppen och alla lookAlike Audience ni skapar utifrån den. Observera att inte alla inflytelserika faktorer som påverkar lookalike-modellen visas.

För numeriska faktorer kan nyckelvärdepar placeras i grupper, beroende på hur många olika värden nyckeln har. Om du t.ex. har en tangent på `income`, det finns troligen många unika värden. Därför placeras nyckelvärdepar i grupper som kan se ut som `income=[0 -> 30000]`, `income=[30000 -> 50000]`och `income=[50000 -> 100000]`.

Dessa luckor beräknas regelbundet om för att säkerställa att data hålls aktuella.

![Avsnittet om inflytelserika faktorer är markerat.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Influensafaktorerna sorteras efter prioritet och är oberoende av varandra.

| Fält | Beskrivning |
| ----- | ----------- |
| Typ | Den typ av data som den inflytelserika faktorn härleds från. Detta kan vara ett profilattribut, en upplevelsehändelse eller ett målgruppsmedlemskap. |
| Nyckel | Datafältets namn. För nycklar av typen målgruppsmedlemskap representerar det här värdet **namespace** för den målgrupp som data kommer från. Möjliga värden är `ups` (Segmenteringstjänst) och `AO` (Målgruppssamordning). För nycklar av andra typer representerar det här värdet sökvägen till XDM-fältet. Om företaget Luma t.ex. har ett anpassat fält som kallas inkomst blir nyckeln `_luma.income` |
| Värde | Värdet varierar beroende på vilken inflytelserik faktor det representerar. För profilattribut eller upplevelsehändelser representerar det här fältet värdet eller värdeintervallet för datafältet som anger likheten med medlemmarna i basmålgruppen. Värdeintervallet skrivs i formuläret `[A -> B]`, där `A` representerar det nedre intervallet medan `B` representerar det högre intervallet. För målgruppsmedlemskap är det här fältet namnet på målgruppen. |
| Viktighetsgrad | Den inflytelserika faktorens relativa betydelse. Detta kan vara högt, medelstort eller lågt. |

## Skapa en lookalike-målgrupp {#create}

>[!IMPORTANT]
>
>Du **inte** Använd en Look-Alike Audience som baspublik för en annan Look-Alike Audience. Det vill säga er **inte** skapa kedjade stilliknande målgrupper.

Om du vill skapa en Look-Alike Audience måste du välja den målgrupp du vill basera den Look-Alike Audience på. Om du vill visa en lista över tillgängliga målgrupper väljer du **[!UICONTROL Audiences]** i det vänstra navigeringsfältet, följt av **[!UICONTROL Browse]**. Listan över målgrupper visas. På den här sidan kan du välja den målgrupp som du vill använda som din grundmålgrupp.

![Knappen Publiker är markerad, liksom den baspublik som används för modellering av look-alike.](../images/ui/lookalike-audiences/browse.png)

På sidan med målgruppsinformation väljer du **[!UICONTROL Create look-alike audience]** för att börja skapa en Look-Alike Audience.

![The [!UICONTROL Create look-alike audience] knappen är markerad.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

The **[!UICONTROL Create a look-alike audience]** popover visas. På den här sidan kan du ange procentandelen för likhet för den lookalike-målgruppen.

![The [!UICONTROL Create a look-alike audience] popover visas.](../images/ui/lookalike-audiences/create-audience.png)

Du kan ange den här procentandelen för likhet på tre olika sätt:

- Flytta reglaget för att ange procentandelen för likhet
- Ange procentvärdet för likhet i den numeriska postrutan bredvid skjutreglaget
- Håll pekaren över diagrammet och välj önskad plats för att ange procentandelen för likhet

Du kan även uppdatera information om den lookalike-målgruppen, inklusive dess namn och beskrivning. Som standard genereras namnet på en Look-Alike Audience baserat på den ursprungliga målgruppens namn och det procenttal för likhet som tidigare angetts.

![Den grundläggande informationen markeras i [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/basic-info.png)

Välj **[!UICONTROL Create]** för att slutföra skapandet av en lookalike-målgrupp.

![Skapa-knappen är markerad i [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/create-audience.png)

Den nya Look-Alike Audience finns i **[!UICONTROL Look-alike audiences]** på sidan med målgruppsinformation. Den finns även i Audience Portal och för annan nedladdning. Observera att det kommer att ta en stund innan ni kan göra en jakt på den lookalike-målgruppen. Profilantalet blir 0 tills det poängsätts.

## Visa lookalike-målgruppsinformation {#view-details}

Om du vill visa information om en Look-Alike Audience väljer du Look-Alike Audience i **[!UICONTROL Look-Alike Audiences]** -delen av den grundläggande målgruppen.

![Avsnittet om lookalike-målgrupper är markerat.](../images/ui/lookalike-audiences/select-laa.png)

Sidan med målgruppsinformation visas. Mer information finns i [målgruppsdelen i gränssnittsguiden för segmenteringstjänsten](./overview.md#audience-details).

![Detaljer om en Look-Alike Audience visas.](../images/ui/lookalike-audiences/laa-details.png)

## Uteslut datafält från look-alike-modellering {#exclude}

Look-Alike Audiences kan konfigureras för att exkludera datafält som är begränsade för marknadsföringsåtgärden &quot;Data Science&quot; genom att använda relevanta etiketter och policyer för dataanvändning. Data som är märkta som begränsade från användning för datavetenskap kommer att tas bort från övervägandet vid utbildning av en Look-Alike Audience-modell och vid generering av en Look-Alike Audience från den utbildade modellen. 

Standardetiketten&quot;C9&quot; kan användas för att märka data som inte ska användas för datavetenskap och kan användas genom att aktivera standardprincipen&quot;Begränsa datavetenskap&quot;. Du kan också skapa ytterligare profiler för att begränsa data med andra etiketter, inklusive känsliga etiketter, från användning för datavetenskap. Mer information om hur du hanterar regler för dataanvändning finns i [användargränssnittshandbok för dataanvändningsprinciper](../../data-governance/policies/user-guide.md). Mer information om hur du hanterar etiketter för dataanvändning finns i [användargränssnittshandbok för dataanvändningsetiketter](../../data-governance/labels/user-guide.md).

Som standard exkluderas modelleringsprocessen för lookalike-målgrupper **alla** fält, datauppsättning eller målgrupp baserat på den integritetspolicy som är aktiverad för din organisation. Om baspubliken inte har några kontraktsetiketter utesluter modelleringsprocessen **alla** fält, datauppsättning eller målgrupp baserat på den integritetspolicy som är aktiverad för din organisation.

Observera att **dig** ansvarar för att säkerställa att data, inklusive känsliga data, märks på rätt sätt och att dataanvändningspolicyer har definierats och möjliggjorts för att uppfylla de rättsliga och lagstadgade skyldigheter som ni tillämpar. Du bör också vara medveten om att datafält eller segmentmedlemskap som **not** direkt korrelerad med datafält som vanligtvis är kopplade till känsliga eller skyddade datatyper kan vara en källa till potentiella avvikelser. **Du** är ansvariga för att analysera data för att identifiera, märka och tillämpa lämpliga dataanvändningsregler för data, inklusive eventuella datafält som kan användas som proxy för känsliga eller skyddade datatyper och som bör undantas från modellering.

## Nästa steg

När du har läst den här guiden har du lärt dig att se lookalike-insikter och skapa Look-Alike Audiences baserat på dessa insikter. Mer information om målgrupper i Adobe Experience Platform finns i [Användargränssnittsguide för segmenteringstjänst](./overview.md).
