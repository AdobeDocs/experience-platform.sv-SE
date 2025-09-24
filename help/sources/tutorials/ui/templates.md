---
description: Lär dig hur du använder mallar i Adobe Experience Platform användargränssnitt för att snabba upp dataöverföringsprocessen för B2B-data.
title: Skapa ett källdataflöde med mallar i användargränssnittet
badge1: Beta
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: 02a22362b9ecbfc5fd7fcf17dc167309a0ea45d5
workflow-type: tm+mt
source-wordcount: '2271'
ht-degree: 0%

---

# Skapa ett källdataflöde med mallar i användargränssnittet {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Mallar för källor i Experience Platform UI"
>abstract="Mallar innehåller automatiskt genererade resurser som scheman, datauppsättningar, identiteter, mappningsregler, identitetsnamnutrymmen och dataflöden som du kan använda när du hämtar in data från en källa till Experience Platform. Du kan uppdatera automatiskt genererade resurser för anpassning så att de passar dina användningsexempel."

>[!IMPORTANT]
>
>Mallarna är i betaversion och stöds av följande källor:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>Dokumentationen och funktionerna kan komma att ändras.

Adobe Experience Platform tillhandahåller förkonfigurerade mallar som du kan använda för att snabba upp dataöverföringsprocessen. Mallar innehåller automatiskt genererade resurser som scheman, datauppsättningar, identiteter, mappningsregler, identitetsnamnutrymmen och dataflöden som du kan använda när du hämtar in data från en källa till Experience Platform.

Med mallar kan man

* Minska tiden till värdet av intag genom att accelerera skapandet av komplexa resurser.
* Minimera antalet fel som kan uppstå under den manuella dataöverföringsprocessen.
* Uppdatera automatiskt genererade resurser när som helst för att passa dina användningsexempel.

I följande självstudiekurs beskrivs hur du använder mallar i användargränssnittet i Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Använda mallar i Experience Platform användargränssnitt {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Välj affärstyp"
>abstract="Välj lämplig affärstyp för ditt användningsfall. Åtkomsten kan variera beroende på ditt Real-Time Customer Data Platform-prenumerationskonto."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html" text="Real-Time CDP - översikt"

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources] och visa en katalog med tillgängliga källor i Experience Platform.

Använd menyn *[!UICONTROL Categories]* för att filtrera källor efter kategori. Du kan också ange ett källnamn i sökfältet för att hitta en viss källa från katalogen.

Gå till kategorin [!UICONTROL Adobe applications] för att se källkortet [!DNL Marketo Engage] och välj sedan [!UICONTROL Add data] för att börja.

![En katalog på källarbetsytan med Marketo Engage-källan markerad.](../../images/tutorials/templates/catalog.png)

Ett popup-fönster visas där du kan bläddra bland mallar eller använda befintliga scheman och datauppsättningar.

* **Bläddra bland mallar**: Källmallar skapar automatiskt scheman, identiteter, datauppsättningar och dataflöden med mappningsregler åt dig. Du kan anpassa dessa resurser efter behov.
* **Använd mina befintliga resurser**: Importera dina data med befintliga datauppsättningar och scheman som du har skapat. Du kan också skapa nya datauppsättningar och scheman vid behov.

>[!NOTE]
>
>Mallar kan automatiskt generera modellbaserade scheman när de arbetar med källor som kräver arbetsflöden för datainhämtning eller stöder flera datamodeller. Dessa scheman möjliggör Data Mirror-funktioner för datasynkronisering i realtid.\
>När du använder mallar med modellbaserade scheman, kommer de automatiskt genererade resurserna att innehålla den nödvändiga primärnyckeln, versionsidentifieraren och tidsstämpelidentifierarfälten.\
>Mer information finns i [Data Mirror översikt](../../../xdm/data-mirror/overview.md) och [modellbaserade scheman, teknisk referens](../../../xdm/schema/model-based.md).

Om du vill använda automatiskt genererade resurser väljer du **[!UICONTROL Browse templates]** och sedan **[!UICONTROL Select]**.

![Ett popup-fönster med alternativ för att bläddra bland mallar eller använda befintliga resurser.](../../images/tutorials/templates/browse-templates.png)

### Autentisering

Autentiseringssteget visas och du uppmanas att antingen skapa ett nytt konto eller använda ett befintligt konto.

>[!BEGINTABS]

>[!TAB Använd ett befintligt konto]

Om du vill använda ett befintligt konto väljer du [!UICONTROL Existing account] och sedan det konto som du vill använda i listan som visas.

