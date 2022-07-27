---
keywords: rtcdp-profil;profiler rtcdp;rtcdp-identiteter;rtcdp-sammanslagningsprinciper;kundprofil i realtid
title: Användargränssnittshandbok för kontoprofil
description: Genom att använda kontoprofiler kan du använda Real-time Customer Data Platform B2B Edition för att samla kontoinformation från flera olika källor. Den här guiden innehåller information om hur du interagerar med kontoprofiler i Adobe Experience Platform användargränssnitt.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 9963c78bff8d48816982bc79af9239f1a7b5e90a
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Användargränssnittshandbok för kontoprofil

>[!NOTE]
>
>Kontoprofiler är bara tillgängliga för Real-time Customer Data Platform B2B Edition-kunder. Om du vill veta mer om CDP i realtid, inklusive de funktioner och funktioner som är tillgängliga för varje licenstyp, kan du börja med att läsa [CDP-översikt i realtid](../overview.md).

Med kontoprofiler kan du samla kontoinformation från flera olika källor. Denna enhetliga vy av ett konto sammanför data från alla era marknadsföringskanaler och de olika system som organisationen för närvarande använder för att lagra kundkontoinformation. Det här dokumentet innehåller en guide till interaktion med kontoprofiler med hjälp av realtidsfunktionerna för CDP, B2B Edition i Adobe Experience Platform användargränssnitt.

Mer information om hur kontoprofiler skapas som en del av B2B-arbetsflödet finns i [självstudiekurs från början till slut](../b2b-tutorial.md).

## Översikt över kontoprofiler {#account-profiles-overview}

Börja med att välja en kontoprofilöversikt **[!UICONTROL Profiles]** under [!UICONTROL Accounts] i den vänstra navigeringen. Under [!UICONTROL Overview] visas en bild eller ett diagram på kontrollpanelen med widgetar på en enda startpunkt.

![Fliken Översikt](images/b2b-account-profile-overview.png)

Mer information om kontrollpanelen för kontoprofiler finns i [Kontrollpanel för kontoprofiler](../../dashboards/guides/account-profiles.md) dokumentation.

## Bläddra bland kontoprofiler {#browse-account-profiles}

Bläddra bland kontoprofiler genom att börja med att välja **[!UICONTROL Profiles]** under [!UICONTROL Accounts] i den vänstra navigeringen.

![Välj profiler i den vänstra navigeringen](images/b2b-account-browse.png)

På **[!UICONTROL Browse]** kan du utforska kontoprofiler med ett konto-ID från en ansluten företagskälla eller genom att ange källinformation direkt.

![Använd konto-ID för att utforska profiler](images/b2b-account-browse-by.png)

### Bläddra efter [!UICONTROL Connected enterprise source] {#browse-by-connected-enterprise-source}

Om du vill bläddra bland kontoprofiler via en ansluten företagskälla väljer du **[!UICONTROL Connected enterprise source]** från **[!UICONTROL Browse by]** väljer du sedan en ansluten källa med väljarknappen bredvid **[!UICONTROL Source]** fält.

![Bläddra bland kontoprofiler efter ansluten företagskälla](images/b2b-account-browse.png)

Då öppnas **[!UICONTROL Select source]** där du kan välja en källa baserat på de anslutningar som din organisation har upprättat.

>[!NOTE]
>
>Din organisation kan ha flera konfigurerade källor för samma tjänsteleverantör (till exempel Marketo), så det är viktigt att du granskar anslutningsnamnet, källsystemet och källsystemsinstansen för att vara säker på att du söker efter rätt källinstans.

Mer information om hur du ansluter företagskällor finns i [källöversikt](../sources/sources-overview.md).

![Välj källarbetsflöde](images/b2b-account-select-source.png)

Du kan välja en källa genom att markera alternativknappen bredvid anslutningsnamnet och sedan använda **[!UICONTROL Select]** för att gå tillbaka till [!UICONTROL Browse] -fliken.

När en källa är markerad måste du nu ange **[!UICONTROL Account ID]** relaterat till källan. Om du till exempel väljer en Salesforce-källa måste du ange ett konto-ID från Salesforce-instansen för att kunna visa den kontoprofil som är kopplad till det ID:t.

>[!NOTE]
>
>För Marketo konto-ID:n finns det två möjliga kontotabeller som du kan referera till. Därför måste du använda en specifik syntax för att se till att du visar rätt konto.
>
>Den vanligaste standardsyntaxen är det konto-ID för Marketo som läggs till av `.mkto_org` (t.ex. `1234567.mkto_org`). Marketo Account-Based Marketing-kunder kan ha ytterligare värden som kan hittas med Marketo konto-ID som bifogas av `.mkto_account`. Kontakta Marketo-administratören om du är osäker på vilken syntax du ska använda.

![Val av konto-ID](images/b2b-account-browse-id.png)

### Bläddra efter [!UICONTROL Others] {#browse-by-others}

I realtid stöder CDP, B2B Edition möjligheten att utföra en direktsökning genom att du kan ange en **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** och **[!UICONTROL Account ID]** för ett konto som du vill visa. Genom att ange källnamnet och instansen direkt anger du det sammanhang som krävs för att Experience Platform ska kunna söka efter och visa korrekta kontoprofildata.

Möjligheten att utföra en direktsökning är användbar under omständigheter då det inte går att ansluta direkt till data från en källa. Om din organisation till exempel har befintliga datastyrningsprinciper som förhindrar direktanslutning till CRM kan du exportera dessa data till ett molnlagringssystem och sedan importera dem till Experience Platform.

