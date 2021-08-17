---
keywords: luftfartygsattribut;luftfartygets destination
title: Luftfartygsattribut
description: Skicka smidigt data från Adobe till Airship som målgruppsattribut för målinriktning inom Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# (Beta) [!DNL Airship Attributes]-anslutning {#airship-attributes-destination}

>[!IMPORTANT]
>
>Målet [!DNL Airship Attributes] i Adobe Experience Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

[!DNL Airship] är den ledande plattformen för kundengagemang, som hjälper er att leverera meningsfulla, personaliserade meddelanden i alla kanaler till era användare under hela kundlivscykeln.

Den här integreringen skickar profildata för Adobe till [!DNL Airship] som [Attribut](https://docs.airship.com/guides/audience/attributes/) för målinriktning eller utlösande åtgärder.

Mer information om [!DNL Airship] finns i [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Dokumentationssidan skapades av [!DNL Airship]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förutsättningar {#prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Airship] måste du:

* Aktivera attribut i ditt [!DNL Airship]-projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
>
>Skapa ett [!DNL Airship]-konto via [den här registreringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan gjort det.

## Aktivera attribut {#enable-attributes}

Adobe Experience Platform-profilattribut liknar [!DNL Airship]-attribut och kan enkelt mappas till varandra i Platform med hjälp av mappningsverktyget som visas längre ned på den här sidan.

[!DNL Airship] projekt har flera fördefinierade och standardattribut. Om du har ett anpassat attribut måste du definiera det i [!DNL Airship] först. Mer information finns i [Konfigurera och hantera attribut](https://docs.airship.com/tutorials/audience/attributes/).

## Generera innehavartoken {#bearer-token}

Gå till **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** i kontrollpanelen [Airship](https://go.airship.com) och välj **[!UICONTROL Tokens]** i den vänstra menyn.

Klicka på **[!UICONTROL Create Token]**.

Ange ett användarvänligt namn för din token, t.ex. &quot;Adobe Attributes Destination&quot;, och välj &quot;All Access&quot; för rollen.

Klicka på **[!UICONTROL Create Token]** och spara informationen konfidentiellt.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda målet [!DNL Airship Attributes] finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1

Utnyttja profildata som samlats in inom Adobe Experience Platform för att personalisera budskapet och multimediematerialet i någon av [!DNL Airship]:s kanaler. Använd till exempel [!DNL Experience Platform]-profildata för att ange platsattribut i [!DNL Airship]. På så sätt kan ett hotellmärke visa en bild för varje användares närmaste hotell.

### Använd skiftläge 2

Utnyttja attribut från Adobe Experience Platform för att ytterligare berika [!DNL Airship]-profiler och kombinera dem med SDK eller [!DNL Airship] prediktiva data. En återförsäljare kan till exempel skapa ett segment med lojalitetsstatus och platsdata (attribut från Platform) och [!DNL Airship] som förväntas ändra data för att skicka extremt målinriktade meddelanden till användare med guldlojalitetsstatus som bor i Las Vegas, NV, och som har en stor sannolikhet för att befinna sig.

## Anslut till målet {#connect}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Bearer token]**: Bearer-token som du skapade från  [!DNL Airship] instrumentpanelen.
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för det här målet.
* **[!UICONTROL Domain]**: Välj antingen ett datacenter för USA eller EU, beroende på vilket  [!DNL Airship] datacenter som gäller för detta mål.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

## Mappningsöverväganden {#mapping-considerations}

[!DNL Airship] attribut kan anges antingen på en kanal, som representerar enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har oformaterad e-postadress som primär identitet i ditt schema väljer du e-postfältet i **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship/mapping.png)

För identifierare som ska mappas till en kanal, d.v.s. en enhet, mappar du till lämplig kanal baserat på källan. Följande bilder visar hur två mappningar skapas:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS channel
* Adobe `fullName`-attribut till [!DNL Airship]-attributet &quot;Fullständigt namn&quot;

>[!NOTE]
>
>Använd det användarvänliga namnet som visas på kontrollpanelen [!DNL Airship] när du väljer målfältet för din attributmappning.

**Kartidentitet**

Välj källfält:

![Koppla till attribut för luftskepp](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Välj målfält:

![Koppla till attribut för luftskepp](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Mappningsattribut**

Välj källattribut:

![Välj källfält](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Välj målattribut:

![Välj målfält](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verifiera mappning:

![Kanalmappning](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [Datastyrningsöversikten](../../../data-governance/home.md).
