---
keywords: Experience Platform;felsökning;Data Science Workspace;populära ämnen
solution: Experience Platform
title: Felsökningsguide för arbetsytan Data Science
topic: Troubleshooting
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 10ccccf72ff7a2fd726066332b9771dff1929af6
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# [!DNL Data Science Workspace] felsökningsguide

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Data Science Workspace]. Mer information och felsökning om [!DNL Platform] API:er i allmänhet finns i [felsökningsguiden för Adobe Experience Platform API](../landing/troubleshooting.md).

## [!DNL JupyterLab] miljön läses inte in i  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Problemet har åtgärdats men kan fortfarande finnas i webbläsaren Google Chrome 80.x. Kontrollera att webbläsaren Chrome är uppdaterad.

Med webbläsarversionen 80.x för [!DNL Google Chrome] blockeras alla cookies från tredje part som standard. Den här principen kan förhindra att [!DNL JupyterLab] läses in i Adobe Experience Platform.

Så här åtgärdar du problemet:

Navigera till det övre högra hörnet i din [!DNL Chrome]-webbläsare och välj **Inställningar** (du kan även kopiera och klistra in &quot;chrome://settings/&quot; i adressfältet). Bläddra sedan längst ned på sidan och klicka på listrutan **Avancerat**.

![avancerat krom](./images/faq/chrome-advanced.png)

Avsnittet **Sekretess och säkerhet** visas. Klicka sedan på **Platsinställningar** följt av **Cookies och platsdata**.

![avancerat krom](./images/faq/privacy-security.png)

![avancerat krom](./images/faq/cookies.png)

Slutligen växlar du Blockera cookies från tredje part till AV.

![avancerat krom](./images/faq/toggle-off.png)

>[!NOTE]
>
>Du kan även inaktivera cookies från tredje part och lägga till [*.]ds.adobe.net till tillåtelselista.

Gå till&quot;chrome://flags/&quot; i adressfältet. Sök efter och inaktivera flaggan *&quot;SameSite som standard-cookies&quot;* genom att använda listrutan till höger.

![inaktivera samma webbplatsflagga](./images/faq/samesite-flag.png)

Efter steg 2 uppmanas du att starta om webbläsaren. När du har startat om bör [!DNL Jupyterlab] vara tillgängligt.

## Varför kan jag inte komma åt [!DNL JupyterLab] i Safari?

Safari inaktiverar cookies från tredje part som standard i Safari &lt; 12. Eftersom instansen av den virtuella datorn [!DNL Jupyter] finns i en annan domän än den överordnade bildrutan, kräver Adobe Experience Platform för närvarande att cookies från tredje part aktiveras. Aktivera cookies från tredje part eller växla till en annan webbläsare, till exempel [!DNL Google Chrome].

För Safari 12 måste du växla din användaragent till [!DNL Chrome] eller [!DNL Firefox]. Om du vill byta användaragent startar du med att öppna menyn *Safari* och väljer **Inställningar**. Inställningsfönstret visas.

![Safari-inställningar](./images/faq/preferences.png)

Välj **Avancerat** i inställningsfönstret i Safari. Markera sedan *Visa menyn Framkalla i menyraden*. Du kan stänga inställningsfönstret när det här steget är klart.

![Safari avancerat](./images/faq/advanced.png)

Välj sedan menyn **Framkalla** i det övre navigeringsfältet. I listrutan **Utveckla** håller du muspekaren över **Användaragent**. Du kan välja den **[!DNL Chrome]** eller **[!DNL Firefox]** användaragentsträng som du vill använda.

![Menyn Framkalla](./images/faq/user-agent.png)

## Varför visas ett 403-förbjudet meddelande när jag försöker överföra eller ta bort en fil i [!DNL JupyterLab]?

Om din webbläsare är aktiverad med annonseringsblockerande program som [!DNL Ghostery] eller [!DNL AdBlock] Plus måste domänen &quot;\*.adobe.net&quot; tillåtas i alla annonseringsblockerande program för att [!DNL JupyterLab] ska fungera normalt. Detta beror på att virtuella datorer [!DNL JupyterLab] körs på en annan domän än domänen [!DNL Experience Platform].

## Varför ser vissa delar av min [!DNL Jupyter Notebook] förvrängda ut eller återges inte som kod?

Detta kan inträffa om cellen i fråga oavsiktligt ändras från &quot;Kod&quot; till &quot;Markering&quot;. När en kodcell är i fokus ändras celltypen till Markdown om du trycker på tangentkombinationen **ESC+M**. En cells typ kan ändras med listrutemätaren högst upp i anteckningsboken för de markerade cellerna. Om du vill ändra en celltyp till kod börjar du med att markera den cell som du vill ändra. Klicka sedan på listrutan som anger cellens aktuella typ och välj sedan &quot;Kod&quot;.

![](./images/faq/code_type.png)

## Hur installerar jag anpassade [!DNL Python]-bibliotek?

Kerneln [!DNL Python] är förinstallerad med många vanliga maskininlärningsbibliotek. Du kan dock installera ytterligare anpassade bibliotek genom att köra följande kommando i en kodcell:

```shell
!pip install {LIBRARY_NAME}
```

En fullständig lista över förinstallerade [!DNL Python]-bibliotek finns i avsnittet [appendix i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Kan jag installera egna PySpark-bibliotek?

Tyvärr kan du inte installera fler bibliotek för PySpark-kärnan. Du kan dock kontakta kundtjänstrepresentanten på Adobe om du vill ha anpassade PySpark-bibliotek installerade.

En lista över förinstallerade PySpark-bibliotek finns i [bilagan i användarhandboken för JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Går det att konfigurera [!DNL Spark]-klusterresurser för [!DNL JupyterLab] [!DNL Spark]- eller PySpark-kärna?

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

Mer information om klusterresurskonfigurationen [!DNL Spark], inklusive en fullständig lista över konfigurerbara egenskaper, finns i [användarhandboken för JupyterLab](./jupyterlab/overview.md#kernels).

## Varför får jag ett fel när jag försöker köra vissa uppgifter för större datamängder?

Om du får ett fel av en anledning som `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` innebär det vanligtvis att drivrutinen eller en körare har slut på minne. Mer information om databegränsningar och hur du kör uppgifter på stora datauppsättningar finns i dokumentationen för JupyterLab-anteckningsböcker [dataåtkomst](./jupyterlab/access-notebook-data.md). Vanligtvis kan det här felet lösas genom att ändra `mode` från `interactive` till `batch`.

## [!DNL Docker Hub] begränsa begränsningar i arbetsytan för datavetenskap

Från och med den 20 november 2020 trädde avgiftsgränserna för anonym och fri autentiserad användning av Docker Hub i kraft. Anonyma och kostnadsfria [!DNL Docker Hub]-användare är begränsade till 100 hämtningsbegäranden för behållarbilder var sjätte timme. Om du påverkas av dessa ändringar får du det här felmeddelandet: `ERROR: toomanyrequests: Too Many Requests.` eller `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

För närvarande påverkar den här gränsen bara din organisation om du försöker skapa 100 bärbara datorer till Recept inom en sextimmarsperiod eller om du använder Spark-baserade bärbara datorer inom arbetsytan Datavetenskap som ofta skalas upp och ned. Detta är dock osannolikt eftersom klustret fortfarande är aktivt i två timmar innan det går ut. Detta minskar antalet pulls som krävs när klustret är aktivt. Om du får något av ovanstående fel måste du vänta tills din [!DNL Docker]-gräns har återställts.

Mer information om hastighetsbegränsningar för [!DNL Docker Hub] finns i [DockerHub-dokumentationen](https://www.docker.com/increase-rate-limits). En lösning för detta håller på att bearbetas och förväntas bli klar i en senare version.