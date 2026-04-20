---
title: Guidad inställning för vidarebefordran av händelser
description: Lär dig hur du konfigurerar vidarebefordran av händelser med hjälp av de guidade inställningarna.
exl-id: c155dec0-9130-4452-834a-08d98a15b006
source-git-commit: a2dd6b2a5ec8ccf4ca93e845c5b7b2b39d8d1599
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---

# Översikt över guidad konfiguration för vidarebefordran av händelser

>[!IMPORTANT]
>
>Den guidade installationsfunktionen är tillgänglig för kunder som har köpt Real-Time CDP Prime- och Ultimate-paketet. Kontakta Adobe om du vill ha mer information.

>[!NOTE]
>
>Alla befintliga klienter kan använda de guidade arbetsflödena för konfiguration för att skapa en referensimplementering som kan användas för följande:
>
>* Använd det som början på en helt ny implementering.
>* Utnyttja det som en referensimplementering som du kan undersöka för att se hur det har konfigurerats och sedan replikera i dina nuvarande produktionsimplementationer.

Den guidade installationsfunktionen hjälper dig att komma igång snabbt och enkelt. Verktyget automatiserar flera steg som utförs i Adobe-taggar och vidarebefordran av händelser, vilket avsevärt minskar installationstiden.

Den här installationen kan installera tillägg automatiskt. Den här hybridimplementeringen rekommenderas av [!DNL Meta] för att samla in och vidarebefordra händelsekonverteringar på serversidan. Den guidade installationsfunktionen är utformad för att hjälpa dig att komma igång med en implementering för vidarebefordran av händelser och är inte avsedd att leverera en komplett, fullt fungerande implementering som passar alla användningssätt.

## Kom igång med guidad konfiguration {#guided-setup}

Om du vill komma igång med funktionen väljer du **[!UICONTROL Get Started]** i användargränssnittet för **[!UICONTROL Event Forwarding]** datainsamlingar.

![Hemsidan för vidarebefordran av händelser som visar Kom igång-kortet i användargränssnittet för datainsamlingar](../../images/ui/guided-setup/get-started.png)

>[!INFO]
>
>Du kan även komma åt de guidade inställningarna direkt från startsidan för Datainsamlingar.

### Skapa en ny taggegenskap {#new-property}

I avsnittet Konfigurera egenskaper väljer du **[!UICONTROL New]** och anger den nya **[!UICONTROL Property Domain]**-informationen.

