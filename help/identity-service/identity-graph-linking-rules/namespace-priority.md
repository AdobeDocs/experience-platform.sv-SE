---
title: Namnområdesprioritet
description: Läs om namnområdesprioritet i identitetstjänsten.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 048d915d33a19a9d50a4951e165b5ade1b9d9734
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 1%

---

# Namnområdesprioritet {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Namnområdesprioritet"
>abstract="Namnområdesprioriteten avgör hur länkar tas bort från identitetsdiagrammet."

>[!AVAILABILITY]
>
>Regler för länkning av identitetsdiagram är för närvarande begränsade. Kontakta ditt Adobe-kontoteam om du vill ha information om hur du kommer åt funktionen i utvecklingssandlådor.

Varje kundimplementering är unik och skräddarsydd för att uppfylla en viss organisations mål, och som sådan varierar vikten av en viss namnrymd från kund till kund. Exempel från verkligheten:

* Ditt företag kan betrakta varje e-postadress som en enpersonsenhet och därför använda [identitetsinställningarna](./identity-settings-ui.md) för att konfigurera e-postnamnområdet som unikt. Ett annat företag kanske vill representera enpersonsenheter som har flera e-postadresser och därmed konfigurera e-postnamnutrymmet som inte unikt. Dessa företag måste använda ett annat ID-namnutrymme som unikt, till exempel ett CRMID-namnutrymme, så att det kan finnas en identifierare för en person som är länkad till flera e-postadresser.
* Du kan samla in onlinebeteende med hjälp av namnutrymmet Inloggnings-ID. Detta inloggnings-ID kan ha en 1:1-relation med CRMID, som sedan lagrar attribut från ett CRM-system och kan betraktas som det viktigaste namnutrymmet. I det här fallet avgör du att CRMID-namnutrymmet är en mer korrekt representation av en person, medan namnutrymmet för inloggnings-ID är det näst viktigaste.

Du måste göra konfigurationer i identitetstjänsten som återspeglar vikten av dina namnutrymmen eftersom detta påverkar hur profiler och relaterade identitetsdiagram formateras och delas upp.

## Ange dina prioriteringar

Bestämning av namnområdesprioritet baseras på följande faktorer:

### Identitetsdiagramstruktur

Om din organisations diagramstruktur är i flera lager bör namnområdesprioriteten återspegla detta så att rätt länkar tas bort vid komprimering av diagram.

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

Ett annat sätt att se på det här ämnet är genom kardinalitet. Hur många identiteter kommer att skapas för en viss person? I de flesta fall har en person ett CRMID, en handfull identifierare för hårdvaruenheter (IDFA/GAID-återställningar bör inte ske så ofta) och ännu fler cookies (en person kan navigera på flera enheter, använda inkogenläge eller återställa cookies när som helst). I allmänhet anger **lägre kardinalitet ett namnutrymme med ett högre värde**.

## Validera inställningarna för namnområdesprioritet

När du har fått en uppfattning om hur du ska prioritera namnutrymmen kan du använda verktyget för diagramsimulering i användargränssnittet för att testa olika scenarier för komprimering av diagram och se till att dina prioritetskonfigurationer returnerar de förväntade diagramresultaten. Mer information finns i handboken om hur du använder verktyget [Diagramsimulering](./graph-simulation.md).

## Konfigurera namnområdesprioritet

Namnområdesprioriteten kan konfigureras med hjälp av användargränssnittet [för identitetsinställningar](./identity-settings-ui.md). I gränssnittet för identitetsinställningar kan du dra och släppa ett namnutrymme för att fastställa dess relativa betydelse.

>[!IMPORTANT]
>
>Du kan inte prioritera namnutrymmen för enheter/cookies framför personnamnutrymmen. Den här begränsningen säkerställer att inga felkonfigurationer görs.

## Användning av namnområdesprioritet

För närvarande påverkar namnområdesprioriteten systembeteendet för kundprofilen i realtid. Bilden nedan visar detta koncept. Mer information finns i guiden om [Adobe Experience Platform och programarkitekturdiagram](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Ett diagram över programomfånget för namnområdesprioritet](../images/namespace-priority/application-scope.png)

