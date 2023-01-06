---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;jupyterlab
solution: Experience Platform
title: Översikt över användargränssnittet i JupyterLab
description: JupyterLab är ett webbaserat användargränssnitt för Project Jupyter och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyter-anteckningsböcker, kod och data. Det här dokumentet innehåller en översikt över JupyterLab och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---

# [!DNL JupyterLab] Översikt över användargränssnittet

[!DNL JupyterLab] är ett webbaserat användargränssnitt för [Project Jupyter](https://jupyter.org/) och är nära integrerat i Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyter-anteckningsböcker, kod och data.

Dokumentet innehåller en översikt över [!DNL JupyterLab] och dess funktioner samt instruktioner för att utföra vanliga åtgärder.

## [!DNL JupyterLab] på [!DNL Experience Platform]

Integreringen av Experience Platform JupyterLab åtföljs av arkitektoniska förändringar, designöverväganden, anpassade utbyggnadsmoduler för bärbara datorer, förinstallerade bibliotek och ett gränssnitt med Adobe-teman.

I följande lista beskrivs några av funktionerna som är unika för JupyterLab på Platform:

| Funktion | Beskrivning |
| --- | --- |
| **Kernlar** | Kerneler har bärbara datorer och andra [!DNL JupyterLab] I gränssnittet kan du köra och granska kod i olika programmeringsspråk. [!DNL Experience Platform] har ytterligare kernel som stöd för utveckling i [!DNL Python], R, PySpark, och [!DNL Spark]. Se [kernels](#kernels) för mer information. |
| **Dataåtkomst** | Få tillgång till befintliga datauppsättningar direkt inifrån [!DNL JupyterLab] med fullt stöd för läs- och skrivfunktioner. |
| **[!DNL Platform]tjänstintegration** | Inbyggda integreringar gör att du kan använda andra [!DNL Platform] tjänster direkt inifrån [!DNL JupyterLab]. En fullständig lista över integreringar som stöds finns i avsnittet om [Integrering med andra plattformstjänster](#service-integration). |
| **Autentisering** | Förutom <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab:s inbyggda säkerhetsmodell</a>, krypteras och autentiseras all interaktion mellan applikationen och Experience Platform, inklusive kommunikation från tjänst till tjänst, via <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Utvecklingsbibliotek** | I [!DNL Experience Platform], [!DNL JupyterLab] innehåller förinstallerade bibliotek för [!DNL Python], R och PySpark. Se [appendix](#supported-libraries) för en fullständig lista över bibliotek som stöds. |
| **Bibliotekshanterare** | När de förinstallerade biblioteken saknas för dina behov kan ytterligare bibliotek installeras för Python och R, och lagras tillfälligt i isolerade behållare för att bibehålla integriteten hos [!DNL Platform] och skydda era data. Se [kernels](#kernels) för mer information. |

>[!NOTE]
>
>Ytterligare bibliotek är bara tillgängliga för den session där de installerades. Du måste installera om alla ytterligare bibliotek som du behöver när du startar nya sessioner.

## Integrering med andra [!DNL Platform] tjänster {#service-integration}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. Integreringen av [!DNL JupyterLab] på [!DNL Platform] som en inbäddad IDE-miljö som gör att den kan interagera med andra [!DNL Platform] tjänster, så att du kan använda [!DNL Platform] till fullo utnyttja sin potential. Följande [!DNL Platform] finns i [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Få tillgång till och utforska datauppsättningar med läs- och skrivfunktioner.
* **[!DNL Query Service]:** Få åtkomst till och utforska datauppsättningar med SQL, vilket ger lägre dataåtkomstkostnader när du hanterar stora mängder data.
* **[!DNL Sensei ML Framework]:** Modellutveckling med möjlighet att träna och poängsätta data, liksom att skapa recept med ett enda klick.
* **[!DNL Experience Data Model (XDM)]:** Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en)som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

>[!NOTE]
>
>Några [!DNL Platform] tjänstintegreringar på [!DNL JupyterLab] begränsas till särskilda kärnor. Se avsnittet om [kernels](#kernels) för mer information.

## Viktiga funktioner och vanliga åtgärder

Information om viktiga funktioner i [!DNL JupyterLab] och instruktioner om hur man utför vanliga åtgärder finns i avsnitten nedan:

* [Åtkomst till JupyterLab](#access-jupyterlab)
* [Gränssnittet JupyterLab](#jupyterlab-interface)
* [Kodceller](#code-cells)
* [Kernlar](#kernels)
* [Kernel-sessioner](#kernel-sessions)
* [Startprogram](#launcher)

### Öppna [!DNL JupyterLab] {#access-jupyterlab}

I [Adobe Experience Platform](https://platform.adobe.com), markera **[!UICONTROL Notebooks]** från den vänstra navigeringskolumnen. Ge lite tid till [!DNL JupyterLab] för att initiera.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] gränssnitt {#jupyterlab-interface}

The [!DNL JupyterLab] -gränssnittet består av en menyrad, ett infällbart vänster sidofält och huvudarbetsytan som innehåller flikar med dokument och aktiviteter.

**Menyrad**

Menyraden högst upp i gränssnittet har menyer på översta nivån som visar åtgärder som är tillgängliga i [!DNL JupyterLab] med sina kortkommandon:

* **Fil:** Åtgärder för filer och kataloger
* **Redigera:** Åtgärder som rör redigering av dokument och andra aktiviteter
* **Visa:** Åtgärder som ändrar utseendet på [!DNL JupyterLab]
* **Kör:** Åtgärder för att köra kod i olika aktiviteter, t.ex. anteckningsböcker och kodkonsoler
* **Kernel:** Åtgärder för hantering av kärnor
* **Tabbar:** En lista över öppna dokument och aktiviteter
* **Inställningar:** Vanliga inställningar och en avancerad inställningsredigerare
* **Hjälp:** En lista med [!DNL JupyterLab] och kernelhjälplänkar

**Vänster sidofält**

Den vänstra sidlisten innehåller klickbara flikar som ger åtkomst till följande funktioner:

* **Filwebbläsare:** En lista över sparade anteckningsboksdokument och kataloger
* **Datautforskaren:** Bläddra bland, få tillgång till och utforska datauppsättningar och scheman
* **Löpande kärnor och terminaler:** En lista över aktiva kernel- och terminalsessioner med möjlighet att avsluta
* **Kommandon:** En lista med användbara kommandon
* **Cellkontroll:** En cellredigerare som ger tillgång till verktyg och metadata som är användbara när du ställer in en anteckningsbok för presentationsändamål
* **tabbar:** En lista med öppna flikar

Markera en flik för att visa dess funktioner, eller markera den på en utökad flik för att komprimera den vänstra sidopanelen så som visas nedan:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Huvudarbetsyta**

Huvudarbetsytan i [!DNL JupyterLab] I kan du ordna dokument och andra aktiviteter i flikpaneler som kan storleksändras eller delas upp. Dra en flik till mitten av en tabbpanel för att migrera fliken. Dela upp en panel genom att dra en flik till vänster, höger, överst eller nederst på panelen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- och minnesserverkonfiguration i [!DNL Python]/R

I [!DNL JupyterLab] markera kugghjulsikonen i det övre högra hörnet för att öppna *Konfiguration av anteckningsboksserver*. Du kan växla GPU på och tilldela den mängd minne du behöver med hjälp av skjutreglaget. Hur mycket minne du kan allokera beror på hur mycket organisationen har allokerat. Välj **[!UICONTROL Update configs]** att spara.

>[!NOTE]
>
>Endast en GPU tilldelas per organisation för bärbara datorer. Om grafikprocessorn används måste du vänta på att den användare som för närvarande har reserverat grafikprocessorn ska frisläppa den. Detta kan du göra genom att logga ut eller lämna GPU:n i viloläge i fyra eller fler timmar.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Avsluta och starta om [!DNL JupyterLab]

I [!DNL JupyterLab]kan du avsluta din session för att förhindra att ytterligare resurser används. Börja med att välja **ikon för ström** ![ikon för ström](../images/jupyterlab/user-guide/power_button.png)väljer **[!UICONTROL Shut Down]** från poveren som verkar avsluta sessionen. Anteckningsbokssessioner avslutas automatiskt efter 12 timmars ingen aktivitet.

Starta om [!DNL JupyterLab]väljer du **omstartsikon** ![omstartsikon](../images/jupyterlab/user-guide/restart_button.png) placerad direkt till vänster om strömikonen och välj **[!UICONTROL Restart]** från poveren som visas.

![avsluta jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Kodceller {#code-cells}

Kodceller är det primära innehållet i anteckningsböcker. De innehåller källkod på samma språk som anteckningsbokens associerade kärna och utdata som ett resultat av körningen av kodcellen. Ett körningsantal visas till höger om varje kodcell som representerar dess körningsordning.

![](../images/jupyterlab/user-guide/code_cell.png)

Vanliga cellåtgärder beskrivs nedan:

* **Lägg till en cell:** Klicka på plustecknet (**+**) på anteckningsbokens meny för att lägga till en tom cell. Nya celler placeras under den cell som för närvarande interagerar med, eller i slutet av anteckningsboken om ingen viss cell är i fokus.

* **Flytta en cell:** Placera markören till höger om cellen som du vill flytta, klicka och dra sedan cellen till en ny plats. Om du flyttar en cell från en anteckningsbok till en annan kopieras cellen tillsammans med dess innehåll.

* **Kör en cell:** Klicka på texten i cellen som du vill köra och klicka sedan på **play** ikon (**Tourism**) på anteckningsbokens meny. En asterisk (**\***) visas i cellens körningsräknare när kärnan bearbetar körningen och ersätts med ett heltal när den är klar.

* **Ta bort en cell:** Klicka på cellen som du vill ta bort och klicka sedan på **sax** ikon.

### Kernlar {#kernels}

Anteckningsbokskärnor är språkspecifika datormotorer för bearbetning av bärbara datorer. Förutom [!DNL Python], [!DNL JupyterLab] har ytterligare språkstöd i R, PySpark och [!DNL Spark] (Scala). När du öppnar ett anteckningsboksdokument startas den tillhörande kärnan. När en anteckningsbokscell körs utför kärnan beräkningen och ger resultat som kan ta mycket processorkraft och minnesresurser i anspråk. Observera att allokerat minne inte frigörs förrän kärnan stängs av.

Vissa funktioner är begränsade till särskilda kärnor enligt tabellen nedan:

| Kernel | Installationsstöd för bibliotek | [!DNL Platform] integreringar |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nej | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-sessioner {#kernel-sessions}

Varje aktiv anteckningsbok eller aktivitet på [!DNL JupyterLab] använder en kernel-session. Alla aktiva sessioner kan hittas genom att utöka **Löpande terminaler och kärnor** från vänster sidospalt. Den bärbara datorns typ och tillstånd för kärnan kan identifieras genom att man observerar den övre högra delen av gränssnittet. I diagrammet nedan är anteckningsbokens tillhörande kärna **[!DNL Python]3** och det aktuella läget representeras av en grå cirkel till höger. En ihålig cirkel innebär en inaktiv kärna och en fylld cirkel betyder en upptagen kärna.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Om kärnan är avstängd eller inaktiv under en längre tid, ska du **Ingen kernel!** med en fylld cirkel visas. Aktivera en kärna genom att klicka på kernelstatusen och välja lämplig kerneltyp enligt nedan:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Startprogram {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Den anpassade *Startprogram* innehåller användbara mallar för bärbara datorer för de kernel som stöds som hjälper dig att komma igång snabbt, inklusive:

| Mall | Beskrivning |
| --- | --- |
| Tom | En tom anteckningsboksfil. |
| Starter | En förfylld anteckningsbok som visar datautforskandet med exempeldata. |
| Detaljhandel | En förfylld anteckningsbok med [säljrecept](../pre-built-recipes/retail-sales.md) med exempeldata. |
| Recipe Builder | En anteckningsboksmall för att skapa ett recept i [!DNL JupyterLab]. Den är förfylld med kod och kommentarer som demonstrerar och beskriver processen att skapa recept. Se [självstudiekurs om anteckningsbok till recept](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) för en detaljerad genomgång. |
| [!DNL Query Service] | En förfylld anteckningsbok som visar hur [!DNL Query Service] direkt i [!DNL JupyterLab] med exempelarbetsflöden som analyserar data i stor skala. |
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

Så här öppnar du en ny *Startprogram*, klicka **Arkiv > Nytt startprogram**. Du kan även utöka **Filläsare** från vänster sidofält och klicka på plustecknet (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Nästa steg

Om du vill veta mer om var och en av de bärbara datorer som stöds och hur du använder dem går du till [Dataåtkomst för Jupyterlab-anteckningsböcker](./access-notebook-data.md) utvecklarhandbok. Den här guiden fokuserar på hur du använder JupyterLab-anteckningsböcker för att få tillgång till dina data, inklusive läsning, skrivning och frågor. Dataåtkomstguiden innehåller även information om den maximala mängden data som kan läsas av varje bärbar dator som stöds.

## Bibliotek som stöds {#supported-libraries}

Kopiera och klistra in om du vill se en lista över paket som stöds i Python, R och PySpark `!conda list` i en ny cell och kör sedan cellen. En lista över paket som stöds visas i alfabetisk ordning.

![exempel](../images/jupyterlab/user-guide/libraries.PNG)

Dessutom används följande beroenden, som inte finns med i listan:
* CUDA 11.2
* CUDNN 8.1

