---
title: Köra och hantera översikt
description: Inspektera, felsök och optimera era era Experience Platform-implementeringar med verktygen Kör och Kör. Få synlighet i schemalagda batchaktiveringar, identifiera konfigurationsproblem och förbättra systemets tillförlitlighet.
hide: true
exl-id: 7f44cdf3-4db1-47f9-bcde-401f6dcfc551
source-git-commit: a36f984e56f37e4769e54eab182a8c54e891e32f
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Köra och hantera översikt

>[!AVAILABILITY]
>
>Funktionerna Kör och Använd finns för närvarande i en begränsad version.

När batchjobb misslyckas eller levererar ofullständiga data måste du snabbt förstå vad som orsakade problemet. Orsaken kan vara problem med datatillgänglighet, felaktig timing, konfigurationsproblem eller begränsningar av systemkapacitet. Utan tydlig synlighet kan du tillbringa timmar med att undersöka flera system innan du hittar svaret.

Med verktygen i [!UICONTROL Run and Operate] kan du:

* **Inspektera dina dataåtgärder**: Få en komplett vy över jobbkörningens status och hälsa i alla dina arbetsflöden.
* **Felsök snabbare**: Få tillgång till detaljerad diagnostikinformation och körningshistorik för att snabbt identifiera rotorsaker och minska den genomsnittliga tiden till lösning.
* **Förebygg problem proaktivt**: Analysera jobbmönster, identifiera konfigurationsproblem innan de orsakar fel och optimera dataåtgärderna.

## Målgrupper {#target-audiences}

[!UICONTROL Run and Operate]-verktygen är utformade för att betjäna flera olika målgrupper i organisationen:

* **Data- och IT-team**: Systemadministratörer och datatekniker som upprätthåller tillförlitliga dataredningar och felsöker tekniska problem.
* **Marknadsföringsåtgärder**: Marknadsföringstekniker som inspekterar dataleveranser till marknadsföringsplattformar och löser aktiveringsproblem.
* **Implementerare**: Användare som validerar implementeringens effektivitet, tillförlitlighet och felsöker tekniska problem.

## Förutsättningar {#prerequisites}

Du behöver behörigheterna **[!UICONTROL View Job Schedules]** och **[!UICONTROL View Profile Management]** [åtkomstkontroll](/help/access-control/home.md#permissions) för att komma åt verktygen Kör och Kör.
Sidan [!UICONTROL Job Schedules] innehåller en översikt över alla schemalagda batchbearbetningsjobb.
Kontakta systemadministratören för att kontrollera att du har rätt behörigheter.

## Komma igång {#getting-started}

Så här kommer du åt verktygen Kör och Använd från Experience Platform-gränssnittet:

1. Logga in på ditt Experience Platform-konto och välj **[!UICONTROL Run and Operate]** i den vänstra navigeringen.
2. Välj det verktyg som passar dina inspektions- eller felsökningsbehov.

   >[!NOTE]
   >
   >För närvarande är de tillgängliga funktionerna [Jobbscheman](job-schedules.md) och [Hälsokontroller](health-checks.md).

![Experience Platform-användargränssnittet visar det vänstra navigeringsfältet Kör och använd.](assets/overview/run-and-operate.png)

## Tillgängliga verktyg {#available-tools}

Följande verktyg hjälper dig att inspektera och optimera dataåtgärderna.

### Jobbscheman {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] är för närvarande bara tillgängligt för följande Real-Time CDP-jobb:
>
> * Intag av batchdata i sjö
> * Inmatning av gruppprofil
> * Grupputleverans
> * Aktivering av batchmål.

Med [Jobbscheman](job-schedules.md) kan du inspektera alla schemalagda batchåtgärder i organisationen, per sandlåda, inklusive inhämtning av data från sjön, profilinmatning, segmentering och målaktivering. Visa jobbkörningsstatus, resultatmått och körningshistorik för att identifiera mönster och diagnostisera konfigurationsproblem som påverkar tillförlitligheten.

![Experience Platform-gränssnittet visar skärmen Jobbscheman.](assets/overview/job-schedules-interface.png)

Jobbscheman innehåller tre undersökningsnivåer:

* **[Inspektera jobbscheman](job-schedules.md)**: Visa alla datauppsättningar och deras schemalagda jobb i en tidslinje för att identifiera mönster och schemaläggningskonflikter i hela pipelinen.
* **[Identifiera antimönster](job-schedules-anti-patterns.md)**: Lär dig att upptäcka och lösa vanliga konfigurationsproblem som schemaöverlappning, kompakt gruppstackning och överdriven gruppering som påverkar prestandan.
* **[Visa jobbinformation](job-schedules-details.md)**: Granska ner i specifika datauppsättningar och enskilda jobbkörningar för att undersöka fel, kontrollera timing och verifiera bearbetade poster.

Ni kan också förstå beroenden mellan olika databehandlingsfaser, vilket hjälper er att säkerställa ett tillförlitligt dataflöde genom hela Experience Platform-arbetsflöden.

### Hälsokontroller {#health-checks}

>[!IMPORTANT]
>
>[!UICONTROL Health checks] är för närvarande tillgänglig som en begränsad version.

Med [Hälsokontroller](health-checks.md) kan du proaktivt identifiera problem med schema- och identitetskonfigurationen innan de påverkar din affärsverksamhet. I nuläget utförs statiska hälsokontroller varje dag i alla dina scheman och identitetsnamnutrymmen, vilket avslöjar att bästa praxis saknas, felkonfigurationer och mönster som leder till fel längre fram i kedjan.

Hälsokontrollerna utvärderar för närvarande fem grundläggande områden:

* **[Verifiering av identitetsfält](health-checks.md#identity-field-validation)**: Verifiera att identitetsfält har rätt längd och mönsterbegränsningar.
* **[Länkningsregler för identitetsdiagram](health-checks.md#identity-graph-linking-rules)**: Bekräfta att länkningsregler har konfigurerats för att förhindra att profiler komprimeras.
* **[Konfiguration av identiteter för både människor och icke-människor](health-checks.md#people-non-people-identity)**: Verifiera korrekt identitetstypanvändning mellan schemaklasser.
* **[Beskrivningar av anpassade identitetsnamnområden](health-checks.md#namespace-missing-description)**: Kontrollera att namnområdesmetadata är fullständiga.
* **[Inaktuella identitetsnamnutrymmen](health-checks.md#deprecated-namespace)**: Identifiera föråldrade namnutrymmen för rensning.

## Nästa steg {#next-steps}

Nu när du förstår syftet med och funktionerna i [!UICONTROL Run and Operate]-verktygen kan du fördjupa din kunskap genom att utforska följande resurser:

* Lär dig hur du använder [hälsokontroller](health-checks.md) för att identifiera problem med schema- och identitetskonfigurationer
* Lär dig hur du [kontrollerar jobbscheman](job-schedules.md) för din batchförbrukning och aktivering
* Lär dig mer om [batchimport](../ingestion/batch-ingestion/overview.md) för att förstå hur data importeras till Experience Platform
* Lär dig hur du [konfigurerar schemalagda aktiveringar](../destinations/ui/activate-batch-profile-destinations.md) för batchmål
* Utforska [dataflödesövervakning](../dataflows/ui/monitor-destinations.md) för mål