![Markeringssidan för ett befintligt konto med en lista över befintliga konton som du kan komma åt.](../../images/tutorials/templates/existing-account.png)

>[!TAB Skapa ett nytt konto]

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan din källanslutningsinformation och autentiseringsuppgifter för kontot. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt lite tid för att upprätta den nya anslutningen.

![Autentiseringssidan för ett nytt konto med källanslutningsinformation och autentiseringsuppgifter för kontot.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Välj mallar

När ditt konto är autentiserat kan du nu välja den mall som du vill använda för ditt dataflöde.

+++[!DNL Marketo Engage] mallar
I följande tabell visas mallarna som är tillgängliga för källan [!DNL Marketo Engage].

| [!DNL Marketo Engage] mallar | Beskrivning |
| --- | --- |
| Aktiviteter | Mallen för aktiviteter innehåller händelsebaserade ögonblicksbilder av aktiviteter som e-postinteraktioner, webbplatsinteraktioner och försäljningssamtal. |
| Företag | I företagsmallen hämtas företagskontoinformation som företagsinformation, plats och faktureringsinformation. |
| Namngivna konton | Mallen Namngivna konton innehåller information om konton som har fastställts som målkonton att fortsätta. |
| Möjligheter | Mallen Affärsmöjligheter innehåller affärsmöjlighetsinformation som typ, försäljningsfas och relaterade konton. |
| Roller för säljprojektskontakt | Mallen Roller för säljprojektskontakt innehåller information om rollerna för leads som är associerade med en viss affärsmöjlighet. |
| Personer | Mallen Personer innehåller attribut för enskilda personer, t.ex. demografisk information, kontaktinformation och medgivanden. |
| Programmedlemskap | Mallen för programmedlemskap innehåller information om kontakter som är kopplade till en företagskampanj, inklusive vårdstånd och kontaktsvar. |
| Program | Mallen Program innehåller information om företagskampanjer, som status, kanaler, tidslinjer och kostnader. |
| Statiska listmedlemskap | Mallen Statiska listmedlemskap samlar relationerna mellan människor och deras medlemskap i statiska listor. |
| Statiska listor | Mallen Statisk lista innehåller instansierade listor med personer för olika användningsområden. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2B-mallar
Följande tabell visar vilka B2B-mallar som är tillgängliga för källan [!DNL Salesforce].

| [!DNL Salesforce] B2B-mallar | Beskrivning |
| --- | --- |
| Kontokontaktrelation | Mallen för kontokontaktrelation hämtar relationen mellan en kontakt och ett eller flera konton. |
| Konton | Kontomallen innehåller företagskontoinformation som företagsinformation, plats och faktureringsinformation. |
| Kampanjmedlemmar | Mallen Kampanjmedlemmar fångar relationen mellan en enskild lead eller kontakt och en viss [!DNL Salesforce]-kampanj. |
| Kampanjer | I Campaigns-mallen samlas information om företagskonton in, t.ex. företagsinformation, plats och faktureringsinformation. |
| Kontakter | Kontaktmallen hämtar attribut för kontakter, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |
| Leads | Mallen Leads innehåller attribut för leads som demografisk information, kontaktinformation och relaterade affärsenheter. |
| Möjligheter | Mallen Affärsmöjligheter innehåller affärsmöjlighetsinformation som typ, försäljningsfas och relaterat konto. |
| Roller för säljprojektskontakt | Mallen Roller för säljprojektskontakt innehåller information om rollerna för leads som är associerade med en viss affärsmöjlighet. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] B2C-mallar
Följande tabell visar vilka B2C-mallar som är tillgängliga för källan [!DNL Salesforce].

| [!DNL Salesforce] B2C-mallar | Beskrivning |
| --- | --- |
| Kontakt | Kontaktmallen hämtar attribut för kontakter, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |
| Lead | Leadmallen hämtar attribut för leads, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2B-mallar
Följande tabell visar vilka B2B-mallar som är tillgängliga för källan [!DNL Microsoft Dynamics].

