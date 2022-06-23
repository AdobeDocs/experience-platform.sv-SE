---
title: Adobe Experience Platform Versionsinformation juni 2022
description: Versionsinformation juni 2022 för Adobe Experience Platform.
source-git-commit: 492a05b24ec905de926d861f607a6e5d294d46e0
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 22 juni 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations är nu smartare och snabbare. Nya valideringskontroller minskar avsevärt de vanligaste mappningsfelen och minskar därmed tiden till värde. |

{style=&quot;table-layout:auto&quot;}

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att ge insikter från era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar. Ett sätt som Data Science Workspace kan uppnå detta är genom JupyterLab. JupyterLab är ett webbaserat användargränssnitt för <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> och är nära integrerat i Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med Jupyters bärbara datorer, kod och data.

| Funktion | Beskrivning |
| --- | --- |
| JupyterLab Launcher | JupyterLab Launcher innehåller nu startsidor för bärbara Spark 3.2-datorer. Bärbara Spark 2.4-startdatorer ersätts nu av bärbara Spark 3.2-datorer och kommer att ingå i den här versionen. |
| Spark 3.2 | Nya recept från Scala (Spark) och PySpark använder nu Spark 3.2 |
| Kernlar | Scala (Spark) bärbara datorer har nu skapats via Scala-kernel. PySpark-anteckningsböcker skrivs nu via Python Kernel. Spark- och PySpark-kärnan är föråldrad och inställd på att tas bort i en senare version. |
| Recept | Nya PySpark- och Spark-recept följer nu Docker-arbetsflödet som liknar Python- och R-recept. |

{style=&quot;table-layout:auto&quot;}

Mer allmän information om arbetsytan Datavetenskap finns i [översiktlig dokumentation](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| (Beta) Destination SDK support för [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) filbaserade mål och [konfigurerbara filnamn](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | Nu kan du använda Destinationen SDK för att skapa Google Cloud-lagringsmål och definiera egna filnamn för exporterade filer, via filnamnsmakron. <br><br> Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras. |

{style=&quot;table-layout:auto&quot;}

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [(Beta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | The [!DNL Google Ad Manager 360] anslutning aktiverar batchöverföring för [!DNL publisher provided identifiers] (PPID) till [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage] <br><br>Den här destinationen finns för närvarande i betaversionen och är endast tillgänglig för ett begränsat antal kunder. Om du vill begära åtkomst till [!DNL Google Ad Manager 360] kontakta din Adobe-representant och uppge [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Aktivera profiler för riktade medieundersökningar och insamling av feedback för att bättre förstå kundernas behov och förväntningar. |

{style=&quot;table-layout:auto&quot;}

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ad hoc-schemamärkning | Hantera åtkomsten till känsliga data genom att lägga till etiketter i datafält med ad hoc-scheman som genereras automatiskt via Query Service CTAS-frågor. Du kan begränsa användningen av vissa fält, eller datauppsättningar, i ad hoc-scheman för att styra åtkomsten till både känsliga personuppgifter och personligt identifierbar information. Genom att använda den attributbaserade åtkomstkontrollfunktionen kan du etikettera ad hoc-schemafält via plattformens användargränssnitt. |
| `FLATTEN` inställning | När du ansluter till en databas via BI-verktyg från tredje part `FLATTEN` När du anger förenklas kapslade datastrukturer till separata kolumner där attributnamnet blir det kolumnnamn som innehåller radvärdena. Detta förbättrar användbarheten för ad hoc-scheman och minskar den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data i BI-verktyg som inte stöder kapslade datastrukturer. |

{style=&quot;table-layout:auto&quot;}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Betaversion av [!DNL Mixpanel] källa | Nu kan du använda [!DNL Mixpanel] källa att importera analysdata från [!DNL Mixpanel] konto till Experience Platform. Se [[!DNL Mixpanel] källdokumentation](../../sources/connectors/analytics/mixpanel.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om källor finns i [källöversikt](../../sources/home.md).