### Identitetstjänst: Identitetsoptimeringsalgoritm

För relativt komplexa diagramstrukturer spelar namnområdesprioriteten en viktig roll när det gäller att säkerställa att rätt länkar tas bort när diagramkomprimeringsscenarier inträffar. Mer information finns i [översikten över algoritmen för identitetsoptimering](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Kundprofil i realtid: primär identitetsbestämning för upplevelsehändelser

* När du har konfigurerat identitetsinställningar för en viss sandlåda bestäms den primära identiteten för upplevelsehändelser av den högsta namnområdesprioriteten i konfigurationen.
   * Det beror på att upplevelsehändelser är dynamiska till sin natur. En identitetskarta kan innehålla tre eller fler identiteter, och namnområdesprioriteten ser till att det viktigaste namnutrymmet är kopplat till upplevelsehändelsen.
* Därför kommer följande konfigurationer **inte längre att användas av kundprofilen i realtid**:
   * Den primära identitetskonfigurationen (`primary=true`) när identiteter skickas i identityMap med API:t för Web SDK, Mobile SDK eller Edge Network Server (ID-namnområde och identitetsvärde används fortfarande i Profile). **Obs!**: Tjänster utanför kundprofilen i realtid, t.ex. datasjölagring eller Adobe Target, fortsätter att använda den primära identitetskonfigurationen (`primary=true`).
   * Alla fält som markerats som primär identitet i ett XDM Experience Event Class-schema.
   * Standardinställningar för primär identitet i Adobe Analytics-källkopplingen (ECID eller AAID).
* Å andra sidan bestämmer inte namnområdesprioriteten **den primära identiteten för profilposter**.
   * För profilposter bör du fortsätta att definiera dina identitetsfält i schemat, inklusive den primära identiteten. Mer information finns i guiden [Definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md).

>[!TIP]
>
>* Namnområdesprioriteten är **en egenskap för ett namnområde**. Det är ett numeriskt värde som tilldelas ett namnutrymme för att ange dess relativa betydelse.
>
>* Primär identitet är den identitet som ett profilfragment lagras mot. Ett profilfragment är en datapost som lagrar information om en viss användare: attribut (till exempel CRM-poster) eller händelser (till exempel webbsurfning).

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

Om identitetsinställningarna är aktiverade kommer beräknade attribut att använda namnområdesprioritet för att lagra det beräknade attributvärdet. För en given händelse kommer identiteten med den högsta namnområdesprioriteten att ha värdet för det beräknade attributet skrivet mot den. Mer information finns i användargränssnittshandboken för [beräknade attribut](../../profile/computed-attributes/ui.md).

### Data Lake

Inmatningen av data i sjön fortsätter att följa de primära identitetsinställningarna som konfigurerats på [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) och scheman.

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

### Partnerbyggda destinationer

Uppdaterade resultat för identifiering av målgrupper för profiler som är kopplade till en delad enhet kan inte skickas till nedströmsdestinationer. Detta kan inträffa i vissa sällsynta fall där:

* Målgruppskvalificering baseras endast på anonym aktivitet.
* Inloggningar för flera profiler sker på kort tid.

Mer information om partnerbyggda mål finns i [målöversikten](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Integritetstjänst

[Borttagningsbegäranden](../privacy.md) för Privacy Service fungerar på följande sätt, för en viss identitet:

* Kundprofil i realtid: Tar bort alla profilfragment med angivet identitetsvärde som primär identitet. **Den primära identiteten i profilen bestäms nu utifrån namnområdesprioritet.**
* Datasjön: Tar bort alla poster med den angivna identiteten som primär eller sekundär identitet.

Mer information finns i [Översikt över sekretesstjänsten](../../privacy-service/home.md).

### Adobe Target

Adobe Target kan generera oväntad målinriktning för delade enhetsscenarier när kantsegmentering används.