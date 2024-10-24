---
title: Namnområdesprioritet
description: Läs om namnområdesprioritet i identitetstjänsten.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: e8e8914c41d7a083395b0bf53aaac8021fcf9e9a
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 1%

---

# Namnområdesprioritet

>[!AVAILABILITY]
>
>Regler för länkning av identitetsdiagram är för närvarande begränsade. Kontakta ditt Adobe-kontoteam om du vill ha information om hur du kommer åt funktionen i utvecklingssandlådor.

Varje kundimplementering är unik och skräddarsydd för att uppfylla en viss organisations mål, och som sådan varierar vikten av en viss namnrymd från kund till kund. Exempel från verkligheten:

* Å ena sidan kan du anse att namnutrymmet E-post representerar en personenhet och därmed är unikt per person. En annan kund kan å andra sidan betrakta e-postnamnutrymmet som en otillförlitlig identifierare och kan därför tillåta att ett enskilt CRMID kopplas till flera identiteter med e-postnamnutrymmet.
* Du kan samla in onlinebeteende med hjälp av namnutrymmet Inloggnings-ID. Detta inloggnings-ID kan ha en 1:1-relation med CRMID, som sedan lagrar attribut från ett CRM-system och kan betraktas som det viktigaste namnutrymmet. I det här fallet avgör du att CRMID-namnutrymmet är en mer korrekt representation av en person, medan namnutrymmet för inloggnings-ID är det näst viktigaste.

Du måste skapa konfigurationer i identitetstjänsten som återspeglar hur viktiga dina namnutrymmen är, eftersom detta påverkar hur profiler formas och segmenteras.

## Ange dina prioriteringar

Bestämning av namnområdesprioritet baseras på följande faktorer:

### Identitetsdiagramstruktur

Om din organisations strukturerade diagram är i flera lager bör namnområdesprioriteten återspegla detta så att rätt länkar tas bort vid komprimering av diagram.

>[!TIP]
>
>* &quot;Diagramkomprimering&quot; avser scenarier där flera olika profiler oavsiktligt sammanfogas till ett enda identitetsdiagram.
>
>* Ett diagram med flera lager refererar till identitetsdiagram med flera länknivåer. Se bilden nedan för ett exempel på ett diagram med tre lager.

![Ett diagram över diagramlager](../images/namespace-priority/graph-layers.png)

### Namnutrymmets semantiska betydelse

En identitet representerar ett objekt i verkligheten. Det finns tre objekt som visas i identitetsdiagrammet. De är följande:

* Personer (olika enheter, e-post, telefonnummer)
* Maskinvaruenhet
* Webbläsare (cookie)

Personnamnutrymmen är relativt oföränderliga jämfört med maskinvaruenheter (som IDFA, GAID), som är relativt oföränderliga jämfört med webbläsare. I princip är du (människa) alltid en enda enhet som kan ha flera maskinvaruenheter (telefon, bärbar dator, surfplatta osv.) och använda flera webbläsare (Google Chrome, Safari, FireFox osv.)

Ett annat sätt att se på det här ämnet är genom kardinalitet. Hur många identiteter kommer att skapas för en viss person? I de flesta fall har en person ett CRMID, en handfull identifierare för hårdvaruenheter (IDFA/GAID-återställning bör inte ske så ofta) och ännu fler cookies (en person kan navigera på flera enheter, använda inkognitoläge eller återställa cookies när som helst). I allmänhet anger **lägre kardinalitet ett namnutrymme med ett högre värde**.

## Validera inställningarna för namnområdesprioritet

När du har fått en uppfattning om hur du ska prioritera namnutrymmen kan du använda verktyget Diagramsimulering för att testa olika scenarier för komprimering av diagram och se till att dina prioritetskonfigurationer returnerar de förväntade diagramresultaten. Mer information finns i handboken om hur du använder verktyget [Diagramsimulering](./graph-simulation.md).

## Konfigurera namnområdesprioritet

Namnområdesprioriteten kan konfigureras med [!UICONTROL Identity Settings]. I gränssnittet [!UICONTROL Identity Settings] kan du dra och släppa ett namnutrymme för att fastställa dess relativa betydelse.

>[!IMPORTANT]
>
>Du kan inte prioritera namnutrymmen för enheter/cookies framför personnamnutrymmen. Den här begränsningen säkerställer att inga felkonfigurationer görs.

## Användning av namnområdesprioritet