Ett annat exempel kan vara att du utför en omvandling av data mellan den tidpunkt då de lämnar ett system och går in på plattformen. Du kan använda direktsökningsfunktionen för att skapa kontext för data (till exempel ange att det är Marketo-data, trots att det kommer från en Amazon S3-bucket) så att systemet vet var de ska sökas och hur de ska återges korrekt.

Välj **[!UICONTROL Others]** från **[!UICONTROL Browse by]** nedrullningsbar listruta och ange **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** och **[!UICONTROL Account ID]** för kontot som du vill visa.

![Bläddra bland andra](images/b2b-account-browse-adhoc.png)

## Visa kontoprofilinformation {#view-account-profile-details}

När du har använt **[!UICONTROL Browse]** för att hitta en kontoprofil, välja **[!UICONTROL Profile ID]** öppnar **[!UICONTROL Detail]** för kontoprofilen. Profilinformationen som visas på **[!UICONTROL Detail]** har sammanfogats från flera profilfragment till en enda vy av det enskilda kontot. Detta inkluderar kontoinformation som grundläggande attribut och data för sociala medier.

Standardfälten som visas kan också ändras på organisationsnivå för att visa de kontoprofilattribut som du föredrar.

>[!NOTE]
>
>Liknande funktioner finns för kundprofiler och en steg-för-steg-guide har skapats med instruktioner för att lägga till och ta bort attribut, ändra storlek på paneler osv. Läs [guide för anpassning av profildetaljer](../../profile/ui/profile-customization.md) om du vill veta mer.

![Visa kontoprofilinformation](images/b2b-account-details.png)

Du kan visa ytterligare information om kontot genom att välja en annan av de tillgängliga flikarna. Flikarna innehåller attribut, personer och fliken för affärsmöjligheter som visar öppna och stängda möjligheter som är kopplade till kontot i företagets system. Mer information om varje flik finns i följande avsnitt.

## Fliken Attribut {#attributes-tab}

The **[!UICONTROL Attributes]** På -fliken visas all postinformation som hör till kontot. Detta inkluderar attributdata från flera källor som har sammanfogats till en enda vy av kontot.

Förutom att du kan visa data i en lista kan du använda sökfältet för att söka efter specifika attribut eller visa postdata som JSON.

![Fliken Attribut](images/b2b-account-attributes.png)

## Fliken Personer {#people-tab}

The **[!UICONTROL People]** -fliken innehåller en lista med enskilda personer som är kopplade till kontot. Dessa personer kan vara kontakter och leads från olika företagssystem som hanteras av olika team inom organisationen, men i realtid visas CDP, B2B Edition som en enda lista som gör att du kan få en mer helhetsbild av dina kontokontakter.

>[!NOTE]
>
>The [!UICONTROL People] På -fliken visas en lista med upp till 25 personer som är associerade med kontot. För konton med fler än 25 associerade personer visas ett slumpmässigt urval på 25 poster.

Förutom att visa dig en ögonblicksbild av information för kontakten, innehåller varje person i listan även en **[!UICONTROL Profile ID]**, som är en klickbar länk som gör att du kan utforska kundprofilen i realtid för den personen. Läs mer om hur du visar enskilda kundprofiler för dina konton i guiden [webbläsarprofiler i realtid med CDP, B2B Edition](../profile/profile-browse.md).

![Fliken Personer](images/b2b-account-people.png)

## Fliken Affärsmöjligheter {#opportunities-tab}

The **[!UICONTROL Opportunities]** -fliken innehåller information om öppna och stängda affärsmöjligheter som är relaterade till kontot. Dessa möjligheter kan förtäras i Experience Platform från flera olika källor, men CDP, B2B Edition i realtid gör det enkelt för marknadsförarna att se alla dessa möjligheter på ett och samma ställe.

>[!NOTE]
>
>The [!UICONTROL Opportunities] På -fliken visas en lista med upp till 25 affärsmöjligheter som är associerade med kontot. För konton med fler än 25 tillhörande möjligheter visas ett slumpmässigt urval på 25 poster.

Varje affärsmöjlighet innehåller information som namn på affärsmöjligheten, belopp, fas och huruvida affärsmöjligheten är öppen, stängd, vunnen eller förlorad.

![Fliken Kontomöjligheter](images/b2b-account-opportunities.png)

## Fliken Relaterade konton {#related-accounts-tab}

The **[!UICONTROL Related accounts]** -fliken innehåller information om andra konton som kan vara relaterade till det konto du bläddrar i. Mer information om funktionerna finns i [översikt över relaterade konton](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* En relaterad kontogrupp kan ha maximalt 30 kontoprofiler. Om fler än 30 kontoprofiler befunnits vara relaterade delas de godtyckligt i flera grupper, där var och en inte har fler än 30 medlemmar. Gruppen Relaterade konton i en kontoprofil omfattar alltid sig själv.
>* The [!UICONTROL Related accounts] På -fliken visas för närvarande en lista med upp till 25 relaterade konton som är kopplade till kontot som du bläddrar i. Detta är en begränsning som kommer att åtgärdas i en framtida uppdatering. Trots den här gränssnittsbegränsningen används alla profiler för målgruppsanpassning när du använder relaterade konton i segmentdefinitioner för grupper med 30 relaterade kontoprofiler.


Varje relaterat konto innehåller information om t.ex. kontoprofils-ID och namn, kontokällnyckeln och ytterligare information om hemsida, adress, överordnat konto, telefon, bransch och årsomsättning.

![Fliken Relaterade konton](images/b2b-account-related-accounts.png)

Du kan använda relaterade konton i den här listan för segmenteringsändamål. Se en [segmenteringsexempel](/help/rtcdp/segmentation/b2b.md#related-account) för att förstå hur du använder relaterade konton för att utöka räckvidden i segmentdefinitioner.