| [!DNL Microsoft Dynamics] B2B-mallar | Beskrivning |
| --- | --- |
| Konton | Kontomallen innehåller företagskontoinformation som företagsinformation, plats och faktureringsinformation. |
| Kampanjer | I Campaigns-mallen samlas information om företagskonton in, t.ex. företagsinformation, plats och faktureringsinformation. |
| Kontakter | Kontaktmallen hämtar attribut för kontakter, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |
| Leads | Mallen Leads innehåller attribut för leads som demografisk information, kontaktinformation och relaterade affärsenheter. |
| Marknadsföringslista | Mallen Marknadsföringslista innehåller en grupp befintliga eller potentiella kunder som skapats för en marknadsföringskampanj eller andra försäljningssyften. |
| Medlemmar i marknadsföringslista | Medlemmar i marknadsföringslistan samlar in information om en viss typ av kundpost, t.ex. leads, konton eller kontakter, i en marknadsföringslista. |
| Möjligheter | Mallen Affärsmöjligheter innehåller affärsmöjlighetsinformation som typ, försäljningsfas och relaterat konto. |
| Roller för säljprojektskontakt | Mallen Roller för säljprojektskontakt innehåller information om rollerna för leads som är associerade med en viss affärsmöjlighet. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] B2C-mallar
Följande tabell visar vilka B2C-mallar som är tillgängliga för källan [!DNL Microsoft Dynamics].

| [!DNL Microsoft Dynamics] B2C-mallar | Beskrivning |
| --- | --- |
| Kontakt | Kontaktmallen hämtar attribut för kontakter, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |
| Lead | Leadmallen hämtar attribut för leads, t.ex. demografisk information, kontaktinformation och relaterade affärsenheter. |

{style="table-layout:auto"}

+++

Beroende på vilken affärstyp du har valt visas en lista med mallar. Välj förhandsgranskningsikonen ![förhandsgranskningsikonen](/help/images/icons/preview.png) bredvid ett mallnamn om du vill förhandsgranska exempeldata från mallen.

![En lista med mallar med förhandsgranskningsikonen markerad.](../../images/tutorials/templates/templates.png)

Förhandsgranskningsfönstret visas så att du kan utforska och inspektera exempeldata från mallen. När du är klar väljer du **[!UICONTROL Got it]**.

![Fönstret med exempeldata för förhandsgranskning.](../../images/tutorials/templates/preview-sample-data.png)

Välj sedan den mall som du vill använda i listan. Du kan välja flera mallar och skapa flera dataflöden samtidigt. En mall kan dock bara användas en gång per konto. När du har valt dina mallar väljer du **[!UICONTROL Finish]** och tillåt en stund för resurserna att generera.

Om du väljer ett eller flera objekt i listan med tillgängliga mallar kommer alla B2B-scheman och identitetsnamnutrymmen fortfarande att genereras för att säkerställa att B2B-relationer mellan scheman konfigureras korrekt.

>[!NOTE]
>
>Mallar som redan har använts inaktiveras.

![Listan med mallar med mallen för säljprojektskontaktroll vald.](../../images/tutorials/templates/select-template.png)

### Ange ett schema

Källorna [!DNL Microsoft Dynamics] och [!DNL Salesforce] har båda stöd för schemaläggning av dataflöden.

Använd schemaläggningsgränssnittet för att konfigurera ett matningsschema för dataflödena. Ställ in din matningsfrekvens på **En gång** för att skapa ett engångsintag.

![Planeringsgränssnittet för Dynamics- och Salesforce-mallar.](../../images/tutorials/templates/schedule.png)

Du kan också ange att din matningsfrekvens ska vara **Minut**, **Timme**, **Dag** eller **Vecka**. Om du schemalägger dataflödet för flera frågor måste du ange ett intervall för att skapa en tidsram mellan varje intag. En matningsfrekvens som till exempel är inställd på **Timme** och ett intervall som är inställt på **15** innebär att dataflödet schemaläggs att importera data var **15:e timme**.

Under det här steget kan du även aktivera **bakgrundsfyllning** och definiera en kolumn för inkrementellt dataintag. Backfill används för att importera historiska data, medan kolumnen som du definierar för inkrementellt intag gör att nya data kan skiljas från befintliga data.

Välj **[!UICONTROL Finish]** när du har slutfört konfigurationen av ditt intag.

![Schemaläggningsgränssnittet för Dynamics- och Salesforce-mallar med bakåtfyllning aktiverat.](../../images/tutorials/templates/backfill.png)

### Granska resurser {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Granska dina automatiskt genererade resurser"
>abstract="Det kan ta upp till fem minuter att generera alla resurser. Om du väljer att lämna sidan får du ett meddelande som returneras när resurserna är klara. Du kan granska resurserna när de har skapats och göra ytterligare konfigurationer av dataflödet när som helst."

På sidan [!UICONTROL Review template assets] visas de resurser som har genererats automatiskt som en del av mallen. På den här sidan kan du visa de automatiskt genererade scheman, datauppsättningar, identitetsnamnutrymmen och dataflöden som är kopplade till din källanslutning. Det kan ta upp till fem minuter att generera alla resurser. Om du väljer att lämna sidan får du ett meddelande som returneras när resurserna är klara. Du kan granska resurserna när de har skapats och göra ytterligare konfigurationer av dataflödet när som helst.

