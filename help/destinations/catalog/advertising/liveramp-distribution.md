---
title: LiveRamp - Distribution Connection
description: Lär dig hur du använder LiveRamp - Distribution Connector för att aktivera målgrupper som tidigare har anslutit till LiveRamp till andra reklamdestinationer.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 5%

---


# [!DNL LiveRamp - Distribution] anslutning {#liveramp-onboarding}

The [!DNL LiveRamp - Distribution] Med hjälp av en anslutning kan ni aktivera målgrupper från Experience Platform till högklassiga utgivare i olika medier för mobiler, webben, displayannonsering och uppkopplade tv-apparater.

>[!IMPORTANT]
>
>Den här målanslutnings- och dokumentationssidan skapas och underhålls av LiveRamp. Om du har frågor eller uppdateringsfrågor kontaktar du LiveRamp direkt [här](mailto:example@email.com).

## Mål som stöds {#supported-destinations}

[!DNL LiveRamp - Distribution] har för närvarande stöd för målgruppsaktivering på följande plattformar:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL LiveRamp - Distribution] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

Marknadsföringsteamet för en sportklädhandlare använde [LiveRamp - introduktion](liveramp-onboarding.md) anslutning för att skicka målgrupper från Experience Platform till deras LiveRamp-konto.

Via [!DNL LiveRamp - Distribution] de nu kan aktivera de deltagande målgrupperna för de destinationer som anges högst upp på denna sida, så att de kan inrikta sig på användare på mobilen, öppna webben, sociala medier och [!DNL CTV] -plattformar.

## Anpassa målgrupper till LiveRamp {#onboarding}

Innan du aktiverar målgrupper via [!DNL LiveRamp - Distribution] anslutning, använd [LiveRamp - introduktion](liveramp-onboarding.md) anslutning för att exportera Experience Platform-målgrupper till LiveRamp.

