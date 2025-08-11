---
title: Versionsinformation om Adobe Experience Platform juli 2025
description: Versionsinformationen för Adobe Experience Platform från juli 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: ht
source-wordcount: '1554'
ht-degree: 100%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 29 juli 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Kapacitet](#capacity)
- [Mål](#destinations)
- [Datainhämtning](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)


## Kapacitet {#capacity}

>[!AVAILABILITY]
>
>Den här funktionen kan användas beroende på region. För användare i Nord- och Sydamerika är den tillgänglig från och med den 11 augusti. För användare i Europa är den tillgänglig från och med den 25 augusti. För användare i Asien kommer den att vara tillgänglig från den 8 september.

Kapaciteten ger en heltäckande bild av organisationens [skyddsräcken](../../rtcdp/guardrails/overview.md) och ger rekommendationer om hur du kan lösa potentiella kapacitetsöverträdelser genom att tilldela kapacitet på sandlådenivå. I den här versionen kan du visa din kapacitet för både strömningsinmatning och strömningssegmentering.

Mer information finns i [kapacitetsöversikten](../../landing/license-usage-and-guardrails/capacity.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Uppdaterade mål**

| Mål | Beskrivning |
| --- | --- |
| Begränsad tillgänglighet för anslutningen [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Efter att ha varit tillgänglig för alla kunder i juni återgår nu denna Adobe-integrering till begränsad tillgänglighet. För närvarande är åtkomsten till den här destinationen begränsad till kunder som redan är aktiverade, medan Adobe och Google arbetar med att lösa implementeringsproblem. Om du är intresserad av att använda den här integreringen när den bredare utrullningen återupptas ber vi dig kontakta Adobe och meddela detta. |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) intern uppgradering | Från och med 31 juli 2025 kan du se två [!DNL The Trade Desk]-kort sida vid sida i målkatalogen. Det här beror på en intern uppgradering av måltjänsten. <br><br>Den befintliga målanslutningen [!DNL The Trade Desk] har bytt namn till **[!UICONTROL (Deprecated) The Trade Desk]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL The Trade Desk]**. Använd den nya anslutningen **[!UICONTROL The Trade Desk]** i katalogen för nya aktiveringsdataflöden. <br><br>Om du har aktiva dataflöden till målet **[!UICONTROL (Deprecated) The Trade Desk]** uppdateras de automatiskt. Du behöver därför inte göra något. <br><br> Om du skapar dataflöden via [Flow Service API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:<ul><li>Flödesspecifikation-id: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>Anslutningsspecifikation-id: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Kontonamn och beskrivningar för målanslutningar | Nu kan du [lägga till kontonamn och beskrivningar](/help/destinations/ui/connect-destination.md) vid anslutning till mål, vilket ger bättre hantering av mål med flera konton. |
| Förbättrad dataströmningsinformation för kantmål | Högerspaltsinformationen för [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) - och [anpassade Personalization](/help/destinations/catalog/personalization/custom-personalization.md)-mål har förbättrats så att dataströmningsnamnet visas, vilket ger tydligare synlighet i associerade dataströmningskonfigurationer och bidrar till att minska förvirringen när befintliga dataflöden granskas. **[!UICONTROL Datastream ID]**-väljaren i målkonfigurationsskärmen har uppdaterats till **[!UICONTROL Datastream]** för att användargränssnittet ska bli tydligare. |
| Synlighet för marknadsföringsåtgärder i målval | Marknadsföringsåtgärder visas nu i den högra listen på fliken **[[!UICONTROL Browse]](/help/destinations/ui/destinations-workspace.md#browse)** på arbetsytan Mål och på sidan **[[!UICONTROL Dataflow runs]](/help/dataflows/ui/monitor-destinations.md)**, vilket ger omedelbar insyn i ändringar av marknadsföringsåtgärder utan att du behöver navigera till visningssidan. Den här förbättringen förbättrar användarupplevelsen genom att göra det enklare att verifiera konfigurationer av marknadsföringsåtgärder under målkonfigurationen. |
| [!BADGE Begränsad beta]{type=Informative} Redigera marknadsföringsåtgärder för mål | Nu kan du [redigera marknadsföringsåtgärderna](/help/destinations/ui/edit-activation.md#edit-marketing-actions) för befintliga destinationer. Den här funktionen är för närvarande i begränsad betaversion. Kontakta din Adobe-representant om du vill få åtkomst. |
| [!BADGE Begränsad beta]{type=Informative} Redigera mål | Du kan nu [redigera målkonfigurationen](/help/destinations/ui/edit-destination.md) när den har skapats. Den här funktionen är för närvarande i begränsad betaversion. Kontakta din Adobe-representant om du vill få åtkomst. |

**Korrigeringar**

| Problem | Beskrivning |
| --- | --- |
| Skrollningsfunktion för kategorier | Problemet med att menyn för kategorisidor i destinationskatalogen och källkatalogen inte rullade korrekt när användaren förde musen över den har åtgärdats, vilket förbättrar navigeringen för användare som bläddrar i destinationskategorier. |

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Datainhämtning {#ingestion}

Experience Platform har ett omfattande ramverk för datainhämtning som stöder både grupp- och strömmande datainhämtning från olika källor.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för övervakning av inmatning av strömningsprofiler | Realtidsövervakning för inmatning av strömmande profiler är nu tillgänglig, vilket ger transparens i mätvärden för genomströmning, fördröjning och datakvalitet. Detta stöder förebyggande varningar och åtgärdbara insikter som hjälper datatekniker att identifiera kapacitetsöverträdelser och problem med inmatning. Läs guiden [Övervaka inmatning av strömmande profiler](../../dataflows/ui/monitor-streaming-profile.md) för mer information. |

Mer information finns i [översikten över datainhämtning](../../ingestion/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B edition har omfattande funktioner för hantering av B2B-kunddata, vilket gör det möjligt för organisationer att skapa enhetliga kundprofiler, skapa sofistikerade B2B-målgrupper och aktivera data över olika marknadsföringskanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppgradering av B2B-arkitektur | Experience Platform uppgraderar till en ny B2B-arkitektur som innebär betydande förbättringar för målgrupper med flera enheter med B2B-attribut. Den här uppgraderingen konsoliderar stöd för sammanfogningsprinciper, ökar målgruppsberäkningens noggrannhet och förbättrar förmågan till enhetsupplösning. Läs [Översikt över uppgraderingen av Real-Time CDP B2B Edition-arkitekturen](../../rtcdp/b2b-architecture-upgrade.md) för en utförlig beskrivning av ändringarna. |
| Konsolidering av sammanfogningspolicy för målgrupper med flera enheter | Målgrupper med flera B2B-attribut har nu endast stöd för en enda sammanfogningspolicy – standardpolicyn för sammanfogning – i stället för att ha stöd för flera sammanfogningspolicyer. Den här ändringen ger en enhetlig målgruppssammansättning och förenklar hanteringen av sammanfogningslogik. Mer information finns i [översikten över sammanfogningspolicyer](../../profile/merge-policies/overview.md). |
| Förbättrad målgruppsberäkning för B2B-enheter | Beräkningarna av målgruppsstorlek för målgrupper med B2B-enheter såsom konton och möjligheter är nu exakta, baserat på segmenteringsresultat i realtid. Denna förbättring ger exaktare och tillförlitligare beräkningar för målgrupper med komplexa B2B-relationer. |
| Ögonblicksbilder av konton för målgruppsmedlemskap | Information om målgruppsmedlemskap ingår nu för kontoenheter vid export av ögonblicksbilder, vilket ger åtkomst till målgruppsstatus på kontonivå, tidsstämplar och medlemsindikatorer. Detta ger en funktionsparitet mellan segmenteringsmodellerna Profil (Person) och Konto. |
| Verktygsändringar i sandlådan för målgrupper med flera enheter | Import av målgrupper med flera enheter med B2B-enheter och Experience Events som exporterats före migrering stöds inte längre. Dessa målgrupper kommer inte att kunna validera importen och kan inte konverteras automatiskt till den nya arkitekturen. Målgrupper måste exporteras igen efter migrering innan de kan importeras till målsandlådor. Mer information finns i [guiden om objekt som stöds för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Avvikelser i enhets-API:et för B2B | [!DNL Profile Access]API-sökningsåtgärder för B2B-entiteter (konto/personrelation, säljprojekt, säljprojektsrelation, kampanj, kampanjmedlem, marknadsföringslista och marknadsföringslistmedlemmar) är nu föråldrade. Även [!DNL Profile Access] API-borttagningsåtgärder för B2B-enheter (konto, konto/personrelation, säljprojekt, säljprojektsrelation, kampanj, kampanjmedlem, marknadsföringslista och marknadsföringslistmedlemmar) är föråldrade. Mer information finns i [guiden för slutpunkts-API:er](../../profile/api/entities.md). |
| Uppdateringar av ID-namnutrymme för entitetsupplösning | Konto- och säljprojektsenheter använder nu tidsprioritetsbaserad sammanfogning med specifika ID-namnutrymmen (`b2b_account` för konto, `b2b_opportunity` för säljprojekt). Alla andra enheter är enhetliga med primära identitetsöverlappningar som sammanfogas med tidsprioritetsbaserad sammanfogning. Mer information om entitetsupplösning finns i [guiden för API-slutpunkter](../../profile/api/entities.md). |

Mer information finns i [Real-Time CDP B2B Edition – översikt](../../rtcdp/b2b-overview.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ändringar av målgruppsimporter för flera enheter | Sandlådeverktygen har uppdaterats för att stödja den nya uppgraderingen av B2B-arkitekturen. Målgrupper med flera enheter som innehåller B2B-enheter och Experience Events måste exporteras på nytt efter uppgraderingen av arkitekturen innan de kan importeras till målsandlådor med sandlådeverktyg. Det går inte att validera importen av versioner från tiden före uppgraderingen. Mer information finns i [guiden om objekt som stöds för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API för extern målgrupp | Du kan använda det externa målgrupps-API:et för att importera externt genererade målgrupper programmatiskt till Adobe Experience Platform. Mer information finns i [guiden för externa målgruppsslutpunkter](../../segmentation/api/external-audiences.md). |

Mer information om segmentering finns i [översikten över segmenteringstjänsten](../../segmentation/home.md)

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya källor**

| Källa | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative}-stöd för [!DNL Didomi] (strömning av SDK) | Använd [!DNL Didomi]-källan för att inhämta data för samtycke och preferenshantering från [!DNL Didomi], vilket stöder efterlevnad av sekretessbestämmelser och samtyckesbaserade marknadsföringsstrategier. Läs [[!DNL Didomi] källöversikten](../../sources/connectors/consent-and-preferences/didomi.md) för information om hur du skaffar konfigurationen. Anvisningar om hur du skapar en källanslutning finns i [[!DNL Didomi] källanslutningsguiden](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för registrering av ändringsdata i utvalda källor med API:et [!DNL Flow Service] | Nu kan du skapa dataflöden som möjliggör registrering av ändringsdata för inkrementell inmatning med hjälp av källanslutningar. Med den här funktionen kan kunderna mata in ändringsdatatypen inkrementellt, vilket ökar datans aktualitet och minskar bearbetningsbelastningen. Mer information finns i dokumentationen om [hur du använder datainhämtning för källor](../../sources/tutorials/api/change-data-capture.md) |
| Stöd för mjuk borttagning av poster i [!DNL Salesforce] | Källan [!DNL Salesforce] har nu stöd för att ta med mjuka borttagna poster via en valfri `includeDeletedObjects`-parameter. Om värdet är sant kan kunderna ta med mjuka borttagna poster i sina [!DNL Salesforce]-frågor och hämta dessa poster till Experience Platform. Läs [[!DNL Salesforce] källdokumentationen](../../sources/connectors/crm/salesforce.md) för mer information. |

Mer information finns i [översikten över källor](../../sources/home.md).
