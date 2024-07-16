---
title: Konfigurera objektidentifiering för datastreams
description: Lär dig hur du konfigurerar identifieringen av robotar för datastreams för att särskilja mänsklig och icke-mänsklig trafik.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: ff95e5e105f7b3e1213eab90456b9fa9000918d3
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 0%

---

# Konfigurera objektidentifiering för datastreams

Trafik som härrör från icke-mänskliga enheter, som automatiserade program, webbskrapor, spindlar, skriptskannrar, kan göra det svårare att identifiera händelser som inträffar från mänskliga besökare. Den här typen av trafik kan påverka viktiga affärsvärden negativt, vilket leder till felaktig trafikrapportering.

Med punktidentifiering kan du identifiera händelser som har genererats av [Web SDK](../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) och [[!DNL Server API]](../server-api/overview.md) som om de har genererats av kända spindlar och bottar.

Genom att konfigurera robotidentifiering för dina datastreams kan du identifiera specifika IP-adresser, IP-intervall och begäranrubriker som du vill klassificera som båda händelser.

Identifiering av robottrafiken kan ge en mer exakt mätning av användaraktiviteten på er webbplats eller i mobilapplikationen.

När en begäran till Edge Network överensstämmer med någon av robotidentifieringsreglerna uppdateras XDM-schemat med en bockpoäng (alltid inställt på 1), vilket visas nedan.

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Denna robotbedömning hjälper de lösningar som tar emot begäran att identifiera robottrafiken korrekt.

>[!IMPORTANT]
>
>Punktavkänning tar inte bort några robotförfrågningar. Det uppdaterar bara XDM-schemat med robotpoängen och vidarebefordrar händelsen till [datastream-tjänsten](configure.md) som du konfigurerade.
>
>Adobe lösningar kan hantera båda poängen på olika sätt. Adobe Analytics använder till exempel sin egen [robotfiltreringstjänst](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) och använder inte poängen som angetts av Edge Network. De två tjänsterna använder samma [IAB-robotlista](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), så robotpoängen är identiska.

Det kan ta upp till 15 minuter att sprida regler för punktidentifiering över hela Edge Network efter att de har skapats.

## Förhandskrav {#prerequisites}

