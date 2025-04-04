---
keywords: luftfartygsattribut;luftfartygets destination
title: Luftfartygsattribut, anslutning
description: Skicka enkelt Adobe Audience Data till Airship som målgruppsattribut för målinriktning inom Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 3%

---

# [!DNL Airship Attributes]-anslutning {#airship-attributes-destination}

>[!IMPORTANT]
>
>* Från och med 25 mars 2025 kan du se två [!DNL Airship Attributes]-kort sida vid sida i målkatalogen. Det här beror på en intern uppgradering av måltjänsten. Den befintliga [!DNL Airship Attributes]-målkopplingen har bytt namn till **[!UICONTROL (Deprecated) Airship Attributes]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Airship Attributes]**.
>* Använd anslutningen **[!UICONTROL Airship Attributes]** i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till målet **[!UICONTROL (Deprecated) Airship Attributes]** uppdateras de automatiskt, så ingen åtgärd krävs från dig.
>* Om du skapar dataflöden via [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:
>   * Flödesspecifikation-id: `a862e0be-966e-4e5a-80d3-1bb566461986`
>   * Anslutningsspecifikation-id: `594bc002-4a47-49b7-8a98-ac0d21045502`

## Översikt {#overview}

[!DNL Airship] är det ledande Experience Platform för kundengagemang som hjälper dig att leverera meningsfulla, personaliserade flerkanalsmeddelanden till dina användare i alla faser av kundlivscykeln.

Den här integreringen skickar Adobe-profildata till [!DNL Airship] som [Attribut](https://docs.airship.com/guides/audience/attributes/) för målinriktning eller utlösande åtgärder.

Mer information om [!DNL Airship] finns i [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL Airship]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förhandskrav {#prerequisites}

Innan du kan skicka målgrupper till [!DNL Airship] måste du:

* Aktivera attribut i ditt [!DNL Airship]-projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
>
>Skapa ett [!DNL Airship]-konto via [den här registreringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan har det.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel e-postadress, telefonnummer, efternamn) och/eller identiteter enligt fältmappningen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Aktivera attribut {#enable-attributes}

Adobe Experience Platform-profilattribut liknar [!DNL Airship]-attribut och kan enkelt mappas till varandra i Experience Platform med hjälp av mappningsverktyget som visas längre fram på den här sidan.

[!DNL Airship] projekt har flera fördefinierade attribut och standardattribut. Om du har ett anpassat attribut måste du definiera det i [!DNL Airship] först. Mer information finns i [Konfigurera och hantera attribut](https://docs.airship.com/tutorials/audience/attributes/).

## Generera innehavartoken {#bearer-token}

Gå till **[!UICONTROL Settings]** **[!UICONTROL APIs & Integrations]** på [kontrollpanelen för luftskepp](https://go.airship.com) och välj **[!UICONTROL Tokens]** på den vänstra menyn.

Klicka på **[!UICONTROL Create Token]**.

Ange ett användarvänligt namn för din token, t.ex. &quot;Adobe Attributes Destination&quot;, och välj &quot;All Access&quot; för rollen.

Klicka på **[!UICONTROL Create Token]** och spara informationen som konfidentiell.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Airship Attributes] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1

Utnyttja profildata som samlats in inom Adobe Experience Platform för att personalisera meddelandet och multimediematerialet i någon av [!DNL Airship]s kanaler. Använd till exempel profildata för [!DNL Experience Platform] för att ange platsattribut i [!DNL Airship]. På så sätt kan ett hotellmärke visa en bild för varje användares närmaste hotell.

### Använd skiftläge 2

Utnyttja attribut från Adobe Experience Platform för att ytterligare berika [!DNL Airship]-profiler och kombinera dem med prediktiva data från SDK eller [!DNL Airship]. En återförsäljare kan t.ex. skapa en målgrupp med lojalitetsstatus och platsdata (attribut från Experience Platform) och [!DNL Airship] förväntas ändra data för att skicka extremt målinriktade meddelanden till användare med guldlojalitetsstatus som bor i Las Vegas, NV och har en hög sannolikhet för kurning.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!UICONTROL Bearer token]**: Bearer-token som du genererade från kontrollpanelen [!DNL Airship].

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för det här målet.
* **[!UICONTROL Domain]**: välj ett datacenter för USA eller EU, beroende på vilket datacenter [!DNL Airship] som gäller för det här målet.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Mappningsöverväganden {#mapping-considerations}

[!DNL Airship]-attribut kan anges antingen på en kanal, som representerar en enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har oformaterad e-postadress som primär identitet i ditt schema, markerar du e-postfältet i **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship/mapping.png)

För identifierare som ska mappas till en kanal, d.v.s. en enhet, mappar du till lämplig kanal baserat på källan. Följande bilder visar hur två mappningar skapas:

* IDFA iOS Advertising ID till en [!DNL Airship] iOS-kanal
* Adobe `fullName`-attribut till attributet [!DNL Airship] &quot;Fullständigt namn&quot;

>[!NOTE]
>
>Använd det användarvänliga namnet som visas på kontrollpanelen [!DNL Airship] när du väljer målfältet för din attributmappning.

**Mappa identitet**

Välj källfält:

![Anslut till attribut för luftskepp](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Välj målfält:

![Anslut till attribut för luftskepp](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Mappningsattribut**

Välj källattribut:

![Välj källfält](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Välj målattribut:

![Välj målfält](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verifiera mappning:

![Kanalmappning](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](../../../data-governance/home.md).
