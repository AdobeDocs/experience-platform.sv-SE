---
keywords: luftfartygets etikett;luftfartygets destination
title: Ansluta till luftfartygets taggar
description: Skicka enkelt Adobe Audience Data till Airship som målgruppstaggar för målinriktning inom Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# [!DNL Airship Tags]-anslutning {#airship-tags-destination}

## Översikt {#overview}

[!DNL Airship] är den ledande kundinteraktionsplattformen, som hjälper dig att leverera meningsfulla, personaliserade flerkanalsmeddelanden till användarna i alla faser av kundlivscykeln.

Den här integreringen överför målgruppsdata från Adobe Experience Platform till [!DNL Airship] som [taggar](https://docs.airship.com/guides/audience/tags/) för målinriktning eller utlösande åtgärder.

Mer information om [!DNL Airship] finns i [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL Airship]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förutsättningar {#prerequisites}

Innan du kan skicka Adobe Experience Platform-målgrupper till [!DNL Airship] måste du:

* Skapa en tagggrupp i ditt [!DNL Airship]-projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
>
>Skapa ett [!DNL Airship]-konto via [den här registreringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan har det.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare som används i målet för Airship-taggar. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Tagggrupper {#tag-groups}

Målgrupper i Adobe Experience Platform liknar [taggar](https://docs.airship.com/guides/audience/tags/) i Airship, men implementeringen skiljer sig något. Den här integreringen mappar statusen för en användares [medlemskap i ett Experience Platform-segment](../../../xdm/field-groups/profile/segmentation.md) till om en [!DNL Airship]-tagg finns eller inte. I en Experience Platform-publik där `xdm:status` ändras till `realized` läggs taggen till i [!DNL Airship]-kanalen eller namngivna användare som profilen mappas till. Om `xdm:status` ändras till `exited` tas taggen bort.

Om du vill aktivera den här integreringen skapar du en *tagggrupp* i [!DNL Airship] med namnet `adobe-segments`.

>[!IMPORTANT]
>
>När du skapar den nya tagggruppen **Kontrollera inte** alternativknappen [!DNL Allow these tags to be set only from your server]. Om du gör det misslyckas integreringen av Adobe-taggar.

Mer information om hur du skapar tagggruppen finns i [Hantera tagggrupper](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups).

## Generera innehavartoken {#generate-bearer-token}

Gå till **[!UICONTROL Settings]** **[!UICONTROL APIs & Integrations]** på [kontrollpanelen för luftskepp](https://go.airship.com) och välj **[!UICONTROL Tokens]** på den vänstra menyn.

Klicka på **[!UICONTROL Create Token]**.

Ange ett användarvänligt namn för din token, till exempel&quot;Adobe Tags Destination&quot;, och välj&quot;All Access&quot; för rollen.

Klicka på **[!UICONTROL Create Token]** och spara informationen som konfidentiell.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Airship Tags] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1 {#use-case-1}

Återförsäljare eller underhållningsplattformar kan skapa användarprofiler för sina lojalitetskunder och skicka dessa målgrupper till [!DNL Airship] för meddelandemålinriktning på mobilkampanjer.

### Använd skiftläge 2 {#use-case-2}

Trigga personliga meddelanden i realtid när användare faller in i eller ut från en viss målgrupp inom Adobe Experience Platform.

En återförsäljare skapar t.ex. en varumärkesspecifik jeans-publik i Experience Platform. Den återförsäljaren kan nu utlösa ett mobilt meddelande så snart någon sätter sin jeans för ett visst varumärke.

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
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Mappningsöverväganden {#mapping-considerations}

[!DNL Airship]-taggar kan anges antingen på en kanal, som representerar en enhetsinstans, till exempel iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, till exempel ett kund-ID. Om du har oformaterad e-postadress som primär identitet i ditt schema, markerar du e-postfältet i **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

För identifierare som ska mappas till en kanal, dvs. en enhet, mappas till rätt kanal baserat på källan. Följande bilder visar hur du mappar ett Google Advertising ID till en [!DNL Airship] Android-kanal.

![Anslut till flaggor för luftskepp](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Ansluta till airship-taggar](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Kanalmappning](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](../../../data-governance/home.md).
