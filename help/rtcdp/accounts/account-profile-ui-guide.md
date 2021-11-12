---
keywords: rtcdp-profil;profiler rtcdp;rtcdp-identiteter;rtcdp-sammanslagningsprinciper;kundprofil i realtid
title: Användargränssnittshandbok för kontoprofil
description: Genom att använda kontoprofiler kan du använda Real-time Customer Data Platform B2B Edition för att samla kontoinformation från flera olika källor. Den här guiden innehåller information om hur du interagerar med kontoprofiler i Adobe Experience Platform användargränssnitt.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: f4ca1efe9c728f50008d7fbaa17aa009dfc18393
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Användargränssnittshandbok för kontoprofil

>[!NOTE]
>
>Kontoprofiler är bara tillgängliga för Real-time Customer Data Platform B2B Edition-kunder. Om du vill veta mer om CDP i realtid, inklusive de funktioner och funktioner som är tillgängliga för varje licenstyp, kan du börja med att läsa [CDP-översikt i realtid](../overview.md).

Med kontoprofiler kan du samla kontoinformation från flera olika källor. Denna enhetliga vy av ett konto sammanför data från alla era marknadsföringskanaler och de olika system som organisationen för närvarande använder för att lagra kundkontoinformation. Det här dokumentet innehåller en guide till interaktion med kontoprofiler med hjälp av realtidsfunktionerna för CDP, B2B Edition i Adobe Experience Platform användargränssnitt.

## Bläddra bland kontoprofiler

Bläddra bland kontoprofiler genom att börja med att välja **[!UICONTROL Profiles]** under [!UICONTROL Accounts] i den vänstra navigeringen.

![](images/b2b-account-browse.png)

På **[!UICONTROL Browse]** kan du utforska kontoprofiler med ett konto-ID från en ansluten företagskälla eller genom att ange källinformation direkt.

![](images/b2b-account-browse-by.png)

### Bläddra efter [!UICONTROL Connected enterprise source]

Om du vill bläddra bland kontoprofiler via en ansluten företagskälla väljer du **[!UICONTROL Connected enterprise source]** från **[!UICONTROL Browse by]** väljer du sedan en ansluten källa med väljarknappen bredvid **[!UICONTROL Source]** fält.

![](images/b2b-account-browse.png)

Då öppnas **[!UICONTROL Select source]** där du kan välja en källa baserat på de anslutningar som din organisation har upprättat.

>[!NOTE]
>
>Din organisation kan ha flera konfigurerade källor för samma tjänsteleverantör (till exempel Marketo), så det är viktigt att du granskar anslutningsnamnet, källsystemet och källsystemsinstansen för att vara säker på att du söker efter rätt källinstans.

