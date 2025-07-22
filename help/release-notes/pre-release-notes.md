---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d30778ef3152b779157206ce0d416c0e61ba98c3
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 21%

---

# Information om förhandsversionen av Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet är avsett som en **förhandsgranskning** av versionsinformationen för den aktuella månaden. Utgivningsobjekt kan ändras och kan läggas till eller tas bort i den slutliga versionen.

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 29 juli 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Mål](#destinations)
- [Datainmatning](#ingestion)
- [Frågetjänst](#query-service)
- [Real-Time CDP B2B-utgåva](#b2b)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Uppdaterade mål**

| Mål | Beskrivning |
| --- | --- |
| Konsolidering av Marketo-destinationskort | Marketo V2- och Marketo Engage Person Sync-målkort har konsoliderats till ett enda, enhetligt målkort. Konsolideringen förenklar urvalsprocessen och ger en smidigare upplevelse för Marketo-integreringar. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för målkryptering med DLZ (Data Landing Zone) | Lagt till krypteringsstöd för Data Landing Zone-målet. Nu kan du bifoga RSA-formaterade offentliga nycklar för att lägga till kryptering till dina exporterade filer, vilket ger bättre skydd vid export av känsliga data. |
| Förbättrad datastream-information för kantmål | Förbättrad information om rätt spår för Adobe Target och anpassade Personalization-mål visar nu både fältet Datastream-namn och Datastream-ID, vilket ger tydligare synlighet i associerade datastream-konfigurationer och minskar förvirringen när befintliga dataflöden granskas. **[!UICONTROL Datastream ID]**-väljaren i målkonfigurationsskärmen har uppdaterats till **[!UICONTROL Datastream]** för att användargränssnittet ska bli tydligare. |
| Synlighet för marknadsföringsåtgärder i målval | Marknadsföringsåtgärder visas nu i rätt spår i steget [!UICONTROL Select Destination] när ett dataflöde konfigureras, vilket ger omedelbar synlighet till ändringar av marknadsföringsåtgärder utan att det krävs navigering till visningssidan. Den här förbättringen förbättrar användarupplevelsen genom att göra det enklare att verifiera konfigurationer av marknadsföringsåtgärder under målkonfigurationen. |
| Redigera marknadsföringsåtgärder för destinationer | Nu kan du redigera marknadsföringsåtgärder för befintliga destinationer. |
| Kontonamn och beskrivningar för målanslutningar | Nu kan du lägga till kontonamn och beskrivningar när du ansluter till mål, vilket ger bättre hantering av mål med flera konton. |

**Korrigeringar**

| Problem | Beskrivning |
| --- | --- |
| Rullningsfunktion för kategorier | Ett problem har korrigerats där kategorisidmenyn i målkatalogen och källkatalogen inte rullade korrekt när användaren för musen över, vilket förbättrar navigeringsanvändbarheten för användare som bläddrar i målkategorier. |

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Datainmatning {#ingestion}

Experience Platform har ett omfattande ramverk för datainhämtning som stöder både batchvis och strömmande datainmatning från olika källor.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för övervakning av inmatning av direktuppspelningsprofiler | Realtidsövervakning för inmatning av strömmande profiler är nu tillgängligt, vilket ger transparens i mätvärden för genomströmning, fördröjning och datakvalitet. Detta stöder förebyggande varningar och åtgärdbara insikter som hjälper datatekniker att identifiera kapacitetsöverträdelser och problem med inmatning. |

Mer information finns i [översikten över dataöverföring](../ingestion/home.md).

## Frågetjänst {#query-service}

Adobe Experience Platform Query Service är ett robust SQL-gränssnitt för dataanalys och -utforskning på hela plattformen.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrad sessionshantering | Data Distiller innehåller nu förbättrade funktioner för sessionshantering, vilket ger bättre kontroll över användarsessioner och förbättrad prestandaövervakning i utvecklings- och produktionsmiljöer. |
| Stöd för teckenbegränsningar för lösenord som inte förfaller | Data Distiller har nu stöd för icke-utgångsdatum med specifika teckenbegränsningar. För lösenord krävs minst en siffra, en gemen, en versal och ett specialtecken, men dollartecknet ($) stöds inte. `!, @, #, ^, or &` rekommenderas som specialtecken. |
| Bättre enhetlighet i olika miljöer | Data Distiller prestanda är nu konsekvent mellan utvecklings- och produktionssandlådor, med liknande backend-resurser tillgängliga i båda miljöerna. Utnyttjade beräkningstimmar kan variera beroende på datavolym och tillgängliga backend-beräkningsresurser vid bearbetningstid. |

Mer information finns i [Översikt över frågetjänsten](../query-service/home.md).

## Real-Time CDP B2B-utgåva {#b2b}

Real-Time CDP B2B edition har omfattande funktioner för hantering av kunddata inom B2B, vilket gör det möjligt för organisationer att skapa enhetliga kundprofiler, skapa sofistikerade B2B-målgrupper och aktivera data över olika marknadsföringskanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppgradering av B2B-arkitektur | Experience Platform uppgraderar till en ny B2B-arkitektur som innebär betydande förbättringar för målgrupper med flera enheter med B2B-attribut. Den här uppgraderingen konsoliderar stöd för sammanslagningsprinciper, ökar målgruppernas noggrannhet och förbättrar möjligheten till enhetsupplösning. |
| Sammanfoga principkonsolidering för målgrupper med flera enheter | Flera målgrupper med B2B-attribut har nu endast stöd för en enda sammanslagningsprincip - standardprincipen för sammanslagning - i stället för att ha stöd för flera sammanslagningsprinciper. Den här ändringen ger en enhetlig målgruppskomposition och förenklar hanteringen av sammanfogningslogik. |
| Uppdateringar av begränsningar för målgrupper | Kontomålgrupper har inte längre de tidigare begränsningarna i ett 30-dagars uppslagsfönster för Experience Events, anpassade entitetsbegränsningar eller begränsningar för att använda `inSegment`-händelser. Dessa uppdateringar ger större flexibilitet när det gäller att skapa komplexa B2B-målgruppsdefinitioner. |
| Bättre antal målgrupper för B2B-enheter | Beräkningar av målgruppsstorlek för målgrupper med B2B-enheter som konton och säljprojekt är nu exakta, baserat på segmenteringsresultat i realtid. Denna förbättring ger exaktare och tillförlitligare uppskattningar för målgrupper som involverar komplexa B2B-relationer. |
| Ögonblicksbilder av konton för målgruppsmedlemskap | Information om målgruppsmedlemskap ingår nu för kontoenheter vid export av ögonblicksbilder, vilket ger åtkomst till målgruppsstatus på kontonivå, tidsstämplar och medlemsindikatorer. Detta ger en funktionsparitet mellan segmenteringsmodellerna Profil (Person) och Konto. |
| Verktygsändringar i sandlådan för målgrupper med flera enheter | Import av målgrupper med flera enheter med B2B-enheter och Experience Events som exporterats före migrering stöds inte längre. Dessa målgrupper kommer inte att kunna validera importen och kan inte konverteras automatiskt till den nya arkitekturen. Publiker måste exporteras igen efter migrering innan de kan importeras till målsandlådor. |
| Avvikelser i enhets-API:t för B2B | Målgruppsgenerering via API för B2B-enheter (konto, säljprojekt, konto-personrelation, relation mellan säljprojekt och person, kampanj, kampanjmedlem, marknadsföringslista och marknadsföringslistmedlem) är nu föråldrat. API-söknings- och borttagningsåtgärder för profilåtkomst för dessa B2B-enheter är också föråldrade. |
| Uppdateringar av identitetsnamnrymden för entitetsupplösning | Konto- och säljprojektsenheter använder nu tidsprioritetsbaserad sammanslagning med specifika identitetsnamnutrymmen (`b2b_account` för konto, `b2b_opportunity` för säljprojekt). Alla andra enheter är enhetliga med primära identitetsöverlappningar som sammanfogas med tidsprioritetsbaserad sammanslagning. |

Mer information finns i [Real-Time CDP B2B edition - översikt](../rtcdp/b2b-overview.md).

## Sandlådor {#sandboxes}

Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ändringar av målgruppsimporter för flera enheter | Sandlådeverktygen har uppdaterats för att stödja den nya uppgraderingen av B2B-arkitekturen. Målgrupper med flera enheter som innehåller B2B-enheter och Experience Events måste exporteras på nytt efter uppgraderingen av arkitekturen innan de kan importeras till målsandlådor via sandlådeverktyg. Det går inte att validera importen av föruppgraderingsversioner. |

Mer information om sandlådor finns i [översikten över sandlådor](../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| API för extern publik | Du kan använda det externa målgrupps-API:t för att programmässigt importera externt genererade målgrupper till Adobe Experience Platform. |

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya källor**

| Source | Beskrivning |
| --- | --- |
| Stöd för [!DNL Didomi] (direktuppspelande SDK) | Med källkopplingen [!DNL Didomi] kan du importera data för samtyckeshantering från plattformen för [!DNL Didomi], vilket stöder efterlevnad av sekretessbestämmelser och medgivandebaserade marknadsföringsstrategier. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för inhämtning av ändringsdata i utvalda källor | Nu kan du skapa dataflöden som möjliggör registrering av ändringsdata för inkrementellt intag med hjälp av källanslutningar. Med den här funktionen kan kunderna ta med sig datatypen change för inkrementellt intag, vilket förbättrar dataaktualiteten och minskar belastningen på processerna. |
| Stöd för mjuk borttagning av poster i [!DNL Salesforce] | Källan [!DNL Salesforce] har nu stöd för att ta med mjuka borttagna poster via en valfri `includeDeletedObjects`-parameter. Om värdet är true kan kunder ta med mjuka borttagna poster i sina [!DNL Salesforce]-frågor och hämta dessa poster till Experience Platform. |

Mer information finns i [översikten över källor](../sources/home.md).
