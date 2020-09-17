---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Användarhandbok för JupyterLab
topic: Overview
description: JupyterLab är ett webbaserat användargränssnitt för Project Jupyter och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyters bärbara datorer, kod och data. Det här dokumentet innehåller en översikt över JupyterLab och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 6%

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
| Detaljhandel | En förfylld anteckningsbok med [säljrecept](https://adobe.ly/2wOgO3L) med exempeldata. |
| Recipe Builder | En anteckningsboksmall för att skapa ett recept i [!DNL JupyterLab]. Den är förfylld med kod och kommentarer som demonstrerar och beskriver processen att skapa recept. I den [bärbara datorn finns självstudiekurser](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) om du vill se en detaljerad genomgång. |
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

## Nästa steg

Om du vill veta mer om de bärbara datorer som stöds och hur du använder dem kan du gå till utvecklarhandboken för dataåtkomst [i](./access-notebook-data.md) Jupyterlab. Den här guiden fokuserar på hur du använder JupyterLab-anteckningsböcker för att få tillgång till dina data, inklusive läsning, skrivning och frågor. Dataåtkomstguiden innehåller även information om den maximala mängden data som kan läsas av varje bärbar dator som stöds.

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
| elastisk | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pipa | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |