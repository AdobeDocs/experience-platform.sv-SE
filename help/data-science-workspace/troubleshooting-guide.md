---
keywords: Experience Platform;felsökning;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Data Science Workspace Troubleshooting Guide
description: Här hittar du svar på vanliga frågor om Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# [!DNL Data Science Workspace] felsökningsguide

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Data Science Workspace]. Mer information och felsökning om [!DNL Experience Platform] API:er i allmänhet finns i [felsökningsguiden för Adobe Experience Platform API](../landing/troubleshooting.md).

## JupyterLab-frågans status för anteckningsbok fastsatt i körningstillståndet

En JupyterLab-anteckningsbok kan indikera att en cell är i körningsläge, i oändlighet, under vissa minnesförhållanden. Om du till exempel skickar en fråga till en stor datauppsättning eller utför flera efterföljande frågor kan JupyterLab-anteckningsboken ta slut på tillgängligt minne för att lagra det resulterande dataframe-objektet. Det finns några indikatorer som kan ses i denna situation. Först försätts kärnan i inaktivt läge även om cellen visas som körd, vilket anges av ikonen [`*`] bredvid cellen. Dessutom anger det nedre fältet mängden RAM-minne som används/är tillgängligt.

![Tillgängligt RAM](./images/jupyterlab/user-guide/allocate-ram.png)

Under läsningen av data kan minnet växa tills det når maximal mängd allokerat minne. Minnet frigörs så snart som det maximala minnet nås och kärnan startas om. Det innebär att det använda minnet i det här scenariot kan visa sig vara mycket lågt på grund av att kärnan har startats om, medan minnet precis före omstarten skulle ha legat mycket nära det maximalt allokerade RAM-minnet.

Du löser det här problemet genom att välja kugghjulsikonen i det övre högra hörnet av JupyterLab och dra reglaget åt höger följt av att välja **[!UICONTROL Update configs]** för att tilldela mer RAM-minne. Om du kör flera frågor och RAM-värdet närmar sig det maximala allokerade beloppet, såvida du inte behöver resultaten från tidigare frågor, startar du om kärnan för att återställa det tillgängliga RAM-minnet. Detta garanterar att du har maximalt tillgängligt RAM-minne för den aktuella frågan.

