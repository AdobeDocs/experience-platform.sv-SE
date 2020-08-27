---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Användarhandbok för JupyterLab
topic: Overview
description: JupyterLab är ett webbaserat användargränssnitt för Project Jupyter och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyters bärbara datorer, kod och data. Det här dokumentet innehåller en översikt över JupyterLab och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '3700'
ht-degree: 10%

---


# [!DNL JupyterLab] användarhandbok

[!DNL JupyterLab] är ett webbaserat användargränssnitt för [Project Jupyter](https://jupyter.org/) som är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyters bärbara datorer, kod och data.

Det här dokumentet innehåller en översikt över [!DNL JupyterLab] och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.

## [!DNL JupyterLab] på [!DNL Experience Platform]

Integreringen av Experience Platform JupyterLab åtföljs av arkitektoniska förändringar, designöverväganden, anpassade utbyggnadsmoduler för bärbara datorer, förinstallerade bibliotek och ett gränssnitt med Adobe-teman.

I följande lista beskrivs några av funktionerna som är unika för JupyterLab på Platform:

| Funktion | Beskrivning |
| --- | --- |
| **Kernlar** | Kernels ger möjlighet att köra och granska kod i olika programmeringsspråk för bärbara datorer och andra [!DNL JupyterLab] gränssnitt. [!DNL Experience Platform] har ytterligare kernel som stöder utveckling i [!DNL Python], R, PySpark och [!DNL Spark]. Mer information finns i avsnittet [Kernlar](#kernels) . |
| **Dataåtkomst** | Få tillgång till befintliga datauppsättningar direkt inifrån [!DNL JupyterLab] med fullt stöd för läs- och skrivfunktioner. |
| **[!DNL Platform]tjänstintegration** | Inbyggda integreringar gör att du kan använda andra [!DNL Platform] tjänster direkt inifrån [!DNL JupyterLab]. En fullständig lista över integreringar som stöds finns i avsnittet om [integrering med andra plattformstjänster](#service-integration). |
| **Autentisering** | Förutom <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab:s inbyggda säkerhetsmodell</a>krypteras och autentiseras all interaktion mellan programmet och Experience Platform, inklusive kommunikation från tjänst till tjänst på plattformen, via <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Utvecklingsbibliotek** | I [!DNL Experience Platform]finns [!DNL JupyterLab] förinstallerade bibliotek för [!DNL Python], R och PySpark. En fullständig lista över bibliotek som stöds finns i [bilagan](#supported-libraries) . |
| **Bibliotekshanterare** | När de förinstallerade biblioteken saknas för dina behov kan ytterligare bibliotek installeras för Python och R, och lagras tillfälligt i isolerade behållare för att bibehålla integriteten hos [!DNL Platform] och skydda dina data. Mer information finns i avsnittet [Kernlar](#kernels) . |

>[!NOTE]
>
>Ytterligare bibliotek är bara tillgängliga för den session där de installerades. Du måste installera om alla ytterligare bibliotek som du behöver när du startar nya sessioner.

## Integrering med andra [!DNL Platform] tjänster {#service-integration}

Standardisering och interoperabilitet är viktiga koncept som ligger bakom [!DNL Experience Platform]. Integreringen av [!DNL JupyterLab] on [!DNL Platform] som en inbäddad IDE gör att den kan interagera med andra [!DNL Platform] tjänster, vilket gör att du kan utnyttja [!DNL Platform] den fullt ut. Följande [!DNL Platform] tjänster är tillgängliga i [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Få tillgång till och utforska datauppsättningar med läs- och skrivfunktioner.
* **[!DNL Query Service]:** Få åtkomst till och utforska datauppsättningar med SQL, vilket ger lägre dataåtkomstkostnader när du hanterar stora mängder data.
* **[!DNL Sensei ML Framework]:** Modellutveckling med möjlighet att träna och poängsätta data, liksom att skapa recept med ett enda klick.
* **[!DNL Experience Data Model (XDM)]:** Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

>[!NOTE]
>
>Vissa [!DNL Platform] tjänstintegreringar på [!DNL JupyterLab] är begränsade till specifika kärnor. Mer information finns i avsnittet om [kernlar](#kernels) .

## Viktiga funktioner och vanliga åtgärder

Information om de viktigaste funktionerna [!DNL JupyterLab] och anvisningar om hur man utför vanliga åtgärder finns i avsnitten nedan:

* [Åtkomst till JupyterLab](#access-jupyterlab)
* [Gränssnittet JupyterLab](#jupyterlab-interface)
* [Kodceller](#code-cells)
* [Kernlar](#kernels)
* [Kernel-sessioner](#kernel-sessions)
* [Körningsresurs för PySpark/Spark](#execution-resource)
* [Startprogram](#launcher)

### Öppna [!DNL JupyterLab] {#access-jupyterlab}

I [Adobe Experience Platform](https://platform.adobe.com)väljer du **Anteckningsböcker** i den vänstra navigeringskolumnen. Ge lite tid åt [!DNL JupyterLab] att initiera.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] gränssnitt {#jupyterlab-interface}

Gränssnittet består [!DNL JupyterLab] av en menyrad, ett fällbart sidofält och huvudarbetsytan som innehåller flikar med dokument och aktiviteter.

**Menyrad**

Menyraden högst upp i gränssnittet har menyer på översta nivån som visar åtgärder som är tillgängliga i [!DNL JupyterLab] med sina kortkommandon:

* **Fil:** Åtgärder för filer och kataloger
* **Redigera:** Åtgärder som rör redigering av dokument och andra aktiviteter
* **Visa:** Åtgärder som ändrar utseendet på [!DNL JupyterLab]
* **Kör:** Åtgärder för att köra kod i olika aktiviteter, t.ex. anteckningsböcker och kodkonsoler
* **Kernel:** Åtgärder för hantering av kärnor
* **Tabbar:** En lista över öppna dokument och aktiviteter
* **Inställningar:** Vanliga inställningar och en avancerad inställningsredigerare
* **Hjälp:** En lista över [!DNL JupyterLab] och kernelhjälplänkar

**Vänster sidofält**

Den vänstra sidlisten innehåller klickbara flikar som ger tillgång till följande funktioner:

* **Filwebbläsare:** En lista över sparade anteckningsboksdokument och kataloger
* **Datautforskaren:** Bläddra bland, få tillgång till och utforska datauppsättningar och scheman
* **Löpande kärnor och terminaler:** En lista över aktiva kernel- och terminalsessioner med möjlighet att avsluta
* **Kommandon:** En lista med användbara kommandon
* **Cellkontroll:** En cellredigerare som ger tillgång till verktyg och metadata som är användbara när du ställer in en anteckningsbok för presentationsändamål
* **tabbar:** En lista med öppna flikar

Klicka på en flik för att visa dess funktioner, eller klicka på en utökad flik för att komprimera den vänstra sidopanelen så som visas nedan:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Huvudarbetsyta**

På huvudarbetsytan i [!DNL JupyterLab] kan du ordna dokument och andra aktiviteter i flikpaneler som kan storleksändras eller delas upp. Dra en flik till mitten av en tabbpanel för att migrera fliken. Dela upp en panel genom att dra en flik till vänster, höger, överst eller nederst på panelen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Kodceller {#code-cells}

Kodceller är det primära innehållet i anteckningsböcker. De innehåller källkod på samma språk som anteckningsbokens associerade kärna och utdata som ett resultat av körningen av kodcellen. Ett körningsantal visas till höger om varje kodcell som representerar dess körningsordning.

![](../images/jupyterlab/user-guide/code_cell.png)

Vanliga cellåtgärder beskrivs nedan:

* **Lägg till en cell:** Klicka på plustecknet (**+**) på anteckningsboksmenyn för att lägga till en tom cell. Nya celler placeras under den cell som för närvarande interagerar med, eller i slutet av anteckningsboken om ingen viss cell är i fokus.

* **Flytta en cell:** Placera markören till höger om cellen som du vill flytta, klicka och dra sedan cellen till en ny plats. Om du flyttar en cell från en anteckningsbok till en annan kopieras cellen tillsammans med dess innehåll.

* **Kör en cell:** Klicka på den cell som du vill köra och klicka sedan på **uppspelningsikonen** (**▶**) på anteckningsbokens meny. En asterisk (**\***) visas i cellens körningsräknare när kärnan bearbetar körningen och ersätts med ett heltal vid slutförandet.

* **Ta bort en cell:** Klicka på cellen som du vill ta bort och klicka sedan på **saxikonen** .

### Kernlar {#kernels}

Anteckningsbokskärnor är språkspecifika datormotorer för bearbetning av bärbara datorer. Dessutom [!DNL Python]har [!DNL JupyterLab] stöd för ytterligare språk i R, PySpark och [!DNL Spark] (Scala). När du öppnar ett anteckningsboksdokument startas den tillhörande kärnan. När en anteckningsbokscell körs utför kärnan beräkningen och ger resultat som kan ta mycket processorkraft och minnesresurser i anspråk. Observera att allokerat minne inte frigörs förrän kärnan stängs av.

Vissa funktioner är begränsade till särskilda kärnor enligt tabellen nedan:

| Kernel | Installationsstöd för bibliotek | [!DNL Platform] integreringar |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nej | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-sessioner {#kernel-sessions}

Varje aktiv anteckningsbok eller aktivitet på [!DNL JupyterLab] använder en kernel-session. Alla aktiva sessioner kan hittas genom att expandera fliken **Löpande terminaler och kerrar** från vänster sidofält. Den bärbara datorns typ och tillstånd för kärnan kan identifieras genom att man observerar den övre högra delen av gränssnittet. I diagrammet nedan är anteckningsbokens tillhörande kärna **[!DNL Python]3** och det aktuella läget representeras av en grå cirkel till höger. En ihålig cirkel innebär en inaktiv kärna och en fylld cirkel betyder en upptagen kärna.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Om kärnan är avstängd eller inaktiv under en längre tid, så **Ingen kernel!** med en fylld cirkel visas. Aktivera en kärna genom att klicka på kernelstatusen och välja lämplig kerneltyp enligt nedan:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Startprogram {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Med den anpassade *startguiden* får du användbara anteckningsboksmallar för de olika paneler som stöds så att du snabbt kan komma igång, bland annat:

| Mall | Beskrivning |
| --- | --- |
| Tom | En tom anteckningsboksfil. |
| Starter | En förfylld anteckningsbok som visar datautforskandet med exempeldata. |
| Detaljhandel | En förfylld anteckningsbok med information om <a href="https://adobe.ly/2wOgO3L" target="_blank">butiksförsäljningsmottagare</a> med exempeldata. |
| Recipe Builder | En anteckningsboksmall för att skapa ett recept i [!DNL JupyterLab]. Den är förfylld med kod och kommentarer som demonstrerar och beskriver processen att skapa recept. I den <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">bärbara datorn finns självstudiekurser</a> om du vill se en detaljerad genomgång. |
| [!DNL Query Service] | En förfylld anteckningsbok som visar hur data används [!DNL Query Service] direkt i [!DNL JupyterLab] de medföljande exempelarbetsflödena för att analysera data i stor skala. |
| XDM-händelser | En förfylld anteckningsbok som visar datautforskande av Experience Event-data efter värde, med fokus på gemensamma funktioner i datastrukturen. |
| XDM-frågor | En förfylld anteckningsbok som visar exempel på affärsfrågor om Experience Event-data. |
| Aggregera | En förfylld anteckningsbok som visar exempel på arbetsflöden för att samla stora mängder data i mindre, hanterbara segment. |
| Klustring | En förfylld anteckningsbok som demonstrerar maskininlärningsmodelleringsprocessen från början till slut med hjälp av klusteralgoritmer. |

Vissa mallar för bärbara datorer är begränsade till vissa kärnor. Malltillgängligheten för varje kärna mappas i följande tabell:

<table>
    <tr>
        <td></td>
        <th><strong>Tom</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Detaljhandel</strong></th>
        <th><strong>Recipe Builder</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM-händelser</strong></th>
        <th><strong>XDM-frågor</strong></th>
        <th><strong>Aggregera</strong></th>
        <th><strong>Klustring</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >no</td>
        <td >ja</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >ja</td>
        <td >ja</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >ja</td>
    </tr>
</table>

Om du vill öppna en ny *startprogram* klickar du på **Arkiv > Ny startfunktion**. Du kan också utöka **filläsaren** från vänster sidofält och klicka på plustecknet (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### GPU- och minnesserverkonfiguration i [!DNL Python]/R

I [!DNL JupyterLab] väljer du kugghjulsikonen i det övre högra hörnet för att öppna *serverkonfigurationen* för bärbara datorer. Du kan växla GPU på och tilldela den mängd minne du behöver med hjälp av skjutreglaget. Hur mycket minne du kan allokera beror på hur mycket organisationen har allokerat. Välj **[!UICONTROL Update configs]** att spara.

>[!NOTE]
>
>Endast en GPU tilldelas per organisation för bärbara datorer. Om grafikprocessorn används måste du vänta på att den användare som för närvarande har reserverat grafikprocessorn ska frisläppa den. Detta kan du göra genom att logga ut eller lämna GPU:n i viloläge i fyra eller fler timmar.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Få åtkomst till [!DNL Platform] data med bärbara datorer

Varje kärna som stöds har inbyggda funktioner som gör att du kan läsa [!DNL Platform] data från en datamängd i en anteckningsbok. Stöd för sidnumrering av data är dock begränsat till bärbara datorer [!DNL Python] och R-datorer.

### Datagränser för bärbara datorer

Följande information definierar den maximala mängden data som kan läsas, vilken typ av data som användes och den beräknade tidsramen som läser data. För [!DNL Python] och R användes en bärbar datorserver som konfigurerats med 40 GB RAM för prestandatesterna. För PySpark och Scala användes ett databricks-kluster som konfigurerats med 64 GB RAM, 8 kärnor, 2 DBU med högst 4 arbetare för de riktmärken som beskrivs nedan.

De ExperienceEvent-schemadata som användes varierade i storlek från ett tusen (1 K) rader på upp till en miljard (1B) rader. Observera att för PySpark och [!DNL Spark] mätvärden användes ett datumintervall på 10 dagar för XDM-data.

Ad hoc-schemadata bearbetades i förväg med [!DNL Query Service] Create Table as Select (CTAS). Dessa data varierade också i storlek från ett tusen (1K) rader, upp till en miljard (1B) rader.

#### [!DNL Python] begränsningar för bärbara datordata

**XDM ExperienceEvent-schema:** Du bör kunna läsa högst 2 miljoner rader (~6,1 GB data på disk) med XDM-data på mindre än 22 minuter. Om du lägger till ytterligare rader kan det leda till fel.

| Antal rader | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Storlek på disk (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (i sekunder) | 20.3 | 86.8 | 63 | 659 | 1315 |

**ad hoc-schema:** Du bör kunna läsa upp maximalt 5 miljoner rader (~5,6 GB data på disk) med data som inte är XDM (ad hoc) på mindre än 14 minuter. Om du lägger till ytterligare rader kan det leda till fel.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Diskstorlek (i MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (i sekunder) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Datagränser för bärbara datorer

**XDM ExperienceEvent-schema:** Du bör kunna läsa upp maximalt 1 miljon rader XDM-data (3 GB data på disk) på mindre än 13 minuter.

| Antal rader | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Storlek på disk (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (i sekunder) | 14.03 | 69.6 | 86.8 | 775 |

**ad hoc-schema:** Du bör kunna läsa upp maximalt 3 miljoner rader ad hoc-data (293 MB data på disk) på ca 10 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Diskstorlek (i MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK (i sek) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Datagränsgränser för PySpark ([!DNL Python] kernel):

**XDM ExperienceEvent-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~13,42 GB data på disk) med XDM-data på ca 20 minuter. Interaktivt läge stöder endast upp till 5 miljoner rader. Om du vill läsa större datauppsättningar rekommenderar vi att du växlar till gruppläge. I gruppläge bör du kunna läsa upp maximalt 500 miljoner rader (~1,31 TB data på disk) med XDM-data på ca 14 timmar.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Storlek på disk | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK (interaktivt läge) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (gruppläge) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**ad hoc-schema:** I interaktivt läge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på mindre än 3 minuter. I gruppläge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på ca 18 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Storlek på disk | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interaktivt SDK-läge (i sekunder) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| SDK-batchläge (i sekunder) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] Datagränser för bärbara datorer (Scala kernel):

**XDM ExperienceEvent-schema:** I interaktivt läge bör du kunna läsa upp maximalt 5 miljoner rader (~13,42 GB data på disk) med XDM-data på ca 18 minuter. Interaktivt läge stöder endast upp till 5 miljoner rader. Om du vill läsa större datauppsättningar rekommenderar vi att du växlar till gruppläge. I gruppläge bör du kunna läsa upp maximalt 500 miljoner rader (~1,31 TB data på disk) med XDM-data på ca 14 timmar.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Storlek på disk | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| Interaktivt SDK-läge (i sekunder) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK-batchläge (i sekunder) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**ad hoc-schema:** I interaktivt läge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på mindre än 3 minuter. I gruppläge bör du kunna läsa upp maximalt 1 miljard rader (~1,05 TB data på disk) med data som inte är XDM på ca 16 minuter.

| Antal rader | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Storlek på disk | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Interaktivt SDK-läge (i sekunder) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| SDK-batchläge (i sekunder) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Läs från en datauppsättning i [!DNL Python]/R

[!DNL Python] och R-anteckningsböcker gör att du kan numrera data när du använder datauppsättningar. Exempelkod för att läsa data med och utan sidnumrering visas nedan.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Läsa från en datauppsättning i/ [!DNL Python]R utan sidnumrering

Om du kör följande kod läses hela datauppsättningen. Om körningen lyckas sparas data som en Pandas-dataram som refereras av variabeln `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: Den unika identiteten för den datauppsättning som ska användas

#### Läs från en datauppsättning i [!DNL Python]/R med sidnumrering

Om du kör följande kod läses data från den angivna datauppsättningen. Sidnumrering uppnås genom att data begränsas och förskjuts genom funktionerna `limit()` respektive `offset()` . Begränsande data avser det maximala antalet datapunkter som ska läsas, medan förskjutning avser antalet datapunkter som ska hoppas över före läsning av data. Om läsåtgärden körs utan fel sparas data som en Pandas-dataram som variabeln refererar till `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: Den unika identiteten för den datauppsättning som ska användas

### Läs från en datauppsättning i PySpark/[!DNL Spark]/Scala

Med en aktiv PySpark- eller Scala-anteckningsbok öppen utökar du fliken **Data Explorer** från det vänstra sidofältet och dubbelklickar på **Datauppsättningar** för att visa en lista över tillgängliga datauppsättningar. Högerklicka på den datauppsättning som du vill få åtkomst till och klicka på **Utforska data i anteckningsbok**. Följande kodceller genereras:

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

I och med introduktionen av Spark 2.4 medföljer [`%dataset`](#magic) anpassad magi.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>
>I Scala kan du använda `sys.env()` för att deklarera och returnera ett värde inifrån `option`.

### Använda %dataset-magi i PySpark 3 ([!DNL Spark] 2.4) bärbara datorer {#magic}

I och med introduktionen av [!DNL Spark] 2.4 medföljer `%dataset` anpassad magi för användning i nya bärbara datorer med PySpark 3 ([!DNL Spark] 2.4) ([!DNL Python] 3 kernel).

**Användning**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Beskrivning**

Ett anpassat [!DNL Data Science Workspace] magiskt kommando för att läsa eller skriva en datauppsättning från en [!DNL Python] bärbar dator ([!DNL Python] 3 kernel).

* **{action}**: Den typ av åtgärd som ska utföras på datauppsättningen. Två åtgärder är tillgängliga,&quot;read&quot; eller&quot;write&quot;.
* **—datasetId {id}**: Används för att ange ID för datauppsättningen som ska läsas eller skrivas. Detta är ett obligatoriskt argument.
* **—dataFrame {df}**: Pandornas dataram. Detta är ett obligatoriskt argument.
   * När åtgärden är &quot;read&quot; är {df} variabeln där resultaten av datauppläsningsåtgärden är tillgängliga.
   * När åtgärden är&quot;write&quot;, skrivs den här dataramen {df} till datauppsättningen.
* **—mode (valfritt)**: Tillåtna parametrar är&quot;batch&quot; och&quot;interactive&quot;. Som standard är läget inställt på &quot;interaktiv&quot;. Vi rekommenderar att du använder gruppläge när du läser stora mängder data.

**Exempel**

* **Läs exempel**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Exempel** på skrivning: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Fråga data med [!DNL Query Service] hjälp av [!DNL Python]

[!DNL JupyterLab] på [!DNL Platform] kan du använda SQL i en [!DNL Python] anteckningsbok för att komma åt data via <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Query Service</a>. Att komma åt data via [!DNL Query Service] kan vara användbart för att hantera stora datauppsättningar på grund av dess överlägsna körtider. Observera att sökning efter data med [!DNL Query Service] har en tidsgräns på tio minuter.

Innan du använder [!DNL Query Service] i [!DNL JupyterLab]måste du ha en fungerande förståelse för <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service] SQL-syntaxen</a>.

Om du frågar efter data med [!DNL Query Service] måste du ange namnet på måldatauppsättningen. Du kan generera de nödvändiga kodcellerna genom att söka efter den önskade datauppsättningen med **Data Explorer**. Högerklicka på datauppsättningslistan och klicka på **Fråga data i anteckningsbok** för att generera följande två kodceller i anteckningsboken:


För att kunna använda [!DNL Query Service] i måste [!DNL JupyterLab]du först skapa en anslutning mellan din fungerande [!DNL Python] anteckningsbok och [!DNL Query Service]. Detta kan du göra genom att köra den första genererade cellen.

```python
qs_connect()
```

I den andra genererade cellen måste den första raden definieras före SQL-frågan. Som standard definierar den genererade cellen en valfri variabel (`df0`) som sparar frågeresultatet som en Pandas-dataram. <br>Argumentet `-c QS_CONNECTION` är obligatoriskt och anger att kernel ska köra SQL-frågan mot [!DNL Query Service]. En lista med ytterligare argument finns i [bilagan](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python-variabler kan refereras direkt i en SQL-fråga med hjälp av strängformaterad syntax och genom att variabler omsluts med klammerparenteser (`{}`), vilket visas i följande exempel:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrera ExperienceEvent-data i [!DNL Python]/R

För att få tillgång till och filtrera en ExperienceEvent-datauppsättning i en [!DNL Python] eller R-anteckningsbok måste du ange ID:t för datauppsättningen (`{DATASET_ID}`) tillsammans med filterreglerna som definierar ett specifikt tidsintervall med hjälp av logiska operatorer. När ett tidsintervall definieras, ignoreras alla angivna sidnumreringar och hela datauppsättningen beaktas.

En lista med filtreringsoperatorer beskrivs nedan:

* `eq()`: Equal to
* `gt()`: Greater than
* `ge()`: Greater than or equal to
* `lt()`: Less than
* `le()`: Less than or equal to
* `And()`: Logiskt AND-operator
* `Or()`: Logiskt OR-operator

Följande celler filtrerar en ExperienceEvent-datauppsättning till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrera ExperienceEvent-data i PySpark/[!DNL Spark]

Om du vill komma åt och filtrera en ExperienceEvent-datauppsättning i en PySpark- eller Scala-anteckningsbok måste du ange datamängdens identitet (`{DATASET_ID}`), organisationens IMS-identitet och filterreglerna som definierar ett visst tidsintervall. Ett filtertidsintervall definieras med funktionen `spark.sql()`där funktionsparametern är en SQL-frågesträng.

Följande celler filtrerar en ExperienceEvent-datauppsättning till data som finns exklusivt mellan 1 januari 2019 och 31 december 2019.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>
>I Scala kan du använda `sys.env()` för att deklarera och returnera ett värde inifrån `option`. Detta eliminerar behovet av att definiera variabler om du vet att de bara kommer att användas en gång. Följande exempel tar `val userToken` från exemplet ovan och deklarerar det textbundet `option` som ett alternativ:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Bibliotek som stöds {#supported-libraries}

### [!DNL Python] / R

| Bibliotek | Version |
| :------ | :------ |
| anteckningsbok | 6.0.0 |
| förfrågningar | 2.22.0 |
| platt | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1.6 |
| kart | 2.2.4 |
| nltk | 3.2.5 |
| pandor | 0.22.0 |
| pandasql | 0.7.3 |
| kudde | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| scipy | 1.3.0 |
| klippa | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodels | 0.10.1 |
| vetenskapsman | 5.1.0.17 |
| ggplot | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| färgolover | 0.3.0 |
| geopandos | 0.5.1 |
| pyshp | 2.1.0 |
| formlig | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-aruler | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-leaps | 3.0 |
| r-manipulera | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-stan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-överlevnad | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-prognos | 8.7 |
| r-rsolnp | 1.16 |
| r-retikera | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-korrplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pipa | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fastparquet | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure-storage | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandor_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| näsa | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| pappersmaskin | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimportör | 0.3.1 |

### PySpark

| Bibliotek | Version |
| :------ | :------ |
| förfrågningar | 2.18.4 |
| gensim | 2.3.0 |
| kart | 2.0.6 |
| nltk | 3.2.4 |
| pandor | 0.20.1 |
| pandasql | 0.7.3 |
| kudde | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scipy | 0.19.1 |
| klippa | 1.3.3 |
| statsmodels | 0.8.0 |
| vetenskapsman | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pipa | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |

## Valfria SQL-flaggor för [!DNL Query Service] {#optional-sql-flags-for-query-service}

Den här tabellen visar de valfria SQL-flaggor som kan användas för [!DNL Query Service].

| **Flagga** | **Beskrivning** |
| --- | --- |
| `-h`, `--help` | Visa hjälpmeddelandet och avsluta. |
| `-n`, `--notify` | Växla alternativ för att meddela frågeresultat. |
| `-a`, `--async` | Om du använder den här flaggan körs frågan asynkront och kerneln kan frigöras medan frågan körs. Var försiktig när du tilldelar frågeresultat till variabler eftersom de kan vara odefinierade om frågan inte är fullständig. |
| `-d`, `--display` | Om du använder den här flaggan kan du inte visa resultat. |

