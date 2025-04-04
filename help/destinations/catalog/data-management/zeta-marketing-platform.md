---
title: Zeta Marketing Platform
description: Zeta Marketing Platform (ZMP) är ett molnbaserat system som hjälper er att anskaffa, utöka och behålla kunder på ett effektivare sätt, med hjälp av intelligens (egna data och AI).
hide: true
hidefromtoc: true
exl-id: 291ee60c-aa81-4f1e-9df2-9905a8eeb612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# Zeta Marketing Platform {#zeta-marketing-platform}

## Översikt {#overview}

Zeta Marketing Platform (ZMP) är ett molnbaserat system som hjälper er att anskaffa, utöka och behålla kunder på ett effektivare sätt, med hjälp av intelligens (egna data och AI). Mer information finns i [Zeta Global](https://zetaglobal.com/).

Med Zeta Marketing Platform-kontakten i Adobe Experience Platform kan ni smidigt synkronisera era målgrupper från Experience Platform till ZMP.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *Zeta Global* -teamet. Kontakta teamet på [Kontakta oss](https://zetaglobal.com/about/contact-us/) om du har frågor eller uppdateringsfrågor.

## Användningsfall {#use-cases}

### Bygg målgruppssegment {#use-case-build-audiences}

En marknadsförare vill skapa unika målgruppsprofiler, identifiera sina mest värdefulla segment och använda dem i alla digitala kanaler som Zeta Marketing Platform stöder. De vill skapa en äkta 360-vy av en konsumentprofil, bygga upp och aktivera meningsfulla målgrupper. Mer information om vilka kanaler Zeta Marketing Platform stöder finns [här](https://zetaglobal.com/platform/integrations/).

### Rikta användare med annonser {#use-case-target-users}

En annonsör vill rikta sig till användare inom specifika målgrupper via Zeta Demand Side Platform (DSP), eftersom dessa användare interagerar med sina varumärken. Klicka [här](https://knowledgebase.zetaglobal.com/pug/) om du vill ha mer information om Zeta DSP.

## Förhandskrav {#prerequisites}

### Krav för Zeta Marketing Platform

* Innan du skapar en ny anslutning till Zeta Marketing Platform-målet måste du skapa en tom kundlista i ditt Zeta Marketing Platform-konto. Du måste välja en av dessa kundlistor som mål för att få den Adobe Experience Platform-publik som du tänker skicka. Du kan skapa en tom kundlista i ZMP genom att följa instruktionerna [här](https://knowledgebase.zetaglobal.com/kb/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Även om Adobe Experience Platform tillåter aktivering av flera målgrupper till en viss ZMP-destinationsinstans, är det obligatoriskt att varje ZMP-destinationsinstans endast tar emot en Experience Platform-målinstans. Om du vill hantera flera målgrupper från Experience Platform skapar du ytterligare ZMP-målinstanser för varje målgrupp och väljer en annan kundlista i listrutan. Detta säkerställer att målgrupperna inte skrivs över. Mer information finns i [Fyll i målinformation](#destination-details).
* Använd följande autentiseringsuppgifter för att konfigurera målet:
   * Användarnamn: **api**
   * Lösenord: Din ZMP REST API-nyckel. Du hittar din REST API-nyckel genom att logga in på ditt ZMP-konto och navigera till avsnittet **Inställningar** > **Integrationer** > **Tangenter och appar**. Mer information finns i [ZMP-dokumentationen](https://knowledgebase.zetaglobal.com/kb/integrations).

## Identiteter som stöds {#supported-identities}

[!DNL Zeta Marketing Platform] stöder aktivering av anpassade användar-ID:n som beskrivs i tabellen nedan. Mer information finns i [identiteter](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> Målet för Zeta Marketing Platform kräver att du mappar ett namnområde för källidentiteten till ZMP `uid`-målidentiteten. Detta hjälper Zeta Marketing Platform att särskilja varje profil unikt.

| Målidentitet | Beskrivning | Överväganden | Anteckningar |
---------|----------|----------|----------|
| uid | Unikt ID som ZMP använder för att differentiera kundprofiler | Obligatoriskt | Välj standardnamnområdet för identiteter `Email` om du vill identifiera unika profiler med deras e-postadresser. Du kan också välja att mappa ditt anpassade namnområde till `uid` om kundprofilerna inte har något e-postmeddelande. |
| email_md5_id | E-post MD5 som representerar varje kundprofil | Valfritt | Välj den här målidentiteten när du vill identifiera kundprofiler unikt med e-post-MD5-värden. Det är viktigt att e-postadresser redan är i MD5-format inom Experience Platform eftersom Experience Platform inte konverterar oformaterad text till MD5. I det här scenariot anger du `uid` (obligatoriskt) till antingen samma MD5-värden för e-post eller till ett annat lämpligt ID-namnområde. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

>[!NOTE]
> När enskilda medlemmar läggs till eller tas bort från Experience Platform-målgruppen skickas uppdateringar till ZMP för att säkerställa att målkundslistan synkroniseras i enlighet med detta.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!UICONTROL Username]**: `api`
* **[!UICONTROL Password]**: Din ZMP REST API-nyckel. Du hittar din REST API-nyckel genom att logga in på ditt ZMP-konto och navigera till avsnittet **Inställningar** > **Integrationer** > **Tangenter och appar**. Mer information finns i [ZMP-dokumentationen](https://knowledgebase.zetaglobal.com/kb/integrations).

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Bild som visar ZMP-konfiguration](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL ZMP Account Site Id]**: Ditt ZMP **Site ID** där du vill skicka dina målgrupper. Du kan visa ditt webbplats-ID genom att gå till avsnittet **Inställningar** > **Integrationer** > **Tangenter och appar**. Mer information finns [här](https://knowledgebase.zetaglobal.com/kb/integrations).
* **[!UICONTROL ZMP Segment]**: Kundlistsegmentet i ditt ZMP-webbplats-ID-konto som du vill ska uppdateras med Experience Platform-målgruppen.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Nedan visas ett exempel på korrekt identitetsmappning när profiler exporteras till [!DNL Zeta Marketing Platform].

Välja källfält:
* Välj ett namnområde för källidentitet (anpassat eller standard, till exempel `Email`) som unikt identifierar en profil i Adobe Experience Platform och [!DNL Zeta Marketing Platform].
* Välj eventuella XDM-källprofilattribut som behöver exporteras till och uppdateras i [!DNL Zeta Marketing Platform].

Markera målfält:
* (Obligatoriskt) Välj `uid` som den målidentitet som du mappar ett källidentitetsnamnområde till.
* (Valfritt) Välj `email_md5_id` som mål-ID som du mappade källidentitetsnamnområdet som representerar e-post-ID5-värden till. Det är viktigt att e-postadresserna redan är i MD5-format i Experience Platform eftersom Experience Platform inte konverterar oformaterad text till MD5
* Välj eventuella ytterligare målmappningar.

![Identitetsmappning](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Exporterade data/Validera dataexport {#exported-data}

En lyckad målgruppsaktivering från Experience Platform till Zeta Marketing Platform uppdaterar kundlistan i ZMP. Antalet och exempelprofilerna i målkundlistan är lika med antalet identiteter som har aktiverats.

![Kundlista i ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Alla målgruppsmedlemmar som har aktiverats från Experience Platform visas också under **Publiker** > **Personer** i ZMP. Du kan även visa segmentet **Kundlista** som en profil tillhör i vyn för enstaka kunder, se nedan.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

* [Zeta Knowledge Base](https://knowledgebase.zetaglobal.com/kb/)
