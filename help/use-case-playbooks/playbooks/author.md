---
solution: Experience Platform
title: Lär dig hur du skapar och delar dina egna Playbooks med hjälp av AI Assistant.
description: Skapa och dela egna fallspelningsböcker.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 0%

---


# Skapa och dela dina egna spelböcker (Beta)

Med [!DNL Playbook Authoring Framework], som drivs av AI Assistant i Adobe Experience Platform, kan du skapa, hantera och dela spelböcker effektivt i Adobe Experience Platform.

Ramverket följer en trestegsprocess:

1. **Metadatainhämtning**: Använd AI-assistenten eller webbformuläret för att hämta metadata för spelningsböcker.

2. **Teknisk association**: Lägg till specifika tekniska resurser som resor eller målgrupper i spelboken. Du behåller fullständig kontroll över processen att skapa spelböcker i din utvecklingssandlåda, vilket säkerställer justering med dina scheman och andra unika datastrukturer.

3. **Playbook-distribution**: Dela spelböcker mellan olika organisationer. ACME:s Martech Center of Excellence i Tyskland kan till exempel skapa en &quot;gyllene&quot; spelbok och distribuera den till regionala organisationer i Thailand, Australien osv. för att standardisera användningsexemplen för marknadsföring.

## Skapa en spelningsbok

Du kan skapa en spelbok på två sätt: antingen med hjälp av AI-assistenten eller manuellt. Läs följande avsnitt för att lära dig hur du skapar en spelbok med AI Assistant.

### Spelboksöversikt

Så här skapar du en spelbok med AI-assistenten:

Välj **[!UICONTROL Playbooks]** i den vänstra navigeringspanelen.

