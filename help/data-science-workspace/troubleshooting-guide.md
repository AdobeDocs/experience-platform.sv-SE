---
keywords: Experience Platform;felsökning;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Felsökningsguide för arbetsytan Data Science
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# [!DNL Data Science Workspace] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Data Science Workspace]. För frågor och felsökning gällande [!DNL Platform] API:er i allmänhet finns i [Felsökningsguide för Adobe Experience Platform API](../landing/troubleshooting.md).

## JupyterLab-frågans status för anteckningsbok fastsatt i körningstillståndet

En JupyterLab-anteckningsbok kan indikera att en cell är i körningsläge, i oändlighet, under vissa minnesförhållanden. Om du till exempel skickar en fråga till en stor datauppsättning eller utför flera efterföljande frågor kan JupyterLab-anteckningsboken ta slut på tillgängligt minne för att lagra det resulterande dataframe-objektet. Det finns några indikatorer som kan ses i denna situation. Först försätts kärnan i inaktivt läge även om cellen visas som den körs enligt [`*`] -ikonen bredvid cellen. Dessutom anger det nedre fältet mängden RAM-minne som används/är tillgängligt.

![Tillgängligt diagram](./images/jupyterlab/user-guide/allocate-ram.png)

Under läsningen av data kan minnet växa tills det når maximal mängd allokerat minne. Minnet frigörs så snart som det maximala minnet nås och kärnan startas om. Det innebär att det använda minnet i det här scenariot kan visa sig vara mycket lågt på grund av att kärnan har startats om, medan minnet precis före omstarten skulle ha legat mycket nära det maximalt allokerade RAM-minnet.

Lös problemet genom att välja kugghjulsikonen i det övre högra hörnet av JupyterLab och dra reglaget åt höger följt av att välja **[!UICONTROL Update configs]** för att tilldela mer RAM-minne. Om du kör flera frågor och RAM-värdet närmar sig det maximala allokerade beloppet, såvida du inte behöver resultaten från tidigare frågor, startar du om kärnan för att återställa det tillgängliga RAM-minnet. Detta garanterar att du har maximalt tillgängligt RAM-minne för den aktuella frågan.

