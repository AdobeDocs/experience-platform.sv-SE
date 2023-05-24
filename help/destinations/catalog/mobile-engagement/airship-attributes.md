---
keywords: luftfartygsattribut;luftfartygets destination
title: Luftfartygsattribut
description: Skicka smidigt data från Adobe till Airship som målgruppsattribut för målinriktning inom Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# [!DNL Airship Attributes] anslutning {#airship-attributes-destination}

## Översikt {#overview}

[!DNL Airship] är den ledande plattformen för kundengagemang, som hjälper er att leverera meningsfulla, personaliserade meddelanden i alla kanaler till era användare under hela kundlivscykeln.

Den här integreringen överför profildata från Adobe till [!DNL Airship] as [Attribut](https://docs.airship.com/guides/audience/attributes/) för målinriktning eller utlösande åtgärder.

Mer information om [!DNL Airship], se [Airship Docs](https://docs.airship.com).

>[!TIP]
>
>Dokumentationssidan skapades av [!DNL Airship] team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förutsättningar {#prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Airship]måste du:

* Aktivera attribut i [!DNL Airship] projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
>
>Skapa en [!DNL Airship] konto via [den här signeringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan gjort det.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn) och/eller identiteter enligt fältmappningen. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Aktivera attribut {#enable-attributes}

Adobe Experience Platform-profilattribut liknar [!DNL Airship] och kan enkelt mappas till varandra i Platform med hjälp av mappningsverktyget som visas längre ned på den här sidan.

[!DNL Airship] projekt har flera fördefinierade och standardattribut. Om du har ett anpassat attribut måste du definiera det i [!DNL Airship] först. Se [Konfigurera och hantera attribut](https://docs.airship.com/tutorials/audience/attributes/) för mer information.

## Generera innehavartoken {#bearer-token}

Gå till **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** i [Kontrollpanel för luftfartyget](https://go.airship.com) och markera **[!UICONTROL Tokens]** i den vänstra menyn.

Klicka på **[!UICONTROL Create Token]**.

Ange ett användarvänligt namn för din token, t.ex. &quot;Adobe Attributes Destination&quot;, och välj &quot;All Access&quot; för rollen.

Klicka **[!UICONTROL Create Token]** och spara informationen konfidentiellt.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Airship Attributes] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Använd skiftläge 1

Utnyttja profildata som samlats in inom Adobe Experience Platform för att personalisera budskapet och multimediematerialet inom något av [!DNL Airship]Det är kanaler. Dra nytta av [!DNL Experience Platform] profildata för att ange platsattribut i [!DNL Airship]. På så sätt kan ett hotellmärke visa en bild för varje användares närmaste hotell.

### Använd skiftläge 2

Utnyttja attribut från Adobe Experience Platform för att ytterligare berika [!DNL Airship] och kombinera det med SDK eller [!DNL Airship] prediktiva data. En återförsäljare kan till exempel skapa ett segment med lojalitetsstatus och platsdata (attribut från Platform) och [!DNL Airship] har förutsett att data kommer att ändras för att skicka extremt målinriktade meddelanden till användare med guldlojalitetsstatus som bor i Las Vegas, NV, och har en stor sannolikhet för att bli hackad.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Bearer token]**: den innehavartoken som du skapade från [!DNL Airship] kontrollpanel.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för det här målet.
* **[!UICONTROL Domain]**: välj antingen ett datacenter för USA eller EU, beroende på vilket [!DNL Airship] datacenter gäller för den här destinationen.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Mappningsöverväganden {#mapping-considerations}

[!DNL Airship] attribut kan anges antingen på en kanal, som representerar enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har e-postadresser med oformaterad text som primär identitet i ditt schema, markerar du e-postfältet i ditt **[!UICONTROL Source Attributes]** och mappa till [!DNL Airship] namngiven användare i den högra kolumnen under **[!UICONTROL Target Identities]**, vilket visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship/mapping.png)

För identifierare som ska mappas till en kanal, d.v.s. en enhet, mappar du till lämplig kanal baserat på källan. Följande bilder visar hur två mappningar skapas:

* IDFA iOS Advertising ID to an [!DNL Airship] iOS
* Adobe `fullName` attribut till [!DNL Airship] Attributet &quot;Fullständigt namn&quot;

>[!NOTE]
>
>Använd det användarvänliga namnet som visas i [!DNL Airship] när du väljer målfält för din attributmappning.

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

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](../../../data-governance/home.md).
