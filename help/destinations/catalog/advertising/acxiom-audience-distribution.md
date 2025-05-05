---
title: Acxiom-målgruppsdistribution
description: Använd  [!DNL Acxiom Audience Distribution] målet om du vill förbättra målgrupper med  [!DNL Acxiom's Real ID] teknik och aktivera målgrupper på flera plattformar, till exempel  [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] med flera.
badge: Beta
source-git-commit: 7db60161b638cce1845c430f6086441599a0bc61
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---


# [!DNL Acxiom Audience Distribution] mål

>[!NOTE]
>
>Målet [!DNL Acxiom Audience Distribution] är i betaversion. Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL Acxiom]-teamet. Kontakta Acxiom [här](mailto:acxiom-adobe-help@acxiom.com) om du har frågor eller uppdateringsfrågor.

Använd målet [!DNL Acxiom Audience Distribution] för att förbättra målgrupper med tekniken [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) och aktivera målgrupper på flera plattformar, till exempel [!DNL Altice], [!DNL Ampersand], [!DNL Comcast].

Den här självstudien innehåller anvisningar om hur du skapar en [!DNL Acxiom Audience Distribution]-målkoppling med användargränssnittet i [!DNL Adobe Experience Platform]. Den här kopplingen används för att skapa och distribuera målgrupper till valda destinationer.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Acxiom Audience Distribution] finns det ett exempel på användning som [!DNL Adobe Experience Platform]-kunder kan lösa med den här anslutningen.

### Skicka målgrupper från Experience Platform till ditt Acxiom-konto {#send-audiences}

Använd den här målkopplingen om du är marknadsföringsproffs och vill skicka målgrupper från [!DNL Experience Platform] till ditt [!DNL Acxiom]-konto för kanalövergripande värvning.

Marknadsföringsavdelningen på ett globalt varumärke för finansiella tjänster är till exempel intresserad av att värva kunder över flera kanaler via olika annonsplattformar. De kan använda [!DNL Acxiom Audience Distribution]-målanslutningen för att skicka målgrupper från [!DNL Experience Platform] till [!DNL Acxiom], förbättra målgrupperna med [!DNL Acxiom's Real ID]-teknik och aktivera målgrupperna på flera plattformar, som [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] med mera.

## Förhandskrav {#prerequisites}

* **Bekräfta användningsvillkoren:** Innan du kan konfigurera ett nytt [!DNL Acxiom Audience Distribution]-mål måste du läsa och signera [!DNL Acxiom's] användningsvillkoren för avtalet. Du får länken till avtalet när den genomförda försäljningsordern är slutförd. Innan du har signerat avtalet kommer du inte att se målkortet [!DNL Acxiom Audience Distribution] i Experience Platform-målkatalogen. När du har godkänt och signerat avtalet slutför [!DNL Adobe] din introduktionsprocess och du ser målkortet [!DNL Acxiom Audience Distribution].
* **Du måste känna till ditt företags-ID för Adobe:** Ditt [!DNL Adobe] organisation-ID krävs för att slutföra ditt användaravtal. Mer information om hur du [visar ditt företags-ID](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) finns i avsnittet [!DNL Adobe's] *Organisationer i Experience Cloud*.

## Destinationer som stöds {#supported-destinations}

Målet [!DNL Acxiom Audience Distribution] stöder för närvarande målgruppsaktivering på följande plattformar.<br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Anslut till målet {#connect}

Autentisering till [!DNL Acxiom's Audience Distribution]-målet hanteras automatiskt bakom scenerna för att underlätta för dig.

## Målspecifika inställningar {#destination-settings}

Vissa [!DNL Acxiom Audience Distribution]-mål kräver ytterligare information. Avsnitten nedan innehåller detaljerad vägledning om hur du konfigurerar dessa alternativ.

### [!DNL LG Ads] {#lg-ads}

Om du vill konfigurera information för målet fyller du i fälten nedan.

* **Segmentkategori**: Målkategorin eller den lodräta som segmentet tillhör. Exempel: finansiella tjänster, bilar, hälsa osv.

![LG lägger till målinformation](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

>[!NOTE]
>
>Målet [!DNL Acxiom Audience Distribution] stöder endast fullständig filexport.

### Mappa attribut och identiteter {#map}

För att målplatsen [!DNL Acxiom Audience Distribution] ska kunna ta emot målgruppsdata på rätt sätt måste du mappa källfälten från Experience Platform till rätt [!DNL Acxiom Audience Distribution] målfält.

[!DNL Acxiom Audience Distribution] tillåter bara mappning till följande målfält. Målfälten som beskrivs i tabellen nedan måste mappas i den ordning som visas nedan.

| Fältnamn | Beskrivning | Obligatoriskt | Fältordning | Maximal längd |
|---|---|---|---|---|          
| Förnamn | Förnamn på individ | Nej | 1 | 255 |
| Mitten | Personens mellannamn eller inledning | Nej | 2 | 50 |
| Efternamn | Personens efternamn | Ja | 3 | 255 |
| Generationssuffix | Personens suffix | Nej | 4 | 10 |
| Adressrad 1 | Adress 1 fält för primärbosättning | Ja | 5 | 255 |
| Adressrad 2 | Adress 2 fält för primärbosättning | Nej | 6 | 255 |
| Ort | Hemort | Ja | 7 | 255 |
| Läge | Statlig förkortning av primär hemvist | Ja | 8 | 2 |
| Postnummer | Fullständigt postnummer för den primära bostaden | Ja | 9 | 10 |
| E-post | Primär e-post Som standard används det här fältet som en dedupliceringsnyckel för att göra posterna unika | Nej | 10 | 255 |
| Telefon | Telefonnummer till individ (riktnummer + nummer)<br> Det här fältet används som standard som en dedupliceringsnyckel för att göra posterna unika. | Nej | 11 | 10 |

I kolumnen **[!UICONTROL Source Field]** anger du namnet på vart och ett av källattributen som du vill mappa till motsvarande målfält, eller markerar pilikonen för att öppna skärmen **[!UICONTROL &#x200B; Select source field]**.<br>
![ Mappningsskärm ](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

När du har mappat alla fält väljer du **[!UICONTROL Next]**.

Om du inte använder standardschemat [!DNL Adobe's] läser du [Användargränssnittsguiden för frågetjänst](../../../query-service/ui/overview.md) om du vill ha mer information om hur du använder frågetjänsten för att fylla i [!DNL Adobe]-standardschemat med dina fältnamn.

### Granska {#review}

När du har slutfört alla steg ovan kan du granska din målanslutningsstatus och målgruppsinformation innan du aktiverar (distribuerar) den. De valda målgrupperna visas längst ned i en lista. Varje målgrupp blir ett separat anrop till API:t [!DNL Acxiom Audience Distribution].

Om du är nöjd med resultaten väljer du **[!UICONTROL Finish]** för att aktivera målet.

![Granska din målgrupp](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## Felsökning {#troubleshooting}

Om din målrepresentant inte kan hitta din målgrupp kontaktar du [!DNL Adobe]-representanten för att få hjälp.

Du måste lämna följande information till din [!DNL Adobe]-representant:
* Målgruppsnamn
* Destinationsnamn
* Målgruppsaktiveringsdatum
* Exporterat filnamn

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du aktiverat en målgrupp för den valda målplattformen. Kontakta sedan din representant för målplattformen för att börja konfigurera kampanjen.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).