Som standard är automatiskt genererade dataflöden inställda på ett utkasttillstånd för att tillåta ytterligare anpassning av konfigurationer, som mappningsregler eller schemalagda frekvenser. Markera ellipserna (`...`) bredvid dataflödets namn och välj sedan **[!UICONTROL Preview mappings]** för att visa de mappningsuppsättningar som har skapats för dataflödet.

![Ett rullgardinsfönster med alternativet Förhandsvisa mappningar markerat.](../../images/tutorials/templates/preview.png)

En förhandsgranskningssida visas där du kan kontrollera mappningsförhållandet mellan källdatafälten och målschemafälten. När du har tittat på dataflödets mappningar. Välj **[!UICONTROL Got it.]**

![Förhandsgranskningsfönstret för mappningen.](../../images/tutorials/templates/preview-mappings.png)

Du kan uppdatera dataflödena när som helst efter körningen. Markera ellipserna (`...`) bredvid dataflödets namn och välj sedan **[!UICONTROL Update dataflow]**. Du dirigeras till arbetsflödessidan för källor där du kan uppdatera dina dataflödesdetaljer, inklusive inställningar för partiellt intag, feldiagnostik och varningsmeddelanden samt mappning av dataflöde.

Du kan använda schemaredigeringsvyn för att göra uppdateringar i det automatiskt genererade schemat. Mer information finns i guiden för [med schemaredigeraren](../../../xdm/tutorials/create-schema-ui.md).

![Ett rullgardinsfönster med alternativet för att uppdatera dataflöden markerat.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>Du kan komma åt dataflödet för utkastet via katalogsidan [!UICONTROL Dataflows] på källarbetsytan. Välj **[!UICONTROL Dataflows]** i det övre huvudet och välj sedan det dataflöde som du vill uppdatera från listan.
>
>![En lista över befintliga dataflöden i dataflödeskatalogen för källarbetsytan.](../../images/tutorials/templates/dataflows.png)

### Publicera dataflödet

Börja publiceringsprocessen genom att gå igenom källarbetsflödet. När du har valt [!UICONTROL Update dataflow] dirigeras du till arbetsflödets *[!UICONTROL Add data]*-steg. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Steget Lägg till data för ett dataflöde ](../../images/tutorials/templates/continue-draft.png)

Bekräfta sedan dataflödesinformationen och konfigurera inställningarna för feldiagnostik, partiell import och varningsmeddelanden. När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödets detaljsteg för ett dataflöde.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>Du kan när som helst välja **[!UICONTROL Save as draft]** för att stoppa och spara de ändringar du har gjort i dataflödet.

Mappningssteget visas. Under det här steget kan du konfigurera om mappningskonfigurationerna för ditt dataflöde. En utförlig guide om de förinställningsfunktioner som används för mappning finns i [användargränssnittshandboken för dataförinställningar](../../../data-prep/ui/mapping.md).

![Mappningssteget för ett dataflöde.](../../images/tutorials/templates/mapping.png)

Granska slutligen informationen om dataflödet och välj sedan **[!UICONTROL Save & ingest]** för att publicera utkastet.

![Granskningssteget för ett dataflöde för utkast.](../../images/tutorials/templates/review.png)

## Nästa steg

Genom att följa den här självstudiekursen har du nu skapat dataflöden och resurser som scheman, datauppsättningar och identitetsnamnutrymmen med hjälp av mallar. Allmän information om källor finns i [Källöversikt](../../home.md).

## Varningar och meddelanden {#alerts-and-notifications}

Mallar stöds av Adobe Experience Platform Alerts och du kan använda meddelandepanelen för att få uppdateringar om statusen för dina resurser och även för att gå tillbaka till granskningssidan.

Markera meddelandeikonen i det övre sidhuvudet i Experience Platform-användargränssnittet och markera sedan statusaviseringen för att se vilka resurser du vill granska.

![Meddelandepanelen i Experience Platform-användargränssnittet med ett varningsmeddelande om ett misslyckat dataflöde markerat.](../../images/tutorials/templates/notifications.png)

Du kan uppdatera aviseringsinställningarna för dina mallar så att du får både e-post- och Experience Platform-meddelanden om status för dina dataflöden. Mer information om hur du konfigurerar aviseringar finns i guiden [Prenumerera på aviseringar om källdataflöden](../ui/alerts.md).