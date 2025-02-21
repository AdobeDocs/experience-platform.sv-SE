---
title: Engagera och skaffa nya kunder utan att vara beroende av cookies från tredje part
description: Lär dig hur du engagerar och skaffar nya kunder genom prospektering av användningsfall, utan att förlita dig på tredjepartscookies.
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 1%

---

# Engagera och skaffa nya kunder utan att vara beroende av cookies från tredje part

>[!AVAILABILITY]
>
>* Den här funktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime och Real-Time CDP Ultimate. Läs mer om de här paketen i [produktbeskrivningarna](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta din Adobe-representant för mer information.

Utnyttja datastödet från tredje part i Real-Time CDP för att utöka er profilbas med profiler för potentiella kunder från datapartners och engagera dem i kundvärvningen eller nå nya kunder.

![Kundprospektering använder en omfattande visuell översikt.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Varför ska man tänka på det här användningsexemplet? {#why-this-use-case}

Varumärken står samtidigt inför utmaningar när det gäller att på ett ansvarsfullt sätt genomföra kundvärvningsärenden utan att vara beroende av cookies från tredje part, begränsade budgetar och högre krav på transparens och avkastning på annonskostnaderna.

Adobe Real-Time Customer Data Platform kan hjälpa varumärken att på ett säkert sätt övergå till att använda sina datahanteringsplattformar (DMP) till cookie-fria alternativ och göra detta på ett sätt som gör att självbetjäningssegmentering, målgruppsböjning och aktivering kan utvecklas till ett enda system. Utan att kompromissa med Adobe orubbliga fokus på ansvarsfull dataanvändning via en patenterad ramverk för datastyrning och samtycke.

Följ till exempel de steg som beskrivs i det här fallet när du behöver köra en kampanj för att locka potentiella kunder att bli användare eller kända kunder.

## Förutsättningar och planering {#prerequisites-and-planning}

När du funderar på att nå ut till och köpa nya kunder bör du tänka på följande under planeringsprocessen:

* Hur lång tid har du på dig att förvänta dig att partnerprofiler ska importeras till Real-Time CDP och uppdateras?
* Vilka identiteter kräver era nedströmsadresser?
* Se till att identifierarna som hämtas är åtgärdbara nedåt
* Är de partnerdata som du importerar knutna till en allmänt accepterad varaktig identifierare, till exempel personlig identifieringsinformation (PII), hashad-PII eller en partneridentifierare?
* Vilka dataanvändningspolicyer behöver ni vara medvetna om ur partnerperspektiv och från ert eget juridiska team, sekretessteam eller efterlevnadsteam?

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

Innan du utökar Real-Time CDP för att engagera och värva nya kunder måste du se till att använda Real-Time CDP för att skapa en stabil grund för era egna data. Arbetsflödena för att uppnå det här användningsfallet liknar arbetsflödena för att interagera med kända kunder.

![Kundprospektering använder en omfattande visuell översikt.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Som **kund** licensierar du profiler för potentiella kunder från en eller flera **datapartner** för att hjälpa till att få högsta möjliga resultat när det gäller kundvärvningen.
2. Som **kund** utökar du dina profildata och styrningsmodeller till att importera listan **partner** med profiler för potentiella kunder.
3. Som **kund** läser du in profiler för potentiella kunder i Real-Time CDP och skapar principer för styrning för att säkerställa ansvarsfull användning.
4. Som **kund** skapar du fokuserade målgrupper från listan med profiler för potentiella kunder.
5. Som **kund** aktiverar du potentiella målgrupper till mål som accepterar de identiteter som finns i listan över potentiella kunder.
6. Om det behövs kan du samarbeta med **datapartnern** för att aktivera målgrupper på sista milen till önskade betalmediemål.

## Videogenomgång {#video-walkthrough}

Se videosjälvstudiekursen nedan för en genomgång av hur ni kan nå och engagera potentiella målgrupper:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Gränssnittsfunktioner och -element som du använder {#ui-functionality-and-elements}

När du är klar med implementeringen av användningsexemplet kommer du att använda följande Real-Time CDP-funktioner och gränssnittselement (listade i den ordning som du ska använda dem). Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden eller be systemadministratören att ge dig de behörigheter som krävs.

* [Identiteter](/help/identity-service/features/namespaces.md)
* [Scheman](/help/xdm/home.md)
* [Dataanvändningsetiketter](/help/data-governance/labels/overview.md)
* [Datauppsättningar](/help/catalog/datasets/overview.md)
* [Källor](/help/sources/home.md)
* [Prospekteringsprofiler](/help/profile/ui/prospect-profile.md)
* [Potentiella målgrupper](/help/segmentation/types/prospect-audiences.md)
* [Mål](/help/destinations/home.md)

### Licensiera profilinformation från partnern {#license-profiles-from-partner}

Det här steget beskrivs i [förutsättningarna](#prerequisites-and-planning) och Adobe förutsätter att du har rätt avtalsavtal på plats med betrodda dataleverantörer för att kunna importera profiler för potentiella kunder från dataparten.

### Utöka er profildata och styrningsmodell för att passa profiler som tillhandahålls av partners {#extend-governance-model}

För att kunna ta emot profiler för potentiella kunder från din datapartner måste du utöka datahanteringsramverket i Real-Time CDP så att det passar den nya profiltypen.

De identitets-, datahanterings- och styrningskomponenter du kommer att använda är:

* En ny **[!UICONTROL Partner ID]**-identitetstyp för de profiler som partnern tillhandahåller
* En ny **[!UICONTROL XDM Individual Prospect Profile]** XDM-klass
* **(Dokumentationen kommer snart)** Fältgrupper har skräddarsytts för partnerdatastöd
* **(Dokumentation kommer snart)** Tredjepartsetiketter som du lägger till i attribut från partners

#### Skapa en namnrymd för en partner-ID {#create-partner-id-namespace}

Börja med att skapa en ny identitetstyp för de profiler som du ska ta emot från partnern. För att göra detta måste du skapa ett nytt identitetsnamnutrymme av typen **[!UICONTROL Partner ID]** i avsnittet Identitet.

![Skapa ett nytt namnområde för en partner-ID.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Läs mer om namnutrymmen för partner-ID i avsnittet [identitetstyper](/help/identity-service/features/namespaces.md).
* Läs om [hur du definierar identitetsfält](/help/xdm/ui/fields/identity.md) i Experience Platform användargränssnitt.

#### Skapa ett nytt schema med klassen **[!UICONTROL XDM Individual Prospect Profile]**

Skapa sedan ett nytt schema i **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]** och tilldela det till klassen **[!UICONTROL XDM Individual Prospect Profile]**.

![Sök efter klassen XDM Individual Prospect Profile i XDM-schemaverktaren.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Läs om hur du [skapar och redigerar scheman i användargränssnittet](/help/xdm/ui/resources/schemas.md) och får fullständig information om klassen XDM Individual Prospect Profile (kommande länkar).

Klassen **[!UICONTROL XDM Individual Prospect Profile]** levereras förkonfigurerad med fälten som visas nedan. Om du vill utöka ditt schema med attribut som tillhandahålls av partners för profiler för potentiella kunder kan du antingen skapa en ny fältgrupp med de attribut som du förväntar dig och lägga till den i schemat, eller så kan du använda en av de förkonfigurerade fältgrupperna som tillhandahålls av Adobe.

![Förkonfigurerade fält för klassen XDM Individual Prospect Profile.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Sedan måste du välja den partner-ID-identitet som du skapade tidigare som primär identitet för schemat. Profilposter måste innehålla en primär identifierare. Detta steg krävs för att säkerställa att data om potentiella kunder kan läsas in i profilarkivet och göras tillgängliga för segmentering och aktivering.

>[!AVAILABILITY]
>
>Proportionsprofiler begränsas automatiskt till att endast använda ID-namnutrymmen av typen Partner-ID. Detta sker genom design och säkerställer en ren separation mellan era egna profiler och profiler för potentiella kunder.

![Välj tidigare konfigurerat partner-ID som primär identitet i schemat.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Observera att schemat ännu inte har aktiverats för profilen. Aktivera det här schemat för att inkluderas i profiltjänsten genom att växla profilknappen. Mer information om hur du aktiverar schemat för användning i kundprofilen i realtid finns i självstudiekursen [Skapa schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Aktivera schema för profil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Lägg till etiketten för datastyrning från tredje part i alla fält i schemat

Överväg att lägga till etiketter för datastyrning från tredje part i alla fält som utgör schemat. Detta är viktigt för att säkerställa en ansvarsfull användning av data från tredje part och minimera risken för dataläckage. Mer information om [etiketter för datastyrning från tredje part](../../data-governance/labels/reference.md#partner-ecosystem-labels) finns.

Gör så här:

1. Navigera till schemat som du skapade och välj fliken **[!UICONTROL Labels]**.
2. Markera alla fält i det här schemat med kryssruteknappen högst upp och klicka sedan på pennikonen till höger för att använda datastyrningsetiketter på det här schemat.
3. Välj etiketten **[!UICONTROL Partner Ecosystem]** bland kategorierna till vänster.
4. Välj etiketten **[!UICONTROL Third Party]** och välj **[!UICONTROL Save]**.
5. Observera att alla fält i schemat nu innehåller etiketten som du valde i föregående steg.

>[!SUCCESS]
>
>Ditt schema är nu klart att användas och du kan gå vidare till nästa steg för att importera data om potentiella kunder från din datapartner.

I det här steget bör du också tänka på hur er datastyrningsmodell ändras när ni utökar er datahanteringsstrategi så att den omfattar data från tredje part från partnern. Ta en titt på vad du bör tänka på i dokumentationslänkarna nedan:

* (**Kommer snart**) Håll tredjepartsdata i en separat datauppsättning så att det blir enkelt att ta bort och ångra integreringar.
* (**Kommer snart**) Använd funktionen [utgångsdatum](/help/hygiene/ui/dataset-expiration.md) i datauppsättningen för klienter som köpt tillägget för datahygien.
* (**Kommer snart**) Var försiktig när du skapar härledda datauppsättningar som hämtar in data från tredje part, eftersom den enda lösningen för att ta bort data från tredje part är att ta bort hela den härledda datauppsättningen när dessa har blandats.

### Läs in listan med profiler för potentiella kunder och inspektera vyn med profiler för potentiella kunder

När du har förberett din datamodell för hantering av profiler för potentiella kunder är det dags att importera data.

#### Skapa en datauppsättning och läsa in exempeldata för potentiella kunder

Om du vill läsa in vissa exempeldata och fylla i profiler för potentiella kunder skapar du en datauppsättning och överför en fil som du har fått från dataparten. Följ stegen nedan:

1. Navigera till **[!UICONTROL Data Management]** > **[!UICONTROL Datasets]** och välj **[!UICONTROL Create dataset]**.
2. Välj Skapa datauppsättning från schema
3. Välj schemat som du skapade i ett tidigare steg
4. Ge datauppsättningen ett namn och eventuellt en beskrivning.
5. Välj **[!UICONTROL Finish]**.

![En inspelning av stegen för att skapa en datauppsättning för profiler för potentiella kunder.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Observera att du, precis som när du skapar ett schema, måste aktivera datauppsättningen som ska ingå i kundprofilen i realtid. Mer information om hur du aktiverar datauppsättningen för användning i kundprofilen i realtid finns i självstudiekursen [Skapa schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Aktivera datauppsättning för profil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Om du vill läsa in en fil som du har fått från partnern till datauppsättningen markerar du datauppsättningen, rullar nedåt i den högra listen och väljer **[!UICONTROL Add data]**. Du kan dra och släppa filen eller välja **[!UICONTROL Choose files]** för att navigera till filplatsen och markera den.

![Lägg till fil i datauppsättning.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

När du har läst in listan över profiler från dataparten till Real-Time CDP fortsätter du till avsnittet [Inspektera de inlästa profilerna för potentiella kunder](#inspect-profiles) för att kontrollera att profilerna för potentiella kunder fylls i i användargränssnittet.

#### Importera data för potentiella kunder via källanslutningar

Du kan ställa in återkommande filimport för att importera data från partnern via en källanslutning och föra in listan med profiler för potentiella kunder i Real-Time CDP.

Några av de rekommenderade källanslutningarna för detta ändamål finns i listan nedan, men observera att alla filbaserade importmetoder i Real-Time CDP fungerar för ditt ändamål.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

När du har läst in listan över profiler från dataparten till Real-Time CDP fortsätter du till nästa avsnitt för att kontrollera att profilerna för potentiella kunder fylls i i användargränssnittet.

#### Inspektera de inlästa profilerna för potentiell kund {#inspect-profiles}

Navigera till **[!UICONTROL Prospects]** > **[!UICONTROL Profiles]** i den vänstra listen om du vill se en lista över profiler för potentiella kunder.

Observera att det kan ta upp till två timmar för de profiler för potentiella kunder som du just har läst in till Real-Time CDP att visas i vyn **[!UICONTROL Browse]** på skärmen Prospekt Profile. Om det visas ett meddelande på sidan om att det inte finns några profiler att bläddra bland just nu kan du försöka igen om en stund. Efter en stund bör profiler för potentiella kunder börja visas i vyn **[!UICONTROL Browse]**.

>[!TIP]
>
>Observera att kolumnen **[!UICONTROL Identity Namespace]** finns. Om du arbetar med flera dataleverantörer använder du den här kolumnen för att härleda de potentiella kundprofilernas ursprung.

![Visa profiler för potentiella kunder inlästa till Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Du kan också välja vilken profil som helst för potentiell kund för vidare undersökning enligt nedan.

![Visa hur du inspekterar profiler för potentiella kunder.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Läs mer om [profiler för potentiella kunder](/help/profile/ui/prospect-profile.md).

### Skapa potentiella målgrupper {#create-prospect-audiences}

Använd segmenteringsfunktionerna i Real-Time CDP för att skapa målgrupper utifrån era profiler för potentiella kunder. Använd önskade segmenteringsregler för att skapa anpassade målgrupper.

Navigera till **[!UICONTROL Prospects]** > **[!UICONTROL Audiences]** för att komma igång och skapa målgrupper som består av profiler för potentiella kunder.

![Vy över potentiella målgrupper.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Observera att målgruppsupplevelsen för profiler med potentiella kunder skiljer sig från upplevelsen när det gäller att skapa målgrupper från era kända förstapartskunder. Den här vyn är begränsad till:

* Attribut från klassen för potentiella kunder som du skapade tidigare.
* Endast utvärdering av batchprofil.
* Har inte stöd för att bygga målgrupper baserat på tidsseriehändelser.

Läs mer om [potentiella målgrupper](/help/segmentation/types/prospect-audiences.md).

### Aktivera profiler för potentiella kunder till mål {#activate-to-destinations}

Utnyttja målgrupperna genom att exportera dem till destinationer. För närvarande stöder endast vissa molnlagringsmål aktivering av profiler för potentiella kunder.

![Destinationer som stöder potentiella målgrupper.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Läs mer](/help/destinations/ui/activate-prospect-audiences.md) om hur du aktiverar potentiella kunder till molnlagringsmål.

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* [Komplettera förstahandsprofiler med attribut från betrodda datapartners](/help/rtcdp/partner-data/supplement-first-party-profiles.md) för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.
* [Anpassa upplevelser på plats för okända besökare med partnerstödd besökarigenkänning](/help/rtcdp/partner-data/onsite-personalization.md) under besöket utan att användaren behöver autentisera sig eller ha en tidigare historik med varumärket.
* [Utökad aktivering av profiler för potentiella kunder och målgrupper](/help/destinations/ui/activate-prospect-audiences.md) för utvalda mål.