För närvarande påverkar namnområdesprioriteten systembeteendet för kundprofilen i realtid. Bilden nedan visar detta koncept. Mer information finns i guiden om [Adobe Experience Platform och programarkitekturdiagram](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Ett diagram över programomfånget för namnområdesprioritet](../images/namespace-priority/application-scope.png)

### Identitetstjänst: Identitetsoptimeringsalgoritm

För relativt komplexa diagramstrukturer spelar namnområdesprioriteten en viktig roll när det gäller att säkerställa att rätt länkar tas bort när diagramkomprimeringsscenarier inträffar. Mer information finns i [översikten över algoritmen för identitetsoptimering](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Kundprofil i realtid: primär identitetsbestämning för upplevelsehändelser

* För upplevelsehändelser bestäms den primära identiteten av den högsta namnområdesprioriteten när du har konfigurerat identitetsinställningar för en viss sandlåda.
   * Det beror på att upplevelsehändelser är dynamiska till sin natur. En identitetskarta kan innehålla tre eller fler identiteter, och namnområdesprioriteten ser till att det viktigaste namnutrymmet är kopplat till upplevelsehändelsen.
* Därför kommer följande konfigurationer **inte längre att användas av kundprofilen i realtid**:
   * Kryssrutan Primär för dataelementtypen i WebSDK (som översätts till `primary=true` i identityMap). **Obs!**: Identitetsnamnrymd och identitetsvärde kommer att fortsätta användas i profilen. Dessutom måste du fortfarande konfigurera inställningarna för den primära kryssrutan eftersom tjänster utanför kundprofilen i realtid fortsätter att referera till den här konfigurationen.
   * Alla fält som markerats som primär identitet i ett XDM Experience Event Class-schema.
   * Standardinställningar för primär identitet i Adobe Analytics-källkopplingen (ECID eller AAID).
* Å andra sidan bestämmer inte namnområdesprioriteten **den primära identiteten för profilposter**.
   * För profilposter kan du använda arbetsytan för scheman i användargränssnittet för Experience Platform för att definiera dina identitetsfält, inklusive den primära identiteten. Mer information finns i guiden [Definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md).

>[!TIP]
>
>* Namnområdesprioriteten är **en egenskap för ett namnområde**. Det är ett numeriskt värde som tilldelas ett namnutrymme för att ange dess relativa betydelse.
>
>* Primär identitet är den identitet som ett profilfragment lagras mot. Ett profilfragment är en datapost som lagrar information om en viss användare: attribut (som vanligtvis hämtas via CRM-poster) eller händelser (som vanligtvis hämtas från upplevelsehändelser eller onlinedata).

### Exempel på scenario

I det här avsnittet finns ett exempel på hur prioritetskonfigurationen kan påverka dina data.

Anta att följande konfigurationer har skapats för en viss sandlåda:

| Namnutrymme | Real-world application of the namespace | Prioritet |
| --- | --- | --- |
| CRMID | Användare | 1 |
| IDFA | Apple hårdvaruenhet (iPhone, IPad osv.) | 2 |
| GAID | Google hårdvaruenhet (Google Pixel, Pixelbook, etc.) | 3 |
| ECID | Webbläsare (Firefox, Safari, Google Chrome osv.) | 4 |
| STÖD | Webbläsare | 5 |

{style="table-layout:auto"}

Med tanke på de konfigurationer som beskrivs ovan kommer användaråtgärder och fastställande av primär identitet att lösas som sådana:

| Användaråtgärd (Experience-händelse) | Autentiseringstillstånd | Datakälla | Namnutrymmen i händelse | Namnområde för primär identitet |
| --- | --- | --- | --- | --- |
| Visa erbjudandesida för kreditkort | Oautentiserad (anonym) | Web SDK | `{ECID}` | ECID |
| Visa hjälpsidan | Oautentiserad | Mobile SDK | `{ECID, IDFA}` | IDFA |
| Visa saldo för checkkonto | Autentiserad | Web SDK | `{CRMID, ECID}` | CRMID |
| Registrera dig för bostadslån | Autentiserad | Källanslutning för analyser | `{CRMID, ECID, AAID}` | CRMID |
| Överför 1 000 dollar från kontroll till besparingar | Autentiserad | Mobile SDK | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

### Segmenteringstjänst: lagring av metadata för segmentmedlemskap

![Ett diagram över segmentmedlemskapslagring](../images/namespace-priority/segment-membership-storage.png)

För en given sammanfogad profil lagras segmentmedlemskap mot identiteten med den högsta namnområdesprioriteten.

Anta till exempel att det finns två profiler:

* Profil 1 representerar John.
   * Johns profil kvalificerar sig för S1 (segmentmedlemskap 1). S1 kan till exempel referera till ett kundsegment som identifierar som manligt.
   * Johns profil berättigar också till S2 (segmentmedlemskap 2). Detta kan gälla ett segment av kunder vars lojalitetsstatus är guld.
* Profil 2 representerar Jane.
   * Jane&#39;s profile eligibility for S3 (segment membership 3). Detta kan gälla ett segment av kunder som identifieras som kvinnliga.
   * Jane&#39;s profile also eligible for S4 (segment membership 4). Detta kan gälla ett segment av kunder vars lojalitetsstatus är platina.

Om John och Jane delar en enhet överförs ECID (webbläsare) från en person till en annan. Detta påverkar dock inte segmentmedlemskapsinformationen som lagras mot John och Jane.

Om kriterierna för godkännande av segment endast baserades på anonyma händelser som sparats mot ECID, skulle Jane kvalificera sig för det segmentet

## Konsekvenser för andra Experience Platform-tjänster {#implications}

I det här avsnittet beskrivs hur namnområdesprioriteten kan påverka andra Experience Platform-tjänster.

### Hantering av avancerad datalivscykel

Funktioner för borttagning av datahygienpost på följande sätt för en viss identitet:

* Kundprofil i realtid: Tar bort alla profilfragment med angiven identitet som primär identitet. **Den primära identiteten i profilen bestäms nu utifrån namnområdesprioritet.**
* Datasjön: Tar bort alla poster med den angivna identiteten som primär identitet. Till skillnad från kundprofil i realtid baseras den primära identiteten i datasjön på den primära identitet som anges i WebSDK (`primary=true`) eller ett fält som markerats som primär identitet

Mer information finns i [Översikt över avancerad livscykelhantering](../../hygiene/home.md).

### Beräknade attribut

Beräknade attribut använder inte namnområdesprioritet för att beräkna värden. Om du använder beräknade attribut måste du se till att CRMID har angetts som din primära identitet för WebSDK. Mer information finns i användargränssnittshandboken för [beräknade attribut](../../profile/computed-attributes/ui.md).

### Data Lake

Inmatningen av data i sjön fortsätter att följa de primära identitetsinställningarna som konfigurerats för [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) och scheman.

Datasjön kommer inte att fastställa den primära identiteten baserat på namnområdesprioriteten. Adobe Customer Journey Analytics kommer till exempel att fortsätta använda värden i identitetskartan även efter det att namnområdesprioriteten har aktiverats (till exempel när en datauppsättning läggs till i en ny anslutning), eftersom Customer Journey Analytics använder data från datavjön.

### XDM-scheman (Experience Data Model)

Alla scheman som inte är en XDM Experience Event, till exempel enskilda XDM-profiler, fortsätter att respektera alla [fält som du markerar som en identitet](../../xdm/ui/fields/identity.md).

Mer information om XDM-scheman finns i översikten [scheman](../../xdm/home.md).

### Intelligenta tjänster

När du väljer data måste du ange ett namnutrymme, som används för att avgöra vilka händelser som beräknar poäng och vilka händelser som lagrar de beräknade poängen. Du rekommenderas att välja det namnutrymme som representerar en person.

* Om du samlar in webbbeteendedata med WebSDk rekommenderar vi att du väljer CRMID-namnområdet i identitetskartan.
* Om du samlar in webbbeteendedata med Analytics-källkopplingen bör du välja identitetsbeskrivningen (CRMID).

Den här konfigurationen resulterar endast i beräkning av bakgrundsmusik med hjälp av autentiserade händelser.

Mer information finns i dokumenten på [Attribution AI](../../intelligent-services/attribution-ai/overview.md) och [Kund-AI](../../intelligent-services/customer-ai/overview.md).

### Integritetstjänst

[Borttagningsbegäranden](../privacy.md) för Privacy Service fungerar på följande sätt, för en viss identitet:

* Kundprofil i realtid: Tar bort alla profilfragment med angivet identitetsvärde som primär identitet. **Den primära identiteten i profilen bestäms nu utifrån namnområdesprioritet.**
* Datasjön: Tar bort alla poster med den angivna identiteten som primär eller sekundär identitet.

Mer information finns i [Översikt över sekretesstjänsten](../../privacy-service/home.md).

### Adobe Target

Adobe Target kan generera oväntad målinriktning för delade enhetsscenarier.