När du har anmält dig till LiveRamp kan du fortsätta aktiveringsarbetsflödet från [ansluta till målet](#connect) steg.

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Identifieringsinställningar"
>abstract="Välj de identifierare som stöds av ditt mål. I dokumentationen finns en fullständig lista över identifierare som stöds för varje mål."

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till LiveRamp {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

![Plattformsgränssnittsbild som visar målanslutningsskärmen.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL Token URL]**: Din URL för LiveRamp-token.
* **[!UICONTROL LiveRamp Organization ID]**: Organisations-ID för ditt LiveRamp-konto.
* **[!UICONTROL Username]**: Användarnamn för ditt LiveRamp-konto.
* **[!UICONTROL Password]**: Lösenord för ditt LiveRamp-konto.

### Konfigurera målinformation {#destination-details}

När du har anslutit till ditt LiveRamp-konto anger du den information som krävs för att ansluta till målet som du vill aktivera målgrupper för.

![Plattformsgränssnittsbild som visar skärmen med målinformation.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Name]**: Ange det önskade namnet för målanslutningen.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen. Använd en beskrivning som hjälper dig att enkelt identifiera syftet med det här målet.
* **[!UICONTROL Destination]**: Använd listrutan för att välja det mål som du vill aktivera målgrupper för. Det mål du väljer här påverkar direkt det du ser i [målspecifika inställningar](#destination-settings) skärm.
* **[!UICONTROL Integration]**: Välj det integrationskonto som du vill använda för ditt mål.
* **[!UICONTROL Identifier]**: Välj de identifierare som stöds av ditt mål. För närvarande har alla mål sina identifierare som stöds förifyllda i listrutan.

## Målspecifika inställningar {#destination-settings}

Varje mål [stöds](#supported-destinations) av [!DNL LiveRamp - Onboarding] kräver att du fyller i specifika konfigurationsalternativ.

I avsnitten nedan finns detaljerade riktlinjer för hur du konfigurerar varje mål.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C-profilprofil-ID"
>abstract="Ange det numeriska ID som är kopplat till din 4C-varumärkesprofil. Om du inte har detta ID kontaktar du din 4C-representant för klienttjänster."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Avtal om målvillkor för annonsördata"
>abstract="Skriv in `I AGREE` för att bekräfta att du godkänner villkoren för Disneys annonsörs data."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Läs avtalet"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Din e-postadress"
>abstract="Ange en e-postadress som är kopplad till en individ. Den här e-postadressen fungerar som en signatur till avtalet för annonsörens datavillkor. Den här e-postadressen används även för att kontakta dig vid behov."

Om du vill konfigurera information för målet fyller du i fälten nedan.

![Plattformsgränssnittsbild som visar kunddatafälten för Disney-destinationen.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Advertiser data destination terms agreement]**: Skriv in `I AGREE` för att bekräfta att du godkänner villkoren för Disneys annonsörs data.
* **[!UICONTROL Client name]**: Ange ditt företagsnamn så som du vill att det ska visas för målpartnern.
* **[!UICONTROL Email address]**: Ange en e-postadress som är kopplad till en individ. Den här e-postadressen fungerar som en signatur till avtalet för annonsörens datavillkor.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Dataproviderns namn"
>abstract="Namnet på ditt företag så som du vill att det ska visas för Pandora. Namnet får innehålla högst 40 gemener och alfanumeriska tecken (t.ex. My_Company)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="E-postadress till kontorepresentant"
>abstract="E-postadressen till din Pandora-kontorepresentant. Den här adressen används för att skicka taxonomiuppdateringar. Om du vill ange flera adresser avgränsar du dem med kommatecken."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="E-postadress"
>abstract="Den här adressen används för att skicka taxonomiuppdateringar. Om du vill ange flera adresser avgränsar du dem med kommatecken."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Kontonamn"
>abstract="Namnet på ditt Pandora-konto. Kontakta din Pandora-kontorepresentant om du inte är säker på vad ditt kontonamn är. Använd inte blanksteg eller specialtecken."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Redigera annonsörs-ID"
>abstract="Ditt Redigera-ID. Måste börja med &quot;t2_&quot; eller &quot;a2_&quot;. Kontakta din REDIGERINGSrepresentant om du inte känner till ditt annonsörs-ID."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Redigera annonsörens namn"
>abstract="Din Reddit-annonsörs namn. Använd inte blanksteg eller specialtecken."

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="E-postadress för Roku-konto"
>abstract="Ange den e-postadress som är kopplad till ditt Roku-konto."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="E-postadress till kontorepresentant"
>abstract="Ange e-postadressen till din Roku-kontorepresentant. Den här adressen används för att skicka taxonomiuppdateringar. Om du vill ange flera adresser avgränsar du dem med kommatecken."

Om du vill konfigurera information för målet fyller du i fälten nedan.

![Plattformsgränssnittsbild som visar de identifierare som stöds för Roku-målet.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Roku account email address]**: Ange den e-postadress som är kopplad till ditt Roku-konto.
* **[!UICONTROL Roku account representative email address]**: Ange e-postadressen till din Roku-kontorepresentant. Om du vill ange flera adresser avgränsar du dem med kommatecken.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Kontotoken"
>abstract="En alfanumerisk identifierare som informerar Spotify om var data ska porteras och att du har verifierats att använda det här arbetsflödet. Kontakta din Spotify-kontohanterare för att få denna token."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="E-postadress till kontohanteraren"
>abstract="E-postadressen till kontohanteraren på Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Klientnamn"
>abstract="Ditt annonsörkontonamn som du vill ska visas för målpartnern. Använd ditt företagsnamn. Använd inte blanksteg eller specialtecken."

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

The [!DNL LiveRamp - Distribution] anslutningen aktiverar målgrupper som redan har anslutit till ditt LiveRamp-konto via [LiveRamp - introduktion](liveramp-onboarding.md) anslutning.

Om du vill aktivera dina målgrupper måste du i det här steget välja **samma målgrupper** som du tidigare har anslutit dig till LiveRamp.

>[!IMPORTANT]
>
>Att välja målgrupper som inte tidigare har anslutit sig till LiveRamp kommer inte att få de nya målgrupperna att komma igång.

## Exporterade data/Validera dataexport {#exported-data}

Om du vill verifiera och övervaka aktiveringen av målgrupperna loggar du in på ditt LiveRamp-konto och kontrollerar aktiveringsstatistik.

Om du har frågor om målgruppsaktiveringen kontaktar du din LiveRamp-kontorepresentant.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information om hur du konfigurerar [!DNL LiveRamp - Onboarding] lagring, se [officiell dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
