---
keywords: airship attributes;airship destination
title: Mål för luftfartygsattribut
seo-title: Mål för luftfartygsattribut
description: Skicka smidigt data från Adobe till Airship som målgruppsattribut för målinriktning inom Airship.
seo-description: Skicka smidigt data från Adobe till Airship som målgruppsattribut för målinriktning inom Airship.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---


# (Beta) [!DNL Airship Attributes] -mål {#airship-attributes-destination}

>[!IMPORTANT]
>
>Målet [!DNL Airship Attributes] i Adobe Experience Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

[!DNL Airship] är den ledande plattformen för kundengagemang, som hjälper er att leverera meningsfulla, personaliserade meddelanden i alla kanaler till era användare under hela kundlivscykeln.

Den här integreringen överför profildata från Adobe till [!DNL Airship] attribut [](https://docs.airship.com/guides/audience/attributes/) för målinriktning eller utlösning.

Mer information [!DNL Airship]finns i [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Den här dokumentationssidan skapades av [!DNL Airship] teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förutsättningar {#prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Airship]måste du:

* Aktivera attribut i ditt [!DNL Airship] projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
>
>Skapa ett [!DNL Airship] konto via [den här registreringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan gjort det.

### Aktivera attribut {#enable-attributes}

Adobe Experience Platform-profilattribut liknar [!DNL Airship] attribut och kan enkelt mappas till varandra i Platform med hjälp av mappningsverktyget som visas längre fram på den här sidan.

[!DNL Airship] projekt har flera fördefinierade och standardattribut. Om du har ett anpassat attribut måste du definiera det i [!DNL Airship] början. Mer information finns i [Konfigurera och hantera attribut](https://docs.airship.com/tutorials/audience/attributes/) .

### Bearer-token {#bearer-token}

1. Gå till **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** på kontrollpanelen för [luftskepp](https://go.airship.com) och välj **[!UICONTROL Tokens]** i den vänstra menyn.
1. Klicka på **[!UICONTROL Create Token]**.
1. Ange ett användarvänligt namn för din token, t.ex. &quot;Adobe Attributes Destination&quot;, och välj &quot;All Access&quot; för rollen.
1. Klicka **[!UICONTROL Create Token]** och spara informationen konfidentiellt.


## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Airship Attributes] destinationen finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Använd skiftläge 1

Utnyttja profildata som samlats in inom Adobe Experience Platform för personalisering av budskapet och multimediematerial i någon av [!DNL Airship]dess kanaler. Använd till exempel [!DNL Experience Platform] profildata för att ange platsattribut i [!DNL Airship]. På så sätt kan ett hotellmärke visa en bild för varje användares närmaste hotell.

### Använd skiftläge 2

Utnyttja attribut från Adobe Experience Platform för att ytterligare berika [!DNL Airship] profiler och kombinera dem med SDK eller [!DNL Airship] prediktiva data. En återförsäljare kan t.ex. skapa ett segment med lojalitetsstatus och platsdata (attribut från Platform) och [!DNL Airship] förutspås omdirigera data för att skicka extremt målinriktade meddelanden till användare med guldlojalitetsstatus som bor i Las Vegas, NV, och som har stor sannolikhet för kurning.

## Anslut till [!DNL Airship Attributes] {#connect-airship-attributes}

1. Bläddra till **[!UICONTROL Destinations]** kategorin i **[!UICONTROL Catalog]**> **[!UICONTROL Mobile Engagement]** . Markera **[!DNL Airship Attributes]** och markera sedan **[!UICONTROL Configure]**.

   >[!NOTE]
   >
   >Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

   ![Koppla till attribut för luftskepp](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. Om du tidigare har konfigurerat en anslutning till ditt **mål i** kontosteget [!DNL Airship Attributes] markerar du **[!UICONTROL Existing Account]** och väljer den befintliga anslutningen. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till [!DNL Airship Attributes]. Välj **[!UICONTROL Connect to destination]** att ansluta Adobe Experience Platform till ditt [!DNL Airship] projekt med den innehavartoken som du skapade från [!DNL Airship] instrumentpanelen.

   >[!NOTE]
   >
   >Adobe Experience Platform stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt [!DNL Airship] konto. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Koppla till attribut för luftskepp](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. När dina inloggningsuppgifter har bekräftats och Adobe Experience Platform är anslutet till ditt [!DNL Airship] projekt kan du välja **[!UICONTROL Next]** att fortsätta till **[!UICONTROL Setup]** steget.

4. I **[!UICONTROL Authentication]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet. <br> I det här steget kan du även välja datacenter i USA eller EU beroende på vilket [!DNL Airship] datacenter som gäller för det här målet. Välj slutligen ett eller flera användningsfall för marknadsföring för vilka data ska exporteras till målet. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa egna. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions). <br> Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Koppla till attribut för luftskepp](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet.

## Aktivera segment {#activate-segments}

Så här aktiverar du segment till [!DNL Airship Attributes]:

1. I **[!UICONTROL Destinations > Browse]** väljer du det [!DNL Airship Attributes] mål där du vill aktivera segmenten.
   ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. Klicka på målets namn. Då kommer du till aktiveringsflödet.
Observera att om det redan finns ett aktiveringsflöde för ett mål kan du se de segment som för närvarande skickas till målet. Välj **[!UICONTROL Edit activation]** i den högra listen och följ stegen nedan för att ändra aktiveringsinformationen. ![activate-flow](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. Välj **[!UICONTROL Activate]**;
1. I **[!UICONTROL Activate destination]** arbetsflödet på **[!UICONTROL Select Segments]** sidan väljer du vilka segment som ska skickas till [!DNL Airship Attributes].
   ![segment-till-mål](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. I **[!UICONTROL Mapping]** steget väljer du vilka attribut och identiteter från [XDM](https://docs.adobe.com/content/help/sv-SE/experience-platform/xdm/home.html) -schemat som ska mappas till målschemat. Välj **[!UICONTROL Add new mapping]** att bläddra i schemat och mappa dem till motsvarande målidentitet.
   ![inledande skärm för identitetsmappning](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] attribut kan anges antingen på en kanal, som representerar enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har oformaterad text (ej hash-kodade) e-postadresser som primär identitet i ditt schema, markerar du e-postfältet i ditt schema **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.
   ![Mappning](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)av namngivna användare För identifierare som ska mappas till en kanal, dvs. en enhet, mappas till lämplig kanal baserat på källan. Följande bilder visar hur två mappningar skapas:

   * IDFA iOS Advertising ID to an [!DNL Airship] iOS channel
   * Adobe-attribut `fullName` till [!DNL Airship] attributet &quot;Fullständigt namn&quot;

   >[!NOTE]
   >
   >Använd det användarvänliga namnet som visas på [!DNL Airship] instrumentpanelen när du väljer målfältet för din attributmappning.

   **Mappa identitet**Välj källfält:
   ![Anslut till attribut](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)för luftskepp Välj målfält:
   ![Koppla till attribut för luftskepp](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **Mappningsattribut**

   Välj källattribut:
   ![Välj källfält](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)Välj målattribut:
   ![Välj målfält](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)Bekräfta mappning:
   ![Kanalmappning](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. Schemaläggning är för närvarande inaktiverat på **[!UICONTROL Segment schedule]** sidan. Klicka **[!UICONTROL Next]** för att fortsätta till granskningssteget. ![Schemaläggning är för närvarande inaktiverad](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. På **[!UICONTROL Review]** sidan visas en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta urvalet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](/help/rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![bekräfta-val](/help/rtcdp/destinations/assets/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![recension](/help/rtcdp/destinations/assets/airship11-review-step.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] mål följer dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] datastyrning används finns i [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md)i realtid.