![Plattformsgränssnitt med alternativet &quot;Playbooks&quot; markerat i den vänstra navigeringspanelen.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Välj **[!UICONTROL New Playbook]** och välj sedan **Generera spelbok med AI Assistant**.

![Gränssnittet för att skapa spelbok visar alternativet Generera spelbok med AI-assistenten markerat.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Använd promptfältet för att beskriva användningsfallet. Exempel:

&quot;Engagera ACME-kunder som surfar på skor men inte slutförde köpet.&quot;

![Gränssnittet för att skapa spelbok markerar det webbformulärsområde där användarna kan skriva in en fråga.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Välj **[!UICONTROL Generate]** om du vill skapa spelbokens metadata.

![Gränssnittet för att skapa spelbok visar knappen Generera markerad i promptområdet.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Välj **[!UICONTROL Edit]** om du vill ändra den genererade titeln, beskrivningen och metadata efter behov.

![En genererad spelbok med knappen Redigera markerad, som tillåter användare att ändra metadata.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Fyll i avsnittet **[!UICONTROL Playbook detail]** för att se till att datateknikerna har all information som krävs för att ställa in användningsfallet. Dessa fält är valfria, men hjälper till att hämta in viktig information, vilket gör det enklare att koppla samman rätt tekniska komponenter. Välj **[!UICONTROL Edit]** om du vill lägga till värden i följande fält:

* **Bransch**
* **Målgrupp**
* **Marknadsföringskanal**

![Avsnittet med information om spelboken med knappen Redigera markerat så att du kan lägga till eller ändra information som bransch, målgrupp och marknadsföringskanal.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

När metadata har genererats väljer du **[!UICONTROL Edit journey map]** om du vill justera stegen i färdplanen efter behov.

![Knappen Redigera färdplan om du vill ändra stegen i färdplanen.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Gränssnittet för redigering av färdkarta så att du kan justera stegen efter att du har hämtat metadata för spelningsboken.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Fortsätt sedan att associera spelboken med tekniska resurser. Om du vill skapa en spelbok manuellt väljer du **[!UICONTROL Create playbook manually]**.

![Alternativet Skapa spelningsbok manuellt om du vill starta en spelbok från en tom mall.](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

En tom spelningsboksmall visas. Fyll i detaljer som **Titel** och **Beskrivning**. Du kan också redigera färdplanen för att lägga till händelser och kontaktytor efter behov.

## Associera spelbok med tekniska resurser

Oavsett om du skapar en spelbok manuellt eller med AI-assistenten måste du koppla den till de tekniska resurser som krävs. Gå till fliken **[!UICONTROL Technical Assets]** och välj önskad produkt. I det här exemplet väljer du **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> Stöd för Real-Time CDP kommer att läggas till i en kommande version.

![Fliken&quot;Technical Assets&quot; med knappen&quot;Add required product&quot; (Lägg till nödvändig produkt) har markerats som du kan använda för att associera tekniska resurser med spelboken.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Välj **[!UICONTROL Select an Asset]** om du vill associera den här spelboken med en resa enligt bilden nedan. Välj sedan **Publicera spelningsbok** för att slutföra spelningsboken.

![Fliken&quot;Technical Assets&quot; med knappen&quot;Select assets&quot; (Välj resurser) har markerats och du kan använda den för att associera en resa med spelboken.](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Välj en resa att associera med en spelbok.](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Efter publiceringen extraherar och associerar spelboken automatiskt kundens schema och målgruppsinformation.

![En publicerad spelbok med metadata och associerade tekniska resurser.](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Alla skapade spelböcker är tillgängliga på fliken **Dina spelböcker**.

Fliken ![&quot;Dina spelböcker&quot; som visar en lista med skapade spelböcker.](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Du kan välja valfri spelningsbok från katalogen för att skapa instanser som ska återanvändas. Läs dokumentationen för att [lära dig hur du skapar instanser](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![Fliken&quot;Spelboksöversikt&quot; med alternativet&quot;Skapa instans&quot; markerat.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> När en spelbok väl har publicerats kan den inte redigeras. Om du vill göra ändringar tar du bort spelboken och börjar om.

## Exempeluppmaningar

AI-assistenten kan bearbeta olika snabbstrukturer och extrahera nyckeldetaljer samtidigt som onödig information filtreras bort. Nedan visas några exempel på användaruppmaningar och hur systemet tolkar dem.

**Exempel 1:**

&quot;Skapa en kampanj med namnet &quot;Complete the Look&quot; för att öka försäljningen och CLV. Kampanjen uppmuntrar kunderna att köpa köksartiklar och möbler för att slutföra ett kompletterande köp via personaliserade rekommendationer och erbjudanden i samband med deras inköp. Meddela först kunderna med produktrekommendationer. Om de inte gör några inköp inom 7 dagar får de ett andra meddelande med produktrekommendationer och erbjudanden. Använd push-meddelanden och e-post för att kontakta kunderna. Rikta er till kunder som har köpt köksartiklar eller möbler de senaste 7 dagarna och som inte har varit målkunder de senaste 30 dagarna. Som en del av kampanjen vill vi mäta nyckeltal som till exempel klick (e-post, app, sms, push), CTR, E-Wallet CTR, AOV Conversion.CLV Revenue, Total Purchase Events (in-store, digital, call center).&quot;

![Ett exempel på en lång uppmaning i textrutan att generera en spelningsbok.](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Exempel 2:**

&quot;Projektnamn: Fashion Newsletter
Bakgrund: (proaktiv eller problemlösning): En resa som är utformad för att skicka modenyhetsbrev till ACME-kunder som prenumererat på nyhetsbrev.
Mål: Skicka nyhetsbrev till ACME-kunder som prenumererar på kommunikation.
Kampanjinformation: Kunden får modenyheter i e-postkanalen varje vecka. E-postmeddelandet ska vara personaliserat och innehållsvariationer baseras på kön, språk och marknad.
Projektkanaler/kontaktytor: E-post
Målgrupp: Kunder som prenumererar på ACME-nyhetsbrev.
Mål-KPI:er/engagemangsmått/avkastning: 1. Öka intäkterna från produkterna. 2. Öka kundlojaliteten.&quot;

![Ett exempel på en ordnad fråga i liststil som har angetts i textinmatningsrutan för att skapa en spelningsbok.](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Exempel 3:**

&quot;Knuffa kunderna för att köpa produkter under en pågående produktkampanj.
Engagera med kunderna under en pågående kampanj genom att skicka lämplig kommunikation via e-post, SMS eller push-meddelanden för att köpa produkter. Skicka en påminnelse via e-post efter 24 timmar av att de inte engagerade sig i kampanjen.&quot;

![Ett exempel på en kortfattad fråga som har angetts i textrutan för att skapa en spelningsbok.](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Exempel 4:**

&quot;Sälj skor till high school-spelare.&quot;

![Ett exempel på en enradig uppmaning som har angetts i textrutan för att skapa en spelningsbok.](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

AI-assistenten tar bort alla onödiga detaljer som &quot;Projektnamn&quot; eller &quot;Bakgrund&quot;. Det extraherar nyckelelement som&quot;målgrupp&quot;,&quot;kampanjmål&quot; och&quot;marknadsföringskanal&quot; och fungerar med alla indatatyper.

De här exemplen visar hur AI kan förfina och extrahera viktig information från användaruppmaningar.

>[!NOTE]
>
> Undvik eventuella PII-ord eller explicita ord när du skriver uppmaningar.

## Riktlinjer och moderering för innehåll

När du skapar spelböcker ska du tänka på vilket språk och vilket innehåll du inkluderar. Spelböcker visas i hela organisationen och stötande eller olämpligt innehåll som användarna flaggar.

### Flaggning och granskningsprocess

Om en spelbok innehåller olämpligt eller stötande innehåll får Adobe automatiskt en rapport för granskning. Adobe granskar det markerade innehållet, meddelar kunden om det anses olämpligt och tar bort spelboken.

## Dela spelböcker över sandlådor {#share-playbooks-sandboxes}

När du skapar och publicerar en spelbok i en sandlåda blir den automatiskt tillgänglig i alla sandlådor i organisationen. Den här funktionen eliminerar behovet av manuell delning och gör att du kan skapa instanser av spelboken i andra sandlådor utan problem.

>[!TIP]
>
>Om spelningsboken refererar till fält som inte är tillgängliga i unionsschemat för målsandlådan eller om du saknar nödvändig behörighet, visas ett felmeddelande när du försöker skapa instansen. Meddelandet anger vilka fält och/eller behörigheter som saknas.

Om några fält saknas i ditt unionsschema markeras de i en dialogruta under importen.

![En dialogruta med fält som saknas i unionsschemat under importprocessen för spelningsboken.](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Dela dina spelböcker i olika organisationer {#sharing-playbooks-organizations}

Genom att dela spelböcker mellan olika organisationer kan du säkerställa enhetlighet och effektivitet när flera team behöver följa samma bästa praxis. Så här delar du en spelbok från en organisation till en annan:

1. **Logga in i källorganisationen**: Navigera till organisationen som innehåller den spelbok som du skapade och vill dela på fliken **[!UICONTROL Your playbooks]**.
2. **Publicera spelningsboken**: Om spelningsboken inte redan är publicerad måste du publicera den innan du delar den.

   >[!NOTE]
   >
   >Ett partnerskap måste upprättas mellan käll- och målorganisationerna för att det ska gå att dela spelböcker. Lär dig hur du [skapar en förfrågan om organisationskoppling](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request).

3. **Starta resursen**: Välj **[!UICONTROL Share Playbook]** när spelboken har publicerats och en koppling har upprättats.
4. **Välj målorganisation**: Välj den organisation du vill dela spelboken med när du uppmanas till det.
5. **Bekräfta och dela**: Bekräfta ditt val. Du får bekräftelsemeddelanden som anger att delningen lyckades.
6. **Verifiera målorganisationen**: Logga in i målorganisationen för att verifiera att spelboken är tillgänglig.
7. **Importera spelningsboken**: Välj **[!UICONTROL Import]** om du vill överföra spelningsboken till målorganisationen. Du kan visa den på fliken **Spelböcker**.

Om spelboken inte visas kontrollerar du att den är publicerad och att organisationspartnerskapet är aktivt.

>[!IMPORTANT]
>
>Transitiv delning av spelbok stöds inte. Om du delar en spelbok från en organisation till en annan och sedan importerar den kan den inte delas igen från den mottagande organisationen till en tredje organisation.

## Nödvändiga behörigheter {#required-permissions}

Du behöver följande behörigheter för att få åtkomst till sandlådan och använda den här funktionen:

### Sandlådebehörigheter

Dessa behörigheter krävs för att få åtkomst till sandlådemiljön där funktionen finns:

* **Hantera sandlåda**
* **Visa sandlåda**

* **Behörigheter för paketdelning**:

Dessa behörigheter krävs för intern delning:

* [**Hantera paket**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Dela paket**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Använd dessa behörigheter för att:

* Ange sandlådemiljön
* Få åtkomst till funktionen i sandlådan
* Hantera och dela paket efter behov

Dessa behörigheter finns i avsnittet **[!UICONTROL Sandboxes]** i behörighetslistan.

![Behörighetslistan med relevanta behörigheter för att hantera och dela spelböcker är markerad.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Resor och besläktade objekt - behörigheter

När du skapar resor som använder Playbooks kan du referera till andra objekt, som **Kanaler**, **Publiker** och andra entiteter. Var och en av dessa objekt har en egen behörighetsgrupp.

Det här är nyckelbehörigheterna för reserelaterade åtgärder, som:

* **Visa resa**
* **Hantera resa**
* Behörigheter för objekt som målgrupper och kanaler

Du behöver även följande behörigheter:

* **Segmentläsning**
* **Profilen har lästs**
* **Datauppsättningen har lästs**

Eftersom Resor är mycket flexibla och kan omfatta många sammankopplade objekt, dokumenteras deras [fullständiga behörigheter](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) separat och kan variera beroende på ditt specifika användningsfall.

## Nästa steg

Nu när du förstår hur du skapar, publicerar och delar spelböcker med hjälp av AI Assistant kan du lära dig hur du kommer igång med de tillgängliga spelböckerna och välja rätt i [Playbooks List](/help/use-case-playbooks/playbooks/choose.md).