![allokera mer ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Om du tilldelar maximalt minne (RAM) och fortfarande stöter på det här problemet, kan du ändra frågan så att den fungerar med en mindre datauppsättningsstorlek genom att minska kolumnerna eller dataintervallet. Om du vill använda hela datamängden rekommenderar vi att du använder en bärbar Spark-dator.

## Miljön [!DNL JupyterLab] läses inte in i [!DNL Google Chrome]

>[!IMPORTANT]
>
>Problemet har åtgärdats men kan fortfarande finnas i webbläsaren Google Chrome 80.x. Kontrollera att webbläsaren i Chrome är uppdaterad.

Med webbläsarversionen [!DNL Google Chrome] 80.x blockeras alla cookies från tredje part som standard. Den här principen kan förhindra att [!DNL JupyterLab] läses in i Adobe Experience Platform.

Så här åtgärdar du problemet:

Navigera till det övre högra hörnet i din [!DNL Chrome]-webbläsare och välj **Inställningar** (du kan också kopiera och klistra in &quot;chrome://settings/&quot; i adressfältet). Bläddra sedan längst ned på sidan och klicka på listrutan **Avancerat**.

![Krom avancerad](./images/faq/chrome-advanced.png)

Avsnittet **Sekretess och säkerhet** visas. Klicka sedan på **Webbplatsinställningar** följt av **Cookies och webbplatsdata**.

![Krom avancerad](./images/faq/privacy-security.png)

![Krom avancerad](./images/faq/cookies.png)

Slutligen växlar du Blockera cookies från tredje part till AV.

![Krom avancerad](./images/faq/toggle-off.png)

>[!NOTE]
>
>Du kan även inaktivera cookies från tredje part och lägga till [*.]ds.adobe.net till tillåtelselista.

Gå till&quot;chrome://flags/&quot; i adressfältet. Sök efter och inaktivera flaggan *&quot;SameSite som standard-cookies&quot;* med hjälp av listrutan till höger.

![inaktivera samma webbplatsflagga](./images/faq/samesite-flag.png)

Efter steg 2 uppmanas du att starta om webbläsaren. När du har startat om bör [!DNL Jupyterlab] vara tillgänglig.

## Varför kan jag inte komma åt [!DNL JupyterLab] i Safari?

Safari inaktiverar cookies från tredje part som standard i Safari &lt; 12. Eftersom instansen av den virtuella datorn [!DNL Jupyter] finns på en annan domän än den överordnade bildrutan kräver Adobe Experience Platform för närvarande att cookies från tredje part aktiveras. Aktivera cookies från tredje part eller växla till en annan webbläsare, till exempel [!DNL Google Chrome].

För Safari 12 måste du växla din användaragent till [!DNL Chrome] eller [!DNL Firefox]. Om du vill byta användaragent startar du med att öppna menyn *Safari* och väljer **Inställningar**. Fönstret Inställningar visas.

![Safari-inställningar](./images/faq/preferences.png)

Välj **Avancerat** i inställningsfönstret i Safari. Markera sedan *Visa menyn Framkalla i menyraden*. Du kan stänga inställningsfönstret när det här steget är klart.

![Safari avancerat](./images/faq/advanced.png)

Välj sedan menyn **Framkalla** i det övre navigeringsfältet. Håll muspekaren över **användaragenten** i listrutan **Framkalla**. Du kan välja den **[!DNL Chrome]**- eller **[!DNL Firefox]** användaragentsträng som du vill använda.

![Menyn Framkalla](./images/faq/user-agent.png)

## Varför visas ett 403-förbjudet meddelande när jag försöker överföra eller ta bort en fil i [!DNL JupyterLab]?

Om din webbläsare är aktiverad med annonseringsblockerande program som [!DNL Ghostery] eller [!DNL AdBlock] Plus måste domänen &quot;\*.adobe.net&quot; tillåtas i varje annonsblockerande programvara för att [!DNL JupyterLab] ska fungera normalt. Detta beror på att [!DNL JupyterLab] virtuella datorer körs på en annan domän än [!DNL Experience Platform]-domänen.

## Varför ser vissa delar av [!DNL Jupyter Notebook] ut att vara förvrängda eller återges inte som kod?

Detta kan inträffa om cellen i fråga oavsiktligt ändras från &quot;Kod&quot; till &quot;Markering&quot;. När en kodcell är i fokus ändras celltypen till Markdown om du trycker på tangentkombinationen **ESC+M**. En cells typ kan ändras med listrutemätaren högst upp i anteckningsboken för de markerade cellerna. Om du vill ändra en celltyp till kod börjar du med att markera den cell som du vill ändra. Klicka sedan på listrutan som anger cellens aktuella typ och välj sedan &quot;Kod&quot;.

![](./images/faq/code_type.png)

## Hur installerar jag anpassade [!DNL Python]-bibliotek?

Kerneln [!DNL Python] är förinstallerad med många vanliga maskininlärningsbibliotek. Du kan dock installera ytterligare anpassade bibliotek genom att köra följande kommando i en kodcell:

```shell
!pip install {LIBRARY_NAME}
```

En fullständig lista över förinstallerade [!DNL Python]-bibliotek finns i avsnittet [appendix i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Kan jag installera egna PySpark-bibliotek?

Tyvärr kan du inte installera fler bibliotek för PySpark-kärnan. Du kan dock kontakta Adobe kundtjänstrepresentant för att få anpassade PySpark-bibliotek installerade åt dig.

En lista över förinstallerade PySpark-bibliotek finns i avsnittet [appendix i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Är det möjligt att konfigurera [!DNL Spark] klusterresurser för [!DNL JupyterLab] [!DNL Spark]- eller PySpark-kärnan?

Du kan konfigurera resurser genom att lägga till följande block i den första cellen i anteckningsboken:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Mer information om [!DNL Spark]-klusterresurskonfigurationen, inklusive en fullständig lista över konfigurerbara egenskaper, finns i [användarhandboken för JupyterLab](./jupyterlab/overview.md#kernels).

## Varför får jag ett fel när jag försöker köra vissa uppgifter för större datamängder?

Om du får ett fel av en anledning som `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` innebär det vanligtvis att drivrutinen eller en körare har slut på minne. Mer information om datagränser och hur du kör uppgifter på stora datauppsättningar finns i dokumentationen för JupyterLab-anteckningsböcker [dataåtkomst](./jupyterlab/access-notebook-data.md) . Vanligtvis kan det här felet lösas genom att `mode` ändras från `interactive` till `batch`.

När du skriver stora Spark-/PySpark-datauppsättningar kan du dessutom förbättra prestandan avsevärt genom att cacha dina data (`df.cache()`) innan du kör skrivkoden.

<!-- remove this paragraph at a later date once the sdk is updated -->

Om du får problem med att läsa data och använder omformningar på data kan du försöka med att cachelagra data före omformningarna. Cachelagring av data förhindrar flera läsningar i nätverket. Börja med att läsa data. Sedan cachelagrar `df.cache()` data. Till sist kan du göra dina omformningar.

## Varför tar mina bärbara Spark/PySpark-datorer så lång tid att läsa och skriva data?

Om du utför omformningar på data, till exempel använder `fit()`, kan omformningarna köras flera gånger. Om du vill öka prestandan cachelagrar du dina data med `df.cache()` innan du utför `fit()`. Detta garanterar att omvandlingarna endast utförs en gång och förhindrar flera läsningar i nätverket.

**Rekommenderad ordning:** Börja med att läsa data. Utför sedan omformningar följt av cachelagring (`df.cache()`) av data. Utför slutligen `fit()`.

## Varför fungerar inte mina Spark/PySpark-bärbara datorer?

Om du får något av följande fel:

- Jobbet avbröts på grund av ett scenfel ... Det går bara att zippa RDD-enheter med samma antal element i varje partition.
- Fjärransluten RPC-klient har kopplats från och andra minnesfel.
- Dåliga prestanda vid läsning och skrivning av datauppsättningar.

Kontrollera att du cachelagrar data (`df.cache()`) innan du skriver data. När du kör kod i anteckningsböcker kan prestandan för anteckningsboken förbättras avsevärt om du använder `df.cache()` före en åtgärd som `fit()`. Om du använder `df.cache()` innan du skriver en datauppsättning säkerställs att omformningarna bara utförs en gång i stället för flera gånger.

## [!DNL Docker Hub]-begränsningar i Data Science Workspace

Från och med den 20 november 2020 trädde avgiftsgränserna för anonym och fri autentiserad användning av Docker Hub i kraft. Anonyma och kostnadsfria [!DNL Docker Hub]-användare är begränsade till 100 begäranden om hämtning av behållarbilder var sjätte timme. Om du påverkas av dessa ändringar får du det här felmeddelandet: `ERROR: toomanyrequests: Too Many Requests.` eller `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

För närvarande påverkar den här gränsen bara din organisation om du försöker skapa 100 bärbara datorer till Recept inom en sextimmarsperiod eller om du använder Spark-baserade bärbara datorer i Data Science Workspace som ofta skalas upp och ned. Detta är dock osannolikt eftersom klustret fortfarande är aktivt i två timmar innan det går ut. Detta minskar antalet pulls som krävs när klustret är aktivt. Om du får något av ovanstående fel måste du vänta tills gränsen på [!DNL Docker] har återställts.

Mer information om hastighetsbegränsningar för [!DNL Docker Hub] finns i [DockerHub-dokumentationen](https://www.docker.com/increase-rate-limits). En lösning för detta håller på att bearbetas och förväntas bli klar i en senare version.