![Konfigurera egenskaper som visar ny domäninformation](../../images/ui/guided-setup//configure-properties-new.png)

Välj **[!UICONTROL Add]** för [!DNL Meta Conversion API] i avsnittet Lägg till tillägg. På sidan Konfigurera information för [!DNL Meta] kan du ange **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** och **[!UICONTROL Data Layer Path]** manuellt, eller så kan du använda alternativet **[!UICONTROL Connect to Meta]**.

![Konfigurera informationssidan för Meta med alternativet Anslut till Meta](../../images/ui/guided-setup/connect-to-meta.png)

#### Anslut till [!DNL Meta] med dina autentiseringsuppgifter {#meta-credentials}

Välj **[!UICONTROL Connect to Meta]**, ange dina [!DNL Meta]-inloggningsuppgifter och välj **[!UICONTROL Log in]** och välj sedan **[!UICONTROL Next]**.

Du kommer nu att bli ombedd att **skapa en affärsportfölj**. Ange **[!UICONTROL Business portfolio name]** och välj **[!UICONTROL Next]**.

![Skapa en företagsportföljssida som visas med ett portföljnamn](../../images/ui/guided-setup/portfolio-name.png)

Välj din affärsportfölj i listan och välj sedan **[!UICONTROL Next]**. Du kan se inställningarna för Business Portfolio, Ad Account och [!DNL Meta Pixel]. Välj **[!UICONTROL Continue]** för att bekräfta inställningarna och välj sedan **[!UICONTROL Next]**.

Det tar några minuter innan installationen är klar och välj sedan **[!UICONTROL Done]**.

**[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** och **[!UICONTROL Data Layer Path]** fylls i automatiskt. Välj **[!UICONTROL Save]**.

![Konfigurera Meta Information-sidan med Meta-information ifylld](../../images/ui/guided-setup/meta-info.png)

#### Skapa resurser för den nya taggegenskapen {#create-resources}

I avsnittet Skapa resurser väljer du **[!UICONTROL Pre-check resources]** om du vill kontrollera organisationen och egenskaperna för kollisioner eller befintliga nödvändiga resurser för implementeringen.

![Skapa resurser som visar resurser för förkontroll](../../images/ui/guided-setup/pre-check-resources.png)

På sidan Åtgärder visas en lista med uppgifter och åtgärder. Välj **[!UICONTROL Create Resources]** om du vill skapa de här aktiviteterna.

![Uppgiftsåtgärder som visar en lista över uppgifter och åtgärder som ska vidtas](../../images/ui/guided-setup/create-resources.png)

Tillåt några minuter för att slutföra installationen av nödvändiga regler, dataelement, tillägg, bibliotek, SDK:er och så vidare. I avsnittet Skapa resurser finns länkar till de egenskaper och resurser som skapats.

#### Validera implementeringen {#validate-implementation}

I avsnittet Validera implementering finns den inbäddningslänk som du kan använda på webbplatsen. **[!UICONTROL Start Validation]** kör testet i din aktuella webbläsarsession på den här guidade konfigurationssidan. Om valideringen lyckas här bör samma implementering fungera när du distribuerar inbäddningslänken på webbplatsen.

Välj **[!UICONTROL Send PageView Event]** om du vill skicka en testhändelse via Adobe Experience Platform Edge Network. Den vidarebefordras sedan till [!DNL Meta] på serversidan. Välj **[!UICONTROL Finished Validation]** för att slutföra installationen.

>[!NOTE]
>
>Om det uppstår fel under valideringsprocessen markerar du länken **[!UICONTROL Assurance]** för att granska händelser som kan ha misslyckats.

![Valideringssida med valideringsresultat](../../images/ui/guided-setup/finished-validation.png)

### Använda en befintlig taggegenskap {#existing-property}

Välj **[!UICONTROL Existing]** i avsnittet Konfigurera egenskaper och välj sedan taggegenskapen i listrutan. Systemet försöker hitta den händelsevidarebefordringsegenskap som redan är kopplad till den här egenskapen via datastreams. Du kan nu fortsätta att konfigurera om [!DNL Meta Conversion API] och sedan förkontrollera och skapa resurser.

![Konfigurera befintlig egenskap som visar den befintliga taggegenskapen vald](../../images/ui/guided-setup/configure-properties-existing.png)

Om den markerade taggegenskapen inte är ansluten till en egenskap för vidarebefordring av händelser eller om datastreams saknas, skapas de automatiskt.

![Konfigurera befintlig egenskap som visar den befintliga taggegenskapen vald](../../images/ui/guided-setup/configure-properties-existing-no-event-fw.png)

Om du vill konfigurera [!DNL Meta Conversion API] följer du den process som markeras ovan i [Anslut till [!DNL Meta] med dina autentiseringsuppgifter](#meta-credentials).

Nu när du har genererat **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** och **[!UICONTROL Data Layer Path]** väljer du **[!UICONTROL Pre-Check resources]** för att skapa arbetsflödet för vidarebefordran av händelser.

Eftersom du använder en befintlig taggegenskap skiljer sig konfigurationsprocessen något från det nya egenskapsarbetsflödet. Du kan se att systemet inte skapar webbegenskapen, värddatorn och miljön eftersom dessa redan finns. Välj slutligen **[!UICONTROL Create Resources]** för att skapa de uppgifter som ännu inte är tillgängliga.

![Uppgiftsåtgärder som visar en lista med uppgifter och åtgärder som ska utföras och som markerar de som kommer att hoppas över](../../images/ui/guided-setup/create-resources-skip.png)

>[!INFO]
>
>Den guidade installationen lägger automatiskt till anteckningar till egenskaper som uppdateras under processen. Du kan visa dessa i avsnittet Anteckningar på den högra panelen i taggegenskapen i redigeringsläge. Du kan se när egenskapen uppdaterades eller skapades med det guidade konfigurationsverktyget. Med hjälp av granskningsspåret kan du spåra ändringar som har gjorts i funktionen för guidade inställningar.

Tillåt några minuter för att slutföra installationen av nödvändiga regler, dataelement, tillägg, bibliotek, SDK:er och så vidare. I avsnittet Skapa resurser finns länkar till de egenskaper och resurser som skapats.

I avsnittet Validera implementering finns den inbäddningslänk som du kan använda på webbplatsen. **[!UICONTROL Start Validation]** kör testet i din aktuella webbläsarsession på den här guidade konfigurationssidan. Om valideringen lyckas här bör samma implementering fungera när du distribuerar inbäddningslänken på webbplatsen.

Välj **[!UICONTROL Send PageView Event]** om du vill skicka en testhändelse via Adobe Experience Platform Edge Network. Den vidarebefordras sedan till [!DNL Meta] på serversidan. Välj **[!UICONTROL Finished Validation]** för att slutföra installationen.

>[!NOTE]
>
>Om det uppstår fel under valideringsprocessen markerar du länken **[!UICONTROL Assurance]** för att granska händelser som kan ha misslyckats.

![Valideringssida med valideringsresultat](../../images/ui/guided-setup/finished-validation.png)

## Nästa steg {#next-steps}

I den här guiden beskrivs hur du använder det guidade konfigurationsverktyget för att skapa och konfigurera egenskaper för [!DNL Meta Conversions API].

Mer information om hur du implementerar din integrering finns i [!DNL Meta]-dokumentationen om [bästa praxis för  [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965). Mer allmän information om taggar och vidarebefordran av händelser i Adobe Experience Cloud finns i [taggöversikten](../../home.md).