Mer information om hur du ansluter företagskällor finns i [källöversikt](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Du kan välja en källa genom att markera alternativknappen bredvid anslutningsnamnet och sedan använda **[!UICONTROL Select]** för att gå tillbaka till [!UICONTROL Browse] -fliken.

När en källa är markerad måste du nu ange **[!UICONTROL Account ID]** relaterat till källan. Om du till exempel väljer en Salesforce-källa måste du ange ett konto-ID från Salesforce-instansen för att kunna visa den kontoprofil som är kopplad till det ID:t.

>[!NOTE]
>
>För Marketo konto-ID:n finns det två möjliga kontotabeller som du kan referera till. Därför måste du använda en specifik syntax för att se till att du visar rätt konto.
>
>Den vanligaste standardsyntaxen är det konto-ID för Marketo som läggs till av `.mkto_org` (t.ex. `1234567.mkto_org`). Marketo kontobaserade marknadsföringskunder kan ha ytterligare värden som kan hittas med det konto-ID för Marketo som finns i `.mkto_account`. Kontakta Marketo-administratören om du är osäker på vilken syntax du ska använda.

![](images/b2b-account-browse-id.png)

### Bläddra efter [!UICONTROL Others]

I realtid stöder CDP, B2B Edition möjligheten att utföra en direktsökning genom att du kan ange en **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** och **[!UICONTROL Account ID]** för ett konto som du vill visa. Genom att ange källnamnet och instansen direkt anger du det sammanhang som krävs för att Experience Platform ska kunna söka efter och visa korrekta kontoprofildata.

Möjligheten att utföra en direktsökning är användbar under omständigheter då det inte går att ansluta direkt till data från en källa. Om din organisation till exempel har befintliga datastyrningsprinciper som förhindrar direktanslutning till CRM kan du exportera dessa data till ett molnlagringssystem och sedan importera dem till Experience Platform.

Ett annat exempel kan vara att du utför en omvandling av data mellan den tidpunkt då de lämnar ett system och går in på plattformen. Du kan använda direktsökningsfunktionen för att skapa kontext för data (till exempel ange att det är Marketo-data, trots att det kommer från en Amazon S3-bucket) så att systemet vet var de ska sökas och hur de ska återges korrekt.

Välj **[!UICONTROL Others]** från **[!UICONTROL Browse by]** nedrullningsbar listruta och ange **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** och **[!UICONTROL Account ID]** för kontot som du vill visa.

![](images/b2b-account-browse-adhoc.png)

## Visa kontoprofilinformation

När du har använt **[!UICONTROL Browse]** för att hitta en kontoprofil, välja **[!UICONTROL Profile ID]** öppnar **[!UICONTROL Detail]** för kontoprofilen. Profilinformationen som visas på **[!UICONTROL Detail]** har sammanfogats från flera profilfragment till en enda vy av det enskilda kontot. Detta inkluderar kontoinformation som grundläggande attribut och data för sociala medier.

Standardfälten som visas kan också ändras på organisationsnivå för att visa de kontoprofilattribut som du föredrar.

>[!NOTE]
>
>Liknande funktioner finns för kundprofiler och en steg-för-steg-guide har skapats med instruktioner för att lägga till och ta bort attribut, ändra storlek på paneler osv. Läs [guide för anpassning av profildetaljer](../../profile/ui/profile-customization.md) om du vill veta mer.

![](images/b2b-account-details.png)

Du kan visa ytterligare information om kontot genom att välja en annan av de tillgängliga flikarna. Flikarna innehåller attribut, personer och fliken för affärsmöjligheter som visar öppna och stängda möjligheter som är kopplade till kontot i företagets system. Mer information om varje flik finns i följande avsnitt.

## Fliken Attribut

The **[!UICONTROL Attributes]** På -fliken visas all postinformation som hör till kontot. Detta inkluderar attributdata från flera källor som har sammanfogats till en enda vy av kontot.

Förutom att du kan visa data i en lista kan du använda sökfältet för att söka efter specifika attribut eller visa postdata som JSON.

![](images/b2b-account-attributes.png)

## Fliken Personer

The **[!UICONTROL People]** -fliken innehåller en lista med enskilda personer som är kopplade till kontot. Dessa personer kan vara kontakter och leads från olika företagssystem som hanteras av olika team inom organisationen, men i realtid visas CDP, B2B Edition som en enda lista som gör att du kan få en mer helhetsbild av dina kontokontakter.

>[!NOTE]
>
>The [!UICONTROL People] På -fliken visas en lista med upp till 25 personer som är associerade med kontot. För konton med fler än 25 associerade personer visas ett slumpmässigt urval på 25 poster.

Förutom att visa dig en ögonblicksbild av information för kontakten, innehåller varje person i listan även en **[!UICONTROL Profile ID]**, som är en klickbar länk som gör att du kan utforska kundprofilen i realtid för den personen. Läs mer om hur du visar enskilda kundprofiler för dina konton i guiden [webbläsarprofiler i realtid med CDP, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Fliken Affärsmöjligheter

The **[!UICONTROL Opportunities]** -fliken innehåller information om öppna och stängda affärsmöjligheter som är relaterade till kontot. Dessa möjligheter kan förtäras i Experience Platform från flera olika källor, men CDP, B2B Edition i realtid gör det enkelt för marknadsförarna att se alla dessa möjligheter på ett och samma ställe.

>[!NOTE]
>
>The [!UICONTROL Opportunities] På -fliken visas en lista med upp till 25 affärsmöjligheter som är associerade med kontot. För konton med fler än 25 tillhörande möjligheter visas ett slumpmässigt urval på 25 poster.

Varje affärsmöjlighet innehåller information som namn på affärsmöjligheten, belopp, fas och huruvida affärsmöjligheten är öppen, stängd, vunnen eller förlorad.

![](images/b2b-account-opportunities.png)