För att robotidentifiering ska fungera på datastream måste du lägga till fältgruppen **[!UICONTROL Bot Detection Information]** i ditt schema. Mer information om hur du lägger till fältgrupper i ett schema finns i [XDM-schemats](../xdm/ui/resources/schemas.md#add-field-groups)-dokumentation.

## Konfigurera objektidentifiering för datastreams {#configure}

Du kan konfigurera robotidentifiering när du har skapat en datastream-konfiguration. Läs dokumentationen om hur du [skapar och konfigurerar ett datastream](configure.md) och följ sedan instruktionerna nedan för att lägga till båda identifieringsfunktioner i ditt datastream.

Gå till datastreams-listan och välj den datastream som du vill lägga till robotidentifiering till.

![Datastreams-användargränssnitt som visar listan med datastreams.](assets/bot-detection/datastream-list.png)

På informationssidan för datastream väljer du alternativet **[!UICONTROL Bot Detection]** till höger.

![Alternativet för punktidentifiering är markerat i användargränssnittet för datastreams.](assets/bot-detection/bot-detection.png)

Sidan **[!UICONTROL Bot Detection Rules]** visas.

![Inställningar för punktavkänning på inställningssidan för datastream.](assets/bot-detection/bot-detection-page.png)

På sidan Regler för punktidentifiering kan du konfigurera robotidentifiering med följande funktioner:

* Använder [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Skapa egna identifieringsregler för robotar.

### Använd listan IAB/ABC International Spiders and Bots {#iab-list}

[IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) är en tredjeparts lista över Internet-spindlar och bots som är branschstandard. Den hjälper dig att identifiera automatiserad trafik, till exempel crawler för sökmotorer, övervakningsverktyg och annan icke-mänsklig trafik som du kanske inte vill visa i dina analysräkningar.

Om du vill konfigurera datastream så att den använder [!DNL IAB/ABC International Spiders and Bots List] växlar du **[!UICONTROL Use IAB/ABC International Spiders and Bots List for bot detection on this datastream]** och väljer sedan Spara för att använda inställningarna för robotidentifiering på datastream.

![IAB-spindlar och robotlista har aktiverats.](assets/bot-detection/bot-detection-list.png)

### Skapa identifieringsregler för robotar {#rules}

Förutom att använda listan [IAB/ABC International Spiders and Bots ](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) kan du definiera egna robotidentifieringsregler för varje datastream.

Du kan skapa identifieringsregler för robotar baserat på **IP-adresser** och **IP-adressintervall**.

Om du behöver mer detaljerade regler för robotidentifiering kan du kombinera IP-villkoren med villkoren för begärandehuvudet. Regler för punktidentifiering kan använda följande rubriker:

| HTTP-huvud | Beskrivning |
| --- | --- |
| `user-agent` | Ett huvud som gör att servrar och nätverkspartners kan identifiera programmet, operativsystemet, leverantören och/eller versionen för den begärande användaragenten. |
| `content-type` | Anger den ursprungliga medietypen för resursen (innan någon innehållskodning används för sändning). |
| `referer` | Identifierar adressen till webbsidan som resursen har begärts från. |
| `sec-ch-ua` | Tillhandahåller varumärket och en viktig version för varje varumärke som är kopplat till webbläsaren i en kommaseparerad lista. |
| `sec-ch-ua-mobile` | Anger om webbläsaren finns på en mobil enhet. Den kan också användas av en webbläsare på datorn för att ange en inställning för en mobilanvändarupplevelse. |
| `sec-ch-ua-platform` | Anger den plattform eller det operativsystem som användaragenten körs på. Exempel: &quot;Windows&quot; eller &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Anger den version av operativsystemet som användaragenten körs på. |
| `sec-ch-ua-arch` | Tillhandahåller användaragentens underliggande processorarkitektur, som ARM eller x86. |
| `sec-ch-ua-model` | Anger den enhetsmodell som webbläsaren körs på. |
| `sec-ch-ua-bitness` | Anger &quot;bitness&quot; för användaragentens underliggande processorarkitektur. Detta är storleken i bitar av ett heltal eller en minnesadress, vanligtvis 64 eller 32 bitar. |
| `sec-ch-ua-wow64` | Anger om en användaragentbinärfil körs i 32-bitarsläge i 64-bitars Windows. |

Följ stegen nedan för att skapa en regel för identifiering av robotar:

1. Välj **[!UICONTROL Add New Rule]**.

   ![Skärmen med inställningar för punktavkänning med knappen Lägg till ny regel markerad.](assets/bot-detection/bot-detection-new-rule.png)

2. Skriv ett namn för regeln i fältet **[!UICONTROL Rule Name]**.

   ![Skärm med regler för punktidentifiering med regelnamnet markerat.](assets/bot-detection/rule-name.png)

3. Välj **[!UICONTROL Add new IP condition]** om du vill lägga till en ny IP-baserad regel. Du kan definiera regeln efter IP-adress eller efter IP-adressintervall.

   ![Skärm med regler för punktavkänning med IP-adressfältet markerat.](assets/bot-detection/ip-address-rule.png)

   ![Skärm med regler för punktavkänning med IP-intervallfältet markerat.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >IP-villkoren baseras på en logisk `OR`-åtgärd. En begäran markeras som om den kommer från en robot om den matchar något av de IP-villkor som du har definierat.

4. Om du vill lägga till rubrikvillkor i regeln väljer du **[!UICONTROL Add header conditions group]** och sedan de rubriker som du vill att regeln ska använda.

   ![Regelskärm för punktavkänning med rubrikvillkoren markerade.](assets/bot-detection/header-conditions.png)

   Lägg sedan till de villkor som ska användas för den valda rubriken.

   ![Regelskärm för punktavkänning med rubrikvillkoren markerade.](assets/bot-detection/header-condition-rule.png)

5. När du har konfigurerat de önskade objektidentifieringsreglerna väljer du **[!UICONTROL Save]** om du vill att reglerna ska tillämpas på ditt datastream.

   ![Regelskärm för punktavkänning med rubrikvillkoren markerade.](assets/bot-detection/bot-detection-save.png)


## Exempel på regler för punktavkänning {#examples}

För att hjälpa dig komma igång med robotidentifiering kan du använda de exempel som beskrivs nedan för att skapa robotidentifieringsregler.

### Punktidentifiering baserad på en IP-adress {#one-ip}

Om du vill markera alla begäranden som kommer från en viss IP-adress som robottrafik skapar du en ny regel som utvärderar en enskild IP-adress, vilket visas i bilden nedan.

![Punktavkänningsregel baserad på en IP-adress.](assets/bot-detection/bot-detection-one-ip.png)

### Punktidentifiering baserad på två IP-adresser {#two-ip}

Om du vill markera alla begäranden som kommer från någon av de två specifika IP-adresserna som Båda-trafik skapar du en ny regel för robotidentifiering som utvärderar två IP-adresser, vilket visas i bilden nedan.

![Punktavkänningsregel baserad på två IP-adresser.](assets/bot-detection/bot-detection-two-ips.png)

### Punktidentifiering baserad på ett intervall med IP-adresser {#range}

Om du vill markera alla begäranden som kommer från en viss IP-adress i ett visst intervall som robottrafik, skapar du en ny regel för identifiering av robotar som utvärderar ett helt IP-adressintervall, vilket visas i bilden nedan.

![Punktavkänningsregel baserad på IP-intervall.](assets/bot-detection/bot-detection-range.png)

### Punktavkänning baserad på en IP-adress och ett begärandehuvud {#ip-header}

Om du vill markera alla begäranden som kommer från en viss IP-adress och som innehåller en viss begäranderubrik som båda trafik, skapar du en ny regel för identifiering av robotar enligt bilden nedan.

Den här regeln kontrollerar om begäran kommer från en viss IP-adress och om begärandehuvudet `referer` börjar med `www.adobe.com`.

![Regel för punktavkänning som baseras på IP-adress och begärandehuvud.](assets/bot-detection/bot-detection-header-ip.png)

### Punktavkänning baserad på flera villkor {#multiple-conditions}

Du kan skapa regler för identifiering av robotar baserat på:

* **Flera olika villkor**: Olika villkor utvärderas som en logisk `AND`-åtgärd, vilket innebär att villkoren måste uppfyllas samtidigt för att begäran ska identifieras som om den kommer från en robot.
* **Flera villkor av samma typ**: Villkor av samma typ utvärderas som en logisk `OR`-åtgärd, vilket innebär att om något av villkoren uppfylls identifieras begäran som om den kommer från en robot.

Regeln som visas i bilden nedan identifierar en robotursprungsbegäran om följande villkor uppfylls:

Begäran kommer från någon av de två IP-adresserna, rubriken `referer` börjar med `www.adobe.com` och rubriken `sec-ch-ua-mobile` identifierar begäran som om den kommer från en webbläsare på skrivbordet.

![Punktavkänningsregel baserad på flera villkor.](assets/bot-detection/bot-detection-multiple.png)
