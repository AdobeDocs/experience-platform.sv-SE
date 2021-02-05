---
keywords: luftfartygets etikett;luftfartygets destination
title: Anslutningsmål för luftfartygets taggar
description: Skicka smidigt data från Adobe till Airship som målgruppstaggar för målinriktning inom Airship.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---


# (Beta) [!DNL Airship Tags] anslutning {#airship-tags-destination}

>[!IMPORTANT]
>
>Målet [!DNL Airship Tags] i Adobe Experience Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt

[!DNL Airship] är den ledande plattformen för kundengagemang, som hjälper er att leverera meningsfulla, personaliserade meddelanden i alla kanaler till era användare under hela kundlivscykeln.

Den här integreringen överför Adobe Experience Platform segmentdata till [!DNL Airship] som [taggar](https://docs.airship.com/guides/audience/tags/) för målinriktning eller utlösande.

Mer information om [!DNL Airship] finns i [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Dokumentationssidan skapades av [!DNL Airship]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [support.airship.com](https://support.airship.com/).

## Förutsättningar

Innan du kan skicka dina Adobe Experience Platform-segment till [!DNL Airship] måste du:

* Skapa en tagggrupp i ditt [!DNL Airship]-projekt.
* Generera en innehavartoken för autentisering.

>[!TIP]
> 
>Skapa ett [!DNL Airship]-konto via [den här registreringslänken](https://go.airship.eu/accounts/register/plan/starter/) om du inte redan gjort det.

### Tagggrupper

Segmentkonceptet i Adobe Experience Platform liknar [taggar](https://docs.airship.com/guides/audience/tags/) i Airship, med små implementeringsskillnader. Den här integreringen mappar statusen för en användares [medlemskap i ett Experience Platform-segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) till om en [!DNL Airship]-tagg finns eller inte. I ett plattformssegment där `xdm:status` ändras till `realized`, läggs taggen till i [!DNL Airship]-kanalen eller den namngivna användaren som profilen mappas till. Om `xdm:status` ändras till `exited` tas taggen bort.

Om du vill aktivera den här integreringen skapar du en *tagggrupp* i [!DNL Airship] med namnet `adobe-segments`.

>[!IMPORTANT]
>
>När du skapar din nya tagggrupp **Kontrollera inte** alternativknappen som säger &quot;[!DNL Allow these tags to be set only from your server]&quot;. Om du gör det misslyckas integreringen av Adobe-taggar.

Mer information om hur du skapar tagggruppen finns i [Hantera tagggrupper](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups).

### Bearer-token

Gå till **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** i kontrollpanelen [Airship](https://go.airship.com) och välj **[!UICONTROL Tokens]** i den vänstra menyn.

Klicka på **[!UICONTROL Create Token]**.

Ange ett användarvänligt namn för din token, t.ex. &quot;Adobe Tags Destination&quot;, och välj &quot;All Access&quot; för rollen.

Klicka på **[!UICONTROL Create Token]** och spara informationen konfidentiellt.

## Användningsfall

För att du bättre ska förstå hur och när du ska använda målet [!DNL Airship Tags] finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Använd skiftläge 1

Återförsäljare eller underhållningsplattformar kan skapa användarprofiler för sina lojalitetskunder och skicka dessa segment till [!DNL Airship] för att rikta meddelanden till mobilkampanjer.

### Använd skiftläge 2

Utlös personliga meddelanden i realtid när användare faller in i eller ut ur specifika segment inom Adobe Experience Platform.

En återförsäljare skapar till exempel ett jeans-specifikt segment i Platform. Den återförsäljaren kan nu utlösa ett mobilt meddelande så snart någon sätter sina jeans-preferenser för ett visst varumärke.

## Anslut till [!DNL Airship Tags] {#connect-airship-tags}

Bläddra till kategorin **[!UICONTROL Mobile Engagement]** i **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Välj **[!DNL Airship Tags]** och sedan **[!UICONTROL Configure]**.

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

![Anslut till luftfartygets taggar](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

Om du tidigare har konfigurerat en anslutning till ditt [!DNL Airship Tags]-mål väljer du **[!UICONTROL Existing Account]** och väljer din befintliga anslutning i steget **Konto**. Du kan också välja **[!UICONTROL New Account]** för att konfigurera en ny anslutning till [!DNL Airship Tags]. Välj **[!UICONTROL Connect to destination]** om du vill ansluta Adobe Experience Platform till ditt [!DNL Airship]-projekt med bearer-token som du skapade från kontrollpanelen [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för ditt [!DNL Airship]-konto. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

![Anslut till luftfartygets taggar](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

När dina inloggningsuppgifter har bekräftats och Adobe Experience Platform är anslutet till ditt [!DNL Airship]-projekt kan du välja **[!UICONTROL Next]** för att fortsätta till **[!UICONTROL Setup]**-steget.

I steget **[!UICONTROL Authentication]** anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet.

I det här steget kan du även välja ett datacenter i USA eller EU, beroende på vilket [!DNL Airship] datacenter som gäller för det här målet. Välj slutligen ett eller flera användningsfall för marknadsföring för vilka data ska exporteras till målet. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa egna. Mer information om användningsfall för marknadsföring finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

![Anslut till luftfartygets taggar](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller välja **[!UICONTROL Next]** om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet.

## Aktivera segment {#activate-segments}

Så här aktiverar du segment till [!DNL Airship Tags]:

I **[!UICONTROL Destinations > Browse]** väljer du det [!DNL Airship Tags]-mål där du vill aktivera dina segment.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Klicka på målets namn. Då kommer du till aktiveringsflödet.

Observera att om det redan finns ett aktiveringsflöde för ett mål kan du se de segment som för närvarande skickas till målet. Välj **[!UICONTROL Edit activation]** till höger och följ stegen nedan för att ändra aktiveringsinformationen.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Välj **[!UICONTROL Activate]**. På sidan **[!UICONTROL Activate destination]** i arbetsflödet väljer du vilka segment som ska skickas till [!DNL Airship Tags].**[!UICONTROL Select Segments]**

![segment-till-mål](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

I steget **[!UICONTROL Mapping]** väljer du vilka attribut och identiteter från schemat [XDM](../../../xdm/home.md) som ska mappas till målschemat. Välj **[!UICONTROL Add new mapping]** om du vill bläddra i schemat och mappa dem till motsvarande målidentitet.

![inledande skärm för identitetsmappning](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] -taggar kan anges antingen på en kanal, som representerar enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har oformaterad e-postadress som primär identitet i ditt schema väljer du e-postfältet i **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

För identifierare som ska mappas till en kanal, d.v.s. en enhet, mappar du till lämplig kanal baserat på källan. Följande bilder visar hur du mappar ett Google Advertising ID till en [!DNL Airship] Android-kanal.

![Anslut till ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Airship-taggarAnslut till Airship-](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![taggarKanalmappning](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

Schemaläggning är för närvarande inaktiverat på sidan **[!UICONTROL Segment schedule]**. Klicka på **[!UICONTROL Next]** för att fortsätta till granskningssteget.

På sidan **[!UICONTROL Review]** visas en sammanfattning av ditt val. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta valet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../../data-governance/enforcement/auto-enforcement.md) i dokumentationsavsnittet för datastyrning.

![bekräfta-val](../../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![bekräfta-val](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] verkställer datastyrning finns i [Datastyrningsöversikt](../../../data-governance/home.md).

