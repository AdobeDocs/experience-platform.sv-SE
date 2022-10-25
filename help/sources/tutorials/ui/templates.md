---
keywords: Experience Platform;hemmabruk;populära ämnen;
description: Adobe Experience Platform tillhandahåller förkonfigurerade mallar som du kan använda för att snabba upp dataöverföringsprocessen. Mallar innehåller automatiskt genererade resurser som scheman, datauppsättningar, mappningsregler, ID-namnutrymmen och dataflöden som du kan använda när du hämtar data från en källa till Experience Platform.
title: (Alfa) Skapa ett källdataflöde med hjälp av mallar i användargränssnittet
hide: true
hidefromtoc: true
source-git-commit: a0ca9cff43b6f8276268467fecf944c664992950
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# (Alfa) Skapa ett källdataflöde med hjälp av mallar i användargränssnittet

>[!IMPORTANT]
>
>Mallarna är i Alfa och stöds för närvarande bara av [[!DNL Marketo Engage] källa](../../connectors/adobe-applications/marketo/marketo.md). Dokumentationen och funktionerna kan komma att ändras.

Adobe Experience Platform tillhandahåller förkonfigurerade mallar som du kan använda för att snabba upp dataöverföringsprocessen. Mallar innehåller automatiskt genererade resurser som scheman, datauppsättningar, mappningsregler, ID-namnutrymmen och dataflöden som du kan använda när du hämtar data från en källa till Experience Platform.

Med mallar kan man

* Minska tiden till värdet av intag genom att accelerera skapandet av XML-baserade resurser.
* Minimera antalet fel som kan uppstå under den manuella dataöverföringsprocessen.
* Uppdatera automatiskt genererade resurser när som helst för att passa dina användningsexempel.

I följande självstudie beskrivs hur du använder mallar i användargränssnittet för plattformen med hjälp av [[!DNL Marketo Engage] källa](../../connectors/adobe-applications/marketo/marketo.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Använda mallar i plattformens användargränssnitt {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Välj affärstyp"
>abstract="Välj lämplig affärstyp för ditt användningsfall. Åtkomsten kan variera beroende på ditt Real-time Customer Data Platform-prenumerationskonto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=sv" text="Real-Time CDP - översikt"

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som kan användas för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Adobe applications] kategori, välj **[!UICONTROL Marketo Engage]** och sedan markera **[!UICONTROL Add data]**.

![En katalog över källarbetsytan med Marketo Engage-källan markerad.](../../images/tutorials/templates/catalog.png)

Ett popup-fönster visas där du kan bläddra bland mallar eller använda befintliga scheman och datauppsättningar. Om du vill använda automatiskt genererade resurser väljer du **[!UICONTROL Browse templates]** och sedan markera **[!UICONTROL Select]**.

![Ett popup-fönster med alternativ för att bläddra bland mallar eller använda befintliga resurser.](../../images/tutorials/templates/browse-templates.png)

### Autentisering

Autentiseringssteget visas och du uppmanas att antingen skapa ett nytt konto eller använda ett befintligt konto.

#### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!UICONTROL Existing account] och välj sedan det konto som du vill använda i listan som visas.

![Urvalssidan för ett befintligt konto med en lista över befintliga konton som du kan komma åt.](../../images/tutorials/templates/existing-account.png)

#### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan din källanslutningsinformation och autentiseringsuppgifter för kontot. När du är klar väljer du **[!UICONTROL Connect to source]** så att den nya anslutningen kan upprättas.

![Autentiseringssidan för ett nytt konto med källanslutningsinformation och autentiseringsuppgifter för kontot.](../../images/tutorials/templates/new-account.png)

### Välj mallar

När du har autentiserat och valt ditt konto visas en lista med mallar. Välj förhandsgranskningsikonen bredvid ett mallnamn om du vill förhandsgranska exempeldata från mallen.

![En lista med mallar med förhandsgranskningsikonen markerad.](../../images/tutorials/templates/templates.png)

Förhandsgranskningsfönstret visas så att du kan utforska och inspektera exempeldata från mallen. När du är klar väljer du **[!UICONTROL Got it]**.

![Fönstret med exempeldata för förhandsgranskning.](../../images/tutorials/templates/preview-sample-data.png)

Välj sedan den mall du vill använda i listan. Du kan välja flera mallar och skapa flera dataflöden samtidigt. En mall kan dock bara användas en gång per konto. När du har valt mallar väljer du **[!UICONTROL Finish]** så att resurserna kan genereras en stund.

![Listan med mallar med mallen för säljprojektskontaktroll vald.](../../images/tutorials/templates/select-template.png)

### Granska resurser {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Granska dina automatiskt genererade resurser"
>abstract="Det kan ta upp till fem minuter att generera alla resurser. Om du väljer att lämna sidan får du ett meddelande som returneras när resurserna är klara. Du kan granska resurserna när de har skapats och göra ytterligare konfigurationer av dataflödet när som helst."

The [!UICONTROL Review template assets] visas de resurser som genereras automatiskt som en del av mallen. På den här sidan kan du visa de automatiskt genererade scheman, datauppsättningar, identitetsnamnutrymmen och dataflöden som är kopplade till din källanslutning.

Automatiskt genererade dataflöden är aktiverade som standard. Markera ellipserna (`...`) bredvid dataflödets namn och välj **[!UICONTROL Preview mappings]** om du vill visa de mappningsuppsättningar som har skapats för dataflödet.

![Ett rullgardinsfönster med alternativet Förhandsvisa mappningar markerat.](../../images/tutorials/templates/preview.png)

En förhandsgranskningssida visas där du kan kontrollera mappningsförhållandet mellan källdatafälten och målschemafälten. När du har tittat på dataflödets mappningar. Välj **[!UICONTROL Got it.]**

![Förhandsgranskningsfönstret för mappningen.](../../images/tutorials/templates/preview-mappings.png)

Du kan uppdatera dataflödena när som helst efter körningen. Markera ellipserna (`...`) bredvid dataflödets namn och välj **[!UICONTROL Update dataflow]**. Du dirigeras till arbetsflödessidan för källor där du kan uppdatera dina dataflödesdetaljer, inklusive inställningar för partiellt intag, feldiagnostik och varningsmeddelanden samt mappning av dataflöde.

![Ett rullgardinsfönster med alternativet för att uppdatera dataflöden markerat.](../../images/tutorials/templates/update.png)

## Nästa steg

Genom att följa den här självstudiekursen har du nu skapat dataflöden och resurser som scheman, datauppsättningar och identitetsnamnutrymmen med hjälp av mallar. Allmän information om källor finns på [källöversikt](../../home.md).
