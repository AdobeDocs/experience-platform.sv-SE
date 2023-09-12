---
title: Konfigurera SDK-taggtillägget för webben
description: Lär dig hur du konfigurerar taggtillägget Experience Platform Web SDK i tagggränssnittet.
source-git-commit: ec0aa64c466a8228d49a776d27040253b5a1b196
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 0%

---


# Konfigurera SDK-taggtillägget för webben

The [!DNL Web SDK] taggtillägget skickar data till Adobe Experience Cloud från webbegenskaper via Experience Platform Edge-nätverket.

Tillägget gör att ni kan strömma data till plattformen, synkronisera identiteter, bearbeta kundens medgivandesignaler och automatiskt samla in kontextdata.

I det här dokumentet förklaras hur du konfigurerar taggtillägget i tagggränssnittet.

## Installera SDK-taggtillägget för webben {#install}

För Web SDK-taggtillägget krävs en egenskap som ska installeras på. Om du inte redan har gjort det läser du i dokumentationen om [skapa en taggegenskap](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

När du har skapat en egenskap öppnar du den och väljer **[!UICONTROL Extensions]** till vänster.

Klicka på fliken **[!UICONTROL Catalog]**.  I listan med tillgängliga tillägg hittar du [!DNL Web SDK] tillägg och markera **[!UICONTROL Install]**.

![Bild som visar användargränssnittet för taggar med tillägget Web SDK markerat](assets/web-sdk-install.png)

Efter markering **[!UICONTROL Install]** måste du konfigurera tillägget för Web SDK-taggen och spara konfigurationen.

>[!NOTE]
>
>Taggtillägget installeras endast efter att konfigurationen har sparats. I nästa avsnitt får du lära dig hur du konfigurerar taggtillägget.

## Konfigurera instansinställningar {#general}

Konfigurationsalternativen högst upp på sidan anger för Adobe Experience Platform var data ska skickas och vilka konfigurationer som ska användas på servern.

![Bild som visar de allmänna inställningarna för Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-general.png)

* **[!UICONTROL Name]**: Adobe Experience Platform Web SDK-tillägget stöder flera instanser på sidan. Namnet används för att skicka data till flera organisationer med en taggkonfiguration. Förekomstnamnet är som standard `alloy`. Du kan dock ändra instansnamnet till ett giltigt JavaScript-objektnamn.
* **[!UICONTROL IMS organization ID]**: ID:t för organisationen som du vill att data ska skickas till på Adobe. För det mesta använder du standardvärdet som fylls i automatiskt. När du har flera instanser på sidan fyller du i det här fältet med värdet för den andra organisationen som du vill skicka data till.
* **[!UICONTROL Edge domain]**: Domänen som tillägget skickar och tar emot data från. Adobe rekommenderar att du använder en CNAME (1st-party domain) för det här tillägget. Standarddomänen från tredje part fungerar för utvecklingsmiljöer men är inte lämplig för produktionsmiljöer. Instruktioner om hur du konfigurerar en CNAME från en förstahandsleverantör finns i listan [här](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## Konfigurera inställningar för dataström {#datastreams}

I det här avsnittet kan du välja de datastreams som ska användas för var och en av de tre tillgängliga miljöerna (produktion, mellanlagring och utveckling).

När en begäran skickas till Edge Network, används ett datastream-ID för att referera till konfigurationen på serversidan. Du kan uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

Se guiden på [datastreams](../../../../datastreams/overview.md) för att lära dig hur du konfigurerar ett datastream.

Du kan antingen välja ett datastream från de tillgängliga listrutorna eller välja **[!UICONTROL Enter values]** och ange ett anpassat datastream-ID för varje miljö.

![Bild som visar datastream-inställningarna för Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-datastreams.png)

## Konfigurera sekretessinställningar {#privacy}

I det här avsnittet kan du konfigurera hur Web SDK hanterar tillståndssignaler från din webbplats. Det gör i synnerhet att du kan välja den standardnivå för samtycke som antas av en användare om ingen annan explicit medgivandeinställning har angetts.

Standardnivån för samtycke sparas inte i användarprofilen.

![Bild som visar sekretessinställningarna för Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Default consent level] | Beskrivning |
| --- | --- |
| [!UICONTROL In] | Samla in händelser som inträffar innan användaren ger sitt samtycke. |
| [!UICONTROL Out] | Ignorera händelser som inträffar innan användaren ger sitt medgivande. |
| [!UICONTROL Pending] | Köhändelser som inträffar innan användaren ger sitt samtycke. När du har angett medgivandeinställningar kommer händelserna att samlas in eller tas bort beroende på vilka inställningar som har angetts. |
| [!UICONTROL Provided by data element] | Standardnivån för samtycke bestäms av ett separat dataelement som du definierar. När du använder det här alternativet måste du ange dataelementet med den angivna listrutan. |

>[!TIP]
>
>Använd **[!UICONTROL Out]** eller **[!UICONTROL Pending]** om du kräver uttryckligt användargodkännande för din affärsverksamhet.

## Konfigurera identitetsinställningar {#identity}

I det här avsnittet kan du definiera hur Web SDK ska fungera när det gäller hantering av användaridentifiering.

![Bild som visar identitetsinställningarna för Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrate ECID from VisitorAPI]**: Det här alternativet är aktiverat som standard. När den här funktionen är aktiverad kan SDK läsa `AMCV` och `s_ecid` cookies och ange `AMCV` cookie används av [!DNL Visitor.js]. Den här funktionen är viktig vid migrering till Web SDK, eftersom vissa sidor fortfarande använder [!DNL Visitor.js]. Med det här alternativet kan SDK fortsätta att använda samma [!DNL ECID] så att användare inte identifieras som två separata användare.
* **[!UICONTROL Use third-party cookies]**: När det här alternativet är aktiverat försöker Web SDK lagra en användaridentifierare i en cookie från tredje part. Om det lyckas identifieras användaren som en enskild användare när de navigerar mellan flera domäner, i stället för att identifieras som en separat användare på varje domän. Om det här alternativet är aktiverat kanske SDK fortfarande inte kan lagra användaridentifieraren i en tredjeparts-cookie om webbläsaren inte stöder cookies från tredje part eller har konfigurerats av användaren så att cookies från tredje part inte tillåts. I det här fallet lagrar SDK bara identifieraren i förstahandsdomänen.

## Konfigurera personaliseringsinställningar {#personalization}

I det här avsnittet kan du konfigurera hur du vill dölja vissa delar av en sida medan anpassat innehåll läses in.

Du kan ange vilka element som ska döljas i den fördolda formatredigeraren. Du kan sedan kopiera det fördolda standardfragmentet som du har fått och klistra in det inuti `<head>` element i webbplatsens [!DNL HTML] kod.

![Bild som visar anpassningsinställningarna för Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migrate Target from at.js to the Web SDK]**: Använd det här alternativet för att aktivera [!DNL Web SDK] läsa och skriva `mbox` och `mboxEdgeCluster` cookies som används av at.js `1.x` eller `2.x` bibliotek. Detta hjälper dig att behålla besökarprofilen när du går från en sida där Web SDK används till en sida där at.js används `1.x` eller `2.x` bibliotek och vice versa.

## Konfigurera inställningar för datainsamling {#data-collection}

![Bild som visar inställningarna för datainsamling i Web SDK-taggtillägget i tagggränssnittet](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Callback function]**: Återanropsfunktionen som finns i tillägget kallas också för [`onBeforeEventSend` function](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) i biblioteket. Med den här funktionen kan du ändra händelser globalt innan de skickas till Edge Network. Mer detaljerad information om hur funktionen används finns [här](../../../../edge/fundamentals/tracking-events.md#modifying-events-globally).
* **[!UICONTROL Enable click data collection]**: Web SDK kan automatiskt samla in länkklickningsinformation åt dig. Som standard är den här funktionen aktiverad men kan inaktiveras med det här alternativet. Länkarna är även märkta som nedladdningslänkar om de innehåller något av de nedladdningsuttryck som finns i [!UICONTROL Download Link Qualifier] textruta. Adobe tillhandahåller vissa standardkvalificerare för nedladdningslänk. Du kan redigera dem efter behov.
* **[!UICONTROL Automatically collected context data]**: Som standard samlar Web SDK in vissa kontextdata för enhet, webb, miljö och platskontext. Om du vill se en lista över den information som samlas in av Adobe finns den [här](../../../../edge/data-collection/automatic-information.md). Om du inte vill att dessa data ska samlas in, eller om du bara vill att vissa kategorier av data ska samlas in, väljer du **[!UICONTROL Specific context information]** och markera de data som du vill samla in.

## Konfigurera åsidosättningar av dataström {#datastream-overrides}

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK.

Detta hjälper dig att utlösa andra datastream-beteenden än standardbeteendena, utan att du behöver skapa ett nytt datastream eller ändra dina befintliga inställningar.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningar av dataströmskonfigurationer i [konfigurationssida för datastream](../../../../datastreams/configure.md).
2. Sedan måste du skicka åsidosättningarna till Edge Network antingen via ett Web SDK-kommando eller med hjälp av taggtillägget Web SDK.

Se datastream [dokumentation om åsidosättning av konfiguration](../../../../datastreams/overrides.md) om du vill ha detaljerade anvisningar om hur du åsidosätter datastream-konfigurationer.

Som ett alternativ till att skicka åsidosättningarna via ett Web SDK-kommando kan du konfigurera åsidosättningarna på taggtilläggsskärmen som visas nedan.

>[!IMPORTANT]
>
> Åsidosättningar av dataström måste konfigureras per miljö. Utvecklings-, staging- och produktionsmiljöerna har alla olika åsidosättningar. Du kan kopiera inställningarna mellan dem med hjälp av de dedikerade alternativen som visas på skärmen nedan.

![Bild som visar åsidosättningar av dataströmskonfigurationer på tilläggssidan för Web SDK-taggen.](assets/datastream-overrides.png)

## Konfigurera avancerade inställningar

Använd **[!UICONTROL Edge base path]** fält om du behöver ändra grundsökvägen som används för att interagera med Edge Network. Det här behöver inte uppdateras, men om du deltar i en beta eller alfa kan Adobe be dig att ändra det här fältet.

![Bild som visar de avancerade inställningarna på tilläggssidan för Web SDK-taggar.](assets/advanced-settings.png)
