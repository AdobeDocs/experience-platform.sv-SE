---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;jupyterlab
solution: Experience Platform
title: Översikt över användargränssnittet i JupyterLab
topic: Översikt
description: JupyterLab är ett webbaserat användargränssnitt för Project Jupyter och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyter-anteckningsböcker, kod och data. Det här dokumentet innehåller en översikt över JupyterLab och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.
translation-type: tm+mt
source-git-commit: 23128fb481452b558c52f962f78ae638fc1f0418
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# [!DNL JupyterLab] Översikt över användargränssnittet

[!DNL JupyterLab] är ett webbaserat användargränssnitt för  [Project ](https://jupyter.org/) Jupyteroch är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyter-anteckningsböcker, kod och data.

Det här dokumentet innehåller en översikt över [!DNL JupyterLab] och dess funktioner samt instruktioner om hur du utför vanliga åtgärder.

## [!DNL JupyterLab] på  [!DNL Experience Platform]

Integreringen av Experience Platform JupyterLab åtföljs av arkitektoniska förändringar, designöverväganden, anpassade utbyggnadsmoduler för bärbara datorer, förinstallerade bibliotek och ett gränssnitt med Adobe-teman.

I följande lista beskrivs några av funktionerna som är unika för JupyterLab på Platform:

| Funktion | Beskrivning |
| --- | --- |
| **Kernlar** | Kernels ger dig möjlighet att köra och granska kod i olika programmeringsspråk med [!DNL JupyterLab] front end. [!DNL Experience Platform] har ytterligare kernel som stöder utveckling i  [!DNL Python], R, PySpark och  [!DNL Spark]. Mer information finns i avsnittet [kernels](#kernels). |
| **Dataåtkomst** | Få tillgång till befintliga datauppsättningar direkt inifrån [!DNL JupyterLab] med fullt stöd för läs- och skrivfunktioner. |
| **[!DNL Platform]tjänstintegration** | Inbyggda integreringar gör att du kan använda andra [!DNL Platform]-tjänster direkt inifrån [!DNL JupyterLab]. En fullständig lista över integreringar som stöds finns i avsnittet [Integrering med andra plattformstjänster](#service-integration). |
| **Autentisering** | Förutom <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab:s inbyggda säkerhetsmodell</a> krypteras och autentiseras all interaktion mellan ditt program och Experience Platform, inklusive kommunikation från tjänst till tjänst för plattform, via <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Utvecklingsbibliotek** | I [!DNL Experience Platform] innehåller [!DNL JupyterLab] förinstallerade bibliotek för [!DNL Python], R och PySpark. I [bilagan](#supported-libraries) finns en fullständig lista över bibliotek som stöds. |
| **Bibliotekshanterare** | När de förinstallerade biblioteken saknas för dina behov kan ytterligare bibliotek installeras för Python och R, och lagras tillfälligt i isolerade behållare för att bibehålla integriteten hos [!DNL Platform] och skydda dina data. Mer information finns i avsnittet [kernels](#kernels). |

>[!NOTE]
>
>Ytterligare bibliotek är bara tillgängliga för den session där de installerades. Du måste installera om alla ytterligare bibliotek som du behöver när du startar nya sessioner.

## Integrering med andra [!DNL Platform]-tjänster {#service-integration}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. Integreringen av [!DNL JupyterLab] på [!DNL Platform] som en inbäddad IDE gör att den kan interagera med andra [!DNL Platform]-tjänster, vilket gör att du kan utnyttja [!DNL Platform] till fullo. Följande [!DNL Platform]-tjänster är tillgängliga i [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Använd och utforska datauppsättningar med läs- och skrivfunktioner.
* **[!DNL Query Service]:** Få tillgång till och utforska datauppsättningar med SQL, vilket ger lägre dataåtkomstkostnader när du hanterar stora mängder data.
* **[!DNL Sensei ML Framework]:** Modellutveckling med möjlighet att träna och poängsätta data, liksom att skapa recept med ett enda klick.
* **[!DNL Experience Data Model (XDM)]:** Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

>[!NOTE]
>
>Vissa [!DNL Platform]-tjänstintegreringar på [!DNL JupyterLab] är begränsade till specifika kärnor. Mer information finns i avsnittet [kernels](#kernels).

## Viktiga funktioner och vanliga åtgärder

Information om de viktigaste funktionerna i [!DNL JupyterLab] och anvisningar om hur du utför vanliga åtgärder finns i avsnitten nedan:

* [Åtkomst till JupyterLab](#access-jupyterlab)
* [Gränssnittet JupyterLab](#jupyterlab-interface)
* [Kodceller](#code-cells)
* [Kernlar](#kernels)
* [Kernel-sessioner](#kernel-sessions)
* [Startprogram](#launcher)

### Öppna [!DNL JupyterLab] {#access-jupyterlab}

I [Adobe Experience Platform](https://platform.adobe.com) väljer du **[!UICONTROL Notebooks]** i den vänstra navigeringskolumnen. Ge [!DNL JupyterLab] tid att initiera helt.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] gränssnitt  {#jupyterlab-interface}

Gränssnittet [!DNL JupyterLab] består av en menyrad, ett fällbart sidofält och huvudarbetsytan som innehåller flikar med dokument och aktiviteter.

**Menyrad**

Menyraden högst upp i gränssnittet har menyer på översta nivån som visar åtgärder som är tillgängliga i [!DNL JupyterLab] med deras kortkommandon:

* **Arkiv:** Åtgärder för filer och kataloger
* **Redigera:** Åtgärder för att redigera dokument och andra aktiviteter
* **Visa:** Åtgärder som ändrar utseendet på  [!DNL JupyterLab]
* **Kör:** Åtgärder för att köra kod i olika aktiviteter som anteckningsböcker och kodkonsoler
* **kernel:** Åtgärder för att hantera kärnor
* **Tabbar:** En lista med öppna dokument och aktiviteter
* **inställningar:** Vanliga inställningar och en avancerad inställningsredigerare
* **Hjälp:** En lista över  [!DNL JupyterLab] och kernelhjälplänkar

**Vänster sidofält**

Den vänstra sidlisten innehåller klickbara flikar som ger åtkomst till följande funktioner:

* **filläsare:** En lista över sparade anteckningsboksdokument och -kataloger
* **Datautforskaren:** Bläddra, få tillgång till och utforska datauppsättningar och scheman
* **Löpande kärnor och terminaler:** En lista över aktiva kernel- och terminalsessioner med möjlighet att avsluta
* **kommandon:** en lista med användbara kommandon
* **Cellinspektören:** En cellredigerare som ger tillgång till verktyg och metadata som är användbara när du ställer in en anteckningsbok för presentationsändamål
* **tabbar:** En lista med öppna flikar

Markera en flik för att visa dess funktioner, eller markera den på en utökad flik för att komprimera den vänstra sidopanelen så som visas nedan:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Huvudarbetsyta**

Huvudarbetsytan i [!DNL JupyterLab] gör att du kan ordna dokument och andra aktiviteter i flikpaneler som kan storleksändras eller delas upp. Dra en flik till mitten av en tabbpanel för att migrera fliken. Dela upp en panel genom att dra en flik till vänster, höger, överst eller nederst på panelen:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- och minnesserverkonfiguration i [!DNL Python]/R

I [!DNL JupyterLab] väljer du kugghjulsikonen i det övre högra hörnet för att öppna *konfigurationen av anteckningsboksservern*. Du kan växla GPU på och tilldela den mängd minne du behöver med hjälp av skjutreglaget. Hur mycket minne du kan allokera beror på hur mycket organisationen har allokerat. Välj **[!UICONTROL Update configs]** att spara.

>[!NOTE]
>
>Endast en GPU tilldelas per organisation för bärbara datorer. Om grafikprocessorn används måste du vänta på att den användare som för närvarande har reserverat grafikprocessorn ska frisläppa den. Detta kan du göra genom att logga ut eller lämna GPU:n i viloläge i fyra eller fler timmar.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Avsluta och starta om [!DNL JupyterLab]

I [!DNL JupyterLab] kan du avsluta din session för att förhindra att fler resurser används. Börja med att välja **strömikonen** och välj sedan **[!UICONTROL Shut Down]** i den pover som visas för att avsluta sessionen. Anteckningsbokssessioner avslutas automatiskt efter 12 timmars ingen aktivitet.

Om du vill starta om [!DNL JupyterLab] väljer du ikonen **starta om** som finns direkt till vänster om strömikonen och väljer sedan **[!UICONTROL Restart]** i den pover som visas.

![avsluta jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Kodceller {#code-cells}

Kodceller är det primära innehållet i anteckningsböcker. De innehåller källkod på samma språk som anteckningsbokens associerade kärna och utdata som ett resultat av körningen av kodcellen. Ett körningsantal visas till höger om varje kodcell som representerar dess körningsordning.

![](../images/jupyterlab/user-guide/code_cell.png)

Vanliga cellåtgärder beskrivs nedan:

* **Lägg till en cell:** Klicka på plustecknet (**+**) på anteckningsboksmenyn för att lägga till en tom cell. Nya celler placeras under den cell som för närvarande interagerar med, eller i slutet av anteckningsboken om ingen viss cell är i fokus.

* **Flytta en cell:** Placera markören till höger om cellen som du vill flytta, klicka och dra sedan cellen till en ny plats. Om du flyttar en cell från en anteckningsbok till en annan kopieras cellen tillsammans med dess innehåll.

* **Kör en cell:** Klicka på brödtexten i den cell som du vill köra och klicka sedan på  **** uppspelningsikonen (**▶**) på anteckningsbokens meny. En asterisk (**\***) visas i cellens körningsräknare när kärnan bearbetar körningen och ersätts med ett heltal när den är klar.

* **Ta bort en cell:** Klicka på cellen som du vill ta bort och klicka sedan på  **** saxikonen.

### Kernlar {#kernels}

Anteckningsbokskärnor är språkspecifika datormotorer för bearbetning av bärbara datorer. Förutom [!DNL Python] har [!DNL JupyterLab] stöd för ytterligare språk i R, PySpark och [!DNL Spark] (Scala). När du öppnar ett anteckningsboksdokument startas den tillhörande kärnan. När en anteckningsbokscell körs utför kärnan beräkningen och ger resultat som kan ta mycket processorkraft och minnesresurser i anspråk. Observera att allokerat minne inte frigörs förrän kärnan stängs av.

Vissa funktioner är begränsade till särskilda kärnor enligt tabellen nedan:

| Kernel | Installationsstöd för bibliotek | [!DNL Platform] integreringar |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nej | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-sessioner {#kernel-sessions}

Varje aktiv anteckningsbok eller aktivitet på [!DNL JupyterLab] använder en kernel-session. Alla aktiva sessioner kan hittas genom att utöka fliken **Löpande terminaler och kernlar** från vänster sidofält. Den bärbara datorns typ och tillstånd för kärnan kan identifieras genom att man observerar den övre högra delen av gränssnittet. I diagrammet nedan är anteckningsbokens associerade kärna **[!DNL Python]3** och det aktuella läget representeras av en grå cirkel till höger. En ihålig cirkel innebär en inaktiv kärna och en fylld cirkel betyder en upptagen kärna.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Om kärnan är avstängd eller inaktiv under en längre period är **Ingen kernel!** med en fylld cirkel visas. Aktivera en kärna genom att klicka på kernelstatusen och välja lämplig kerneltyp enligt nedan:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Startprogram {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Med den anpassade *Launcher* får du användbara anteckningsboksmallar för de paneler som stöds så att du snabbt kan komma igång med uppgiften, inklusive:

| Mall | Beskrivning |
| --- | --- |
| Tom | En tom anteckningsboksfil. |
| Starter | En förfylld anteckningsbok som visar datautforskandet med exempeldata. |
| Detaljhandel | En förfylld anteckningsbok med [säljrecept](https://adobe.ly/2wOgO3L) som innehåller exempeldata. |
| Recipe Builder | En anteckningsboksmall för att skapa ett recept i [!DNL JupyterLab]. Den är förfylld med kod och kommentarer som demonstrerar och beskriver processen att skapa recept. Se självstudiekursen ](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) för en detaljerad genomgång i [anteckningsboken om du vill recensera. |
| [!DNL Query Service] | En förfylld anteckningsbok som visar hur [!DNL Query Service] används direkt i [!DNL JupyterLab] med medföljande exempelarbetsflöden som analyserar data i stor skala. |
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

Om du vill öppna en ny *startfil* klickar du på **Arkiv > Ny startare**. Du kan även expandera filläsaren **** från vänster sidofält och klicka på plustecknet (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Nästa steg

Om du vill veta mer om de bärbara datorer som stöds och hur du använder dem kan du gå till utvecklarhandboken för [Jupyterlab-anteckningsböcker och dataåtkomst](./access-notebook-data.md). Den här guiden fokuserar på hur du använder JupyterLab-anteckningsböcker för att få tillgång till dina data, inklusive läsning, skrivning och frågor. Dataåtkomstguiden innehåller även information om den maximala mängden data som kan läsas av varje bärbar dator som stöds.

## Bibliotek som stöds {#supported-libraries}

Om du vill visa en lista över paket som stöds i Python, R och PySpark kopierar och klistrar du in `!pip list --format=columns` i en ny cell och kör sedan cellen. En lista över paket som stöds visas i alfabetisk ordning.

![exempel](../images/jupyterlab/user-guide/libraries.PNG)