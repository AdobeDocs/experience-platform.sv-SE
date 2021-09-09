---
keywords: luftfartygets etikett;luftfartygets destination
title: Ansluta till luftfartygets taggar
description: Skicka smidigt data från Adobe till Airship som målgruppstaggar för målinriktning inom Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# [!DNL Airship Tags] anslutning {#airship-tags-destination}

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

## Tagggrupper

Segmentkonceptet i Adobe Experience Platform liknar [taggar](https://docs.airship.com/guides/audience/tags/) i Airship, med små implementeringsskillnader. Den här integreringen mappar statusen för en användares [medlemskap i ett Experience Platform-segment](../../../xdm/field-groups/profile/segmentation.md) till om en [!DNL Airship]-tagg finns eller inte. I ett plattformssegment där `xdm:status` ändras till `realized`, läggs taggen till i [!DNL Airship]-kanalen eller den namngivna användaren som profilen mappas till. Om `xdm:status` ändras till `exited` tas taggen bort.

Om du vill aktivera den här integreringen skapar du en *tagggrupp* i [!DNL Airship] med namnet `adobe-segments`.

>[!IMPORTANT]
>
>När du skapar din nya tagggrupp **Kontrollera inte** alternativknappen som säger &quot;[!DNL Allow these tags to be set only from your server]&quot;. Om du gör det misslyckas integreringen av Adobe-taggar.

Mer information om hur du skapar tagggruppen finns i [Hantera tagggrupper](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups).

## Generera innehavartoken

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

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Bearer token]**: Bearer-token som du skapade från  [!DNL Airship] instrumentpanelen.
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för det här målet.
* **[!UICONTROL Domain]**: Välj antingen ett datacenter för USA eller EU, beroende på vilket  [!DNL Airship] datacenter som gäller för detta mål.


## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

## Mappningsöverväganden {#mapping-considerations}

[!DNL Airship] -taggar kan anges antingen på en kanal, som representerar enhetsinstans, t.ex. iPhone, eller en namngiven användare, som mappar alla användarens enheter till en gemensam identifierare, t.ex. ett kund-ID. Om du har oformaterad e-postadress som primär identitet i ditt schema väljer du e-postfältet i **[!UICONTROL Source Attributes]** och mappar till den [!DNL Airship] namngivna användaren i den högra kolumnen under **[!UICONTROL Target Identities]**, som visas nedan.

![Mappning av namngivna användare](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

För identifierare som ska mappas till en kanal, d.v.s. en enhet, mappar du till lämplig kanal baserat på källan. Följande bilder visar hur du mappar ett Google Advertising ID till en [!DNL Airship] Android-kanal.

![Anslut till ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Airship-taggarAnslut till Airship-](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![taggarKanalmappning](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] verkställer datastyrning finns i [Datastyrningsöversikt](../../../data-governance/home.md).