![tilldela mer ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Om du tilldelar maximalt minne (RAM) och fortfarande stöter på det här problemet, kan du ändra frågan så att den fungerar med en mindre datauppsättningsstorlek genom att minska kolumnerna eller dataintervallet. Om du vill använda hela datamängden rekommenderar vi att du använder en bärbar Spark-dator.

## [!DNL JupyterLab] miljön läses inte in i [!DNL Google Chrome]

>[!IMPORTANT]
>
>Problemet har åtgärdats men kan fortfarande finnas i webbläsaren Google Chrome 80.x. Kontrollera att webbläsaren Chrome är uppdaterad.

Med [!DNL Google Chrome] webbläsarversion 80.x, blockeras alla cookies från tredje part som standard. Den här principen kan förhindra [!DNL JupyterLab] från inläsning i Adobe Experience Platform.

Så här åtgärdar du problemet:

I [!DNL Chrome] webbläsare, navigera till det övre högra hörnet och markera **Inställningar** (Du kan också kopiera och klistra in &quot;chrome://settings/&quot; i adressfältet). Bläddra sedan längst ned på sidan och klicka på **Avancerat** listruta.

![avancerat krom](./images/faq/chrome-advanced.png)

The **Integritet och säkerhet** visas. Klicka på **Platsinställningar** följt av **Cookies och webbplatsdata**.

![avancerat krom](./images/faq/privacy-security.png)

![avancerat krom](./images/faq/cookies.png)

Slutligen växlar du Blockera cookies från tredje part till AV.

![avancerat krom](./images/faq/toggle-off.png)

>[!NOTE]
>
>Du kan även inaktivera cookies från tredje part och lägga till [*.]ds.adobe.net till tillåtelselista.

Gå till&quot;chrome://flags/&quot; i adressfältet. Sök efter och inaktivera flaggan *&quot;SameSite som standard cookies&quot;* genom att använda listrutan till höger.

![inaktivera samma webbplatsflagga](./images/faq/samesite-flag.png)

Efter steg 2 uppmanas du att starta om webbläsaren. När du har startat om [!DNL Jupyterlab] ska vara tillgängliga.

## Varför kan jag inte komma åt [!DNL JupyterLab] i Safari?

Safari inaktiverar cookies från tredje part som standard i Safari &lt; 12. För dina [!DNL Jupyter] Instansen av den virtuella datorn finns på en annan domän än den överordnade bildrutan. Adobe Experience Platform kräver för närvarande att cookies från tredje part aktiveras. Aktivera cookies från tredje part eller byt till en annan webbläsare, till exempel [!DNL Google Chrome].

För Safari 12 måste du byta användaragent till[!DNL Chrome]&#39; eller &#39;[!DNL Firefox]&#39;. Om du vill byta användaragent startar du genom att öppna *Safari* meny och välj **Inställningar**. Inställningsfönstret visas.

![Safari-inställningar](./images/faq/preferences.png)

I inställningsfönstret i Safari väljer du **Avancerat**. Kontrollera sedan *Visa menyn Framkalla i menyraden* box. Du kan stänga inställningsfönstret när det här steget är klart.

![Safari avancerat](./images/faq/advanced.png)

I det övre navigeringsfältet väljer du **Utveckla** -menyn. Från **Utveckla** listruta, hovra över **Användaragent**. Du kan välja **[!DNL Chrome]** eller **[!DNL Firefox]** Användaragentsträng som du vill använda.

![Menyn Framkalla](./images/faq/user-agent.png)

## Varför visas ett 403-förbjudet meddelande när jag försöker överföra eller ta bort en fil i [!DNL JupyterLab]?

Om webbläsaren är aktiverad med reklamblockerande program som [!DNL Ghostery] eller [!DNL AdBlock] Dessutom måste domänen &quot;\*.adobe.net&quot; vara tillåten i varje annonsblockerande programvara för [!DNL JupyterLab] att fungera normalt. Det beror på att [!DNL JupyterLab] virtuella datorer körs på en annan domän än [!DNL Experience Platform] domän.

## Varför göra vissa delar av [!DNL Jupyter Notebook] ser uttråkad ut eller återges den inte som kod?

Detta kan inträffa om cellen i fråga oavsiktligt ändras från &quot;Kod&quot; till &quot;Markering&quot;. När en kodcell är i fokus trycker du på tangentkombinationen **ESC+M** ändrar celltypen till Markering. En cells typ kan ändras med listrutemätaren högst upp i anteckningsboken för de markerade cellerna. Om du vill ändra en celltyp till kod börjar du med att markera den cell som du vill ändra. Klicka sedan på listrutan som anger cellens aktuella typ och välj sedan &quot;Kod&quot;.

![](./images/faq/code_type.png)

## Hur installerar jag [!DNL Python] bibliotek?

The [!DNL Python] kernel är förinstallerad med många vanliga maskininlärningsbibliotek. Du kan dock installera ytterligare anpassade bibliotek genom att köra följande kommando i en kodcell:

```shell
!pip install {LIBRARY_NAME}
```

En fullständig lista över förinstallerade [!DNL Python] bibliotek, se [Bilaga i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Kan jag installera egna PySpark-bibliotek?

Tyvärr kan du inte installera fler bibliotek för PySpark-kärnan. Du kan dock kontakta kundtjänstrepresentanten på Adobe om du vill ha anpassade PySpark-bibliotek installerade.

En lista över förinstallerade PySpark-bibliotek finns i [Bilaga i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Går det att konfigurera [!DNL Spark] klusterresurser för [!DNL JupyterLab] [!DNL Spark] eller PySpark-kärna?

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

Mer information om [!DNL Spark] klusterresurskonfiguration, inklusive en fullständig lista över konfigurerbara egenskaper, finns i [Användarhandbok för JupyterLab](./jupyterlab/overview.md#kernels).

## Varför får jag ett fel när jag försöker köra vissa uppgifter för större datamängder?

Om du får ett felmeddelande av en anledning som `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Detta innebär vanligtvis att minnet håller på att ta slut för drivrutinen eller en exekvering. Se JupyterLab-anteckningsböcker [dataåtkomst](./jupyterlab/access-notebook-data.md) dokumentation för mer information om databegränsningar och hur du kör uppgifter på stora datamängder. Vanligtvis kan det här felet lösas genom att ändra `mode` från `interactive` till `batch`.

När du skriver stora Spark-/PySpark-datauppsättningar kan du dessutom cachelagra dina data (`df.cache()`) innan skrivkoden körs kan prestandan förbättras avsevärt.

<!-- remove this paragraph at a later date once the sdk is updated -->

Om du får problem med att läsa data och använder omformningar på data kan du försöka med att cachelagra data före omformningarna. Cachelagring av data förhindrar flera läsningar i nätverket. Börja med att läsa data. Nästa, cache (`df.cache()`) data. Till sist kan du göra dina omformningar.

## Varför tar mina bärbara Spark/PySpark-datorer så lång tid att läsa och skriva data?

Om du utför dataomvandlingar, till exempel använder `fit()`kan omformningarna köras flera gånger. Om du vill öka prestandan cachelagrar du data med `df.cache()` innan du utför `fit()`. Detta garanterar att omvandlingarna endast utförs en gång och förhindrar flera läsningar i nätverket.

**Rekommenderad beställning:** Börja med att läsa data. Utför sedan omformningar följt av cachelagring (`df.cache()`) data. Till sist utför du en `fit()`.

## Varför fungerar inte mina Spark/PySpark-bärbara datorer?

Om du får något av följande fel:

- Jobbet avbröts på grund av ett scenfel ... Det går bara att zippa RDD-enheter med samma antal element i varje partition.
- Fjärransluten RPC-klient har kopplats från och andra minnesfel.
- Dåliga prestanda vid läsning och skrivning av datauppsättningar.

Kontrollera att du cachelagrar data (`df.cache()`) innan du skriver data. När kod körs i anteckningsböcker, använda `df.cache()` före en åtgärd som `fit()` kan förbättra prestanda för bärbara datorer avsevärt. Använda `df.cache()` innan du skriver en datauppsättning ser du till att omformningarna bara utförs en gång i stället för flera gånger.

## [!DNL Docker Hub] begränsa begränsningar i arbetsytan för datavetenskap

Från och med den 20 november 2020 trädde avgiftsgränserna för anonym och fri autentiserad användning av Docker Hub i kraft. Anonym och kostnadsfri [!DNL Docker Hub] -användare är begränsade till 100 begäranden om hämtning av bilder var sjätte timme. Om du påverkas av dessa ändringar får du det här felmeddelandet: `ERROR: toomanyrequests: Too Many Requests.` eller `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

För närvarande påverkar den här gränsen bara din organisation om du försöker skapa 100 bärbara datorer till Recept inom en sextimmarsperiod eller om du använder Spark-baserade bärbara datorer inom arbetsytan Datavetenskap som ofta skalas upp och ned. Detta är dock osannolikt eftersom klustret fortfarande är aktivt i två timmar innan det går ut. Detta minskar antalet pulls som krävs när klustret är aktivt. Om du får något av ovanstående fel måste du vänta tills [!DNL Docker] gränsen har återställts.

Mer information om [!DNL Docker Hub] hastighetsbegränsningar, gå till [DockerHub-dokumentation](https://www.docker.com/increase-rate-limits). En lösning för detta håller på att bearbetas och förväntas bli klar i en senare version.
