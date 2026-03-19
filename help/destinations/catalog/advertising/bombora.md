---
title: Bombora ABM Audience connection
description: Aktivera profiler för era Bombora-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på målgrupper.
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Bombora ABM Audience connection {#bombora}

>[!AVAILABILITY]
>
>Funktionen för att aktivera kontomålgrupper för Bombora ABM-målgrupper är tillgänglig för företag som köper [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)- och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-utgåvorna av Real-Time Customer Data Platform.

Aktivera profiler för era Bombora-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på [kontomålgrupper](/help/segmentation/types/account-audiences.md).

## Användningsfall {#use-case}

För att du bättre ska förstå hur och när du ska använda Bomboras mål finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Integrering med DSP {#dsp-integration}

Som B2B-marknadsförare kan du skapa en kontolista i CDP i realtid, som identifierar företag som visar hög återgivning för dina produkter och sedan använda den här destinationen för att aktivera den här listan i Bombora.

Tack vare Bomboras integrering med DSP:er kan ni köra riktade annonskampanjer med hjälp av Bomboradata. På så sätt kan ni försäkra er om att era annonskostnader fokuseras på de företag som mest sannolikt konverterar.

### Account-Based Marketing {#abm}

Som B2B-marknadsförare kan ni skapa en kontolista baserad på CRM- och marknadsföringssignaler. Sedan kan du använda den här destinationen för att aktivera den här listan i Bombora, där ABM-kompatibla kontroller hjälper dig att rikta in dig på beslutsfattare i dessa företag.

### Kontobaserad marknadsföring i flera kanaler {#multi-channel-abm}

Som B2B-marknadsförare kan du skapa en kontolista i CDP i realtid och identifiera företag med hög återgivning. Sedan kan ni använda den här destinationen för att aktivera listan i Bombora och köra riktade kampanjer i flera kanaler.

På betalda sociala medier kan du leverera personaliserade annonser till proffs på målkonton på plattformar som [!DNL LinkedIn] och [!DNL Facebook]. Med inbyggda annonsplattformar kan ni se till att innehållet når relevanta beslutsfattare.

Ni kan även utöka kampanjer till avancerad TV och leverera annonser till viktiga konton.

Detta flerkanaliga arbetssätt säkerställer enhetliga meddelanden på olika plattformar och maximerar engagemanget och konverteringsgraden.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

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


## Identiteter som stöds {#supported-identities}

Bombora kräver att målidentiteten mappas enligt tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| `primaryId` | Bombora kräver att den här målidentiteten mappas för att integreringen ska fungera korrekt. Du kan mappa vilket källfält som helst till den här identiteten. Denna mappning är obligatorisk men exporterar inte data till Bombora. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-and-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i målet [!DNL Bombora]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Om du vill exportera kontogrupper till Bombora behöver du följande information.

1. Ett Bombora-konto. Om du inte har något kan du begära ett Bombora-konto med hjälp av [aktiveringsformuläret för Bombora-målgrupper](https://customers.bombora.com/artcdp/audience-activation-request).
2. Ett Bombora **[!UICONTROL client ID]** och **[!UICONTROL client secret]**.
3. Data som skickas till Bombora måste komma från datauppsättningar som är **profilaktiverade**, så datauppsättningen inkluderas i profilen. Se till att dina datauppsättningar är [aktiverade för profilen](/help/catalog/datasets/enable-for-profile.md) innan du aktiverar målgrupper till det här målet.

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Lägg till innehavartoken](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL Client ID]**: Ange ditt [!DNL Bombora] klient-ID.
* **[!UICONTROL Client secret]**: Ange din [!DNL Bombora]-klienthemlighet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Lägg till information om målanslutningen](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

Nu kan ni aktivera era målgrupper i Bombora.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) om du vill ha instruktioner om hur du aktiverar kontomålgrupper till det här målet.

### Obligatoriska mappningar {#mapping}

Bomboras mål kräver att du konfigurerar följande mappningar för att kunna aktivera data.

| Source | Målfält | Beskrivning |
|---------|----------|---------|
| Valfritt värde | `Identity: primaryId` | Denna kartläggning är obligatorisk för Experience Platform att upprätta en anslutning till Bombora. Det här värdet exporteras inte till Bombora, men krävs för målkonfigurationen. Du kan välja vilket attribut som helst för källfältet. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora använder webbplats- eller domänadresser för att skapa en kontolista. |

![Lägg till obligatoriska mappningar](../..//assets/catalog/advertising/bombora/mappings.png)

## Funktionen Målgruppssynkronisering {#sync-behavior}

Efter den första målgruppsaktiveringen synkas efterföljande uppdateringar av målgruppen i Experience Platform stegvis till Bombora. Följande beteenden gäller:

* **Konto har lagts till för målgruppen**: När ett konto läggs till för målgruppen i Experience Platform läggs det automatiskt till för motsvarande målgrupp i Bombora.
* **Kontot har tagits bort eller kvalificerar inte längre**: När ett konto inte längre kvalificerar sig för målgruppen eller tas bort från målgruppen i Experience Platform tas det bort från motsvarande målgrupp i Bombora.
* **Konto eller profil borttagen**: När ett konto eller en profil tas bort från Experience Platform och det kontot inte längre är kvalificerat för målgruppen tas den bort från motsvarande målgrupp i Bombora.

### Borttagning och frånkoppling av målgrupper {#deletion-disconnect}

Om du tar bort en målgrupp i Experience Platform eller en målgrupp från ett aktiveringsdataflöde för Bombora tas målgruppen bort från ditt Bombora-konto.

## Ytterligare kommentarer och viktiga bildtexter {#additional-notes}

Om en kontopublik med samma namn aktiverades tidigare för Bombora, kommer du att få ett felmeddelande om du försöker aktivera den igen via ett annat dataflöde till Bomboras mål.
