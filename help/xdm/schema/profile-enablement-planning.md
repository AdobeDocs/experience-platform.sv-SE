---
keywords: Experience Platform;profil;kundprofil i realtid;schema;datauppsättning;planering;aktivering
solution: Experience Platform
title: Planering för aktivering av kundprofiler i realtid
description: Granska de viktigaste övervägandena du måste utvärdera innan du aktiverar scheman och datauppsättningar för kundprofil i realtid.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planering för aktivering av kundprofiler i realtid

Använd den här sidan för att bekräfta att ditt schema och din datauppsättning är klara innan du aktiverar dem för kundprofil i realtid. Slutför den här planeringsgranskningen när du har utformat dina schemafält men innan du aktiverar schemat för profil. Profilaktivering tillämpar permanenta beteendeförändringar i din datamodell. Du kan inte ändra schemaaktivering, och aktiveringen av en datauppsättning påverkar hur dess poster behandlas i kundprofilen i realtid. Granska den här vägledningen för att undvika oavsiktlig aktivering, problem med datakvaliteten eller långvariga begränsningar i schemadesignen.

Om du aktiverar Profil avgör du hur data sammanfogas, sammanfogas och aktiveras i Experience Platform. Planeringen ser till att schemastrukturen, identitetskonfigurationen och datauppsättningssyftet är korrekta innan du gör ändringen. När du har slutfört den här planeringsgranskningen kan du fortsätta att aktivera data för profilen i **[!UICONTROL Schema Editor]**- eller **[!UICONTROL Dataset]**-gränssnittet.

## Förhandskrav

Innan du använder den här planeringsguiden bör du kontrollera att du har:

* Skapade ett schema med hjälp av API:t **[!UICONTROL Schema Editor]** eller Schema Registry. Se självstudiekursen [för att skapa scheman](../tutorials/create-schema-ui.md) för att komma igång.
* Minst ett identitetsfält har konfigurerats i schemat. Mer information finns i konfigurationsguiden för [identitetsfältet](../ui/fields/identity.md).
* Grundläggande förståelse för [kundprofilen i realtid](../../profile/home.md) och hur den använder scheman för att skapa enhetliga kundvyer.
* Lämpliga behörigheter för att aktivera scheman och datauppsättningar för profilen. Kontakta systemadministratören om du inte har tillgång till alternativen för profilaktivering.

Om du inte har slutfört dessa krav börjar du med självstudiekursen [för att skapa schema](../tutorials/create-schema-ui.md) innan du fortsätter med den här planeringsguiden.

## Varför planera saker {#why-planning-matters}

Aktiveringen av profiler ändrar permanent hur Experience Platform hanterar dina data. Följande permanenta ändringar gäller för scheman och datauppsättningar.

**Scheman**: När du aktiverar ett schema för profilen kan du inte inaktivera eller ta bort det. Du kan inte heller ta bort eller byta namn på fält från schemat efter att data har importerats. Den här varaktigheten innebär att schemats design måste vara fullständig och stabil innan du aktiverar profilen, eftersom du inte kan ändra beslutet eller förenkla strukturen senare.

**Datauppsättningar**: När du aktiverar en datauppsättning för profil används kundprofilen i realtid för att skapa och uppdatera profiler. Granska datauppsättningsaktiveringsbeteendet i användarhandboken för [datauppsättningen](../../catalog/datasets/enable-for-profile.md). Till skillnad från scheman kan du inaktivera eller ta bort datauppsättningen senare, men om du gör det tas tillhörande profilposter bort, vilket kan påverka arbetsflödena för segmentering och aktivering. Tänk på effekten längre fram i kedjan innan du gör ändringar i en aktiverad datauppsättning.

Eftersom dessa ändringar påverkar processerna längre fram i kedjan bör du kontrollera att ett schema och dess datauppsättningar är lämpliga för profilen innan du aktiverar dem.

### Förstå aktiveringsarbetsflödet

Du måste aktivera både schemat OCH datauppsättningarna som använder det schemat för profilen. Aktivera resurser i följande ordning:

1. **Aktivera schemat för profilen**: Aktivera först profilen i schemat i **[!UICONTROL Schema Editor]**. Detta gör att alla datauppsättningar som använder det här schemat kan aktiveras för profilen.
2. **Aktivera enskilda datauppsättningar för profilen**: När schemat har aktiverats ska du aktivera profilen för varje datauppsättning som ska bidra till enhetliga kundprofiler.

Du kan inte aktivera en datauppsättning för profilen om dess schema inte redan är aktiverat. Schemat fungerar som en förutsättning för datauppsättningsaktivering. Denna tvåstegsprocess säkerställer att datamodellen valideras innan kundprofilen i realtid börjar bearbeta poster.

## När ett schema eller en datauppsättning ska aktiveras för profilen {#when-to-enable}

Granska villkoren nedan för att bekräfta att aktiveringen av profilen är lämplig för dina data.

Aktivera profil i följande situationer:

* Data bidrar till en enhetlig kundprofil.
* Data krävs för segmenterings- eller aktiveringsarbetsflöden.
* Schemat innehåller identitetsfält som representerar en person- eller kundnivånyckel.
* Datauppsättningen innehåller Experience Events eller profilattribut som måste sammanfogas över flera kanaler. Granska [XDM ExperienceEvent-klassen](../classes/experienceevent.md) för att bekräfta händelsekraven.

## När det inte går att aktivera ett schema eller en datauppsättning för profilen {#when-not-to-enable}

Undvik att aktivera profil i följande fall:

* Schemat representerar endast sökdata eller referensdata.
* Datauppsättningen innehåller testdata, temporära data eller icke-produktionsdata.
* Uppgifterna identifierar inte någon person eller används endast för rapportering.
* Schemat är experimentellt eller strukturellt ofullständigt.

Om du aktiverar Profil i dessa scenarier kan det skapa onödiga profiler, öka licensanvändningen eller medföra långsiktiga schemabegränsningar.

## Viktiga överväganden innan du aktiverar profil {#key-considerations}

Granska övervägandena i det här avsnittet för att se till att ditt schema och din datauppsättning stöder användningsfall för profiler och långsiktig datastyrning. Innan du aktiverar profil bör du kontrollera schemastrukturen, identitetskonfigurationen och datamängdens syfte.

### Schemaberedskap

Granska schemastrukturen för att bekräfta att den stöder profilkrav. Schemat måste innehålla de fält som krävs för segmentering och aktivering, men inte fält som är experimentella eller inte behövs på lång sikt. Kom ihåg att eventuella ytterligare fält som du lägger till efter aktivering måste vara additiva (mer information finns i [begränsningar för immutability-schema](#why-planning-matters)). Den här begränsningen innebär att du bör validera fältvalet noggrant innan du aktiverar Profil. Mer information om tillåtna uppdateringar finns i [schemaförändringsreglerna](./composition.md#evolution).

### Identitetskonfiguration

Identitetskonfigurationen avgör hur profiler sammanfogar poster mellan datauppsättningar. Börja med att bekräfta att en giltig primär identitet har valts - det här fältet måste vara stabilt, unikt och ifyllt på alla poster. Kontrollera att identitetsnamnutrymmen har tilldelats på rätt sätt för att förhindra sammanfogningsfel. Om du använder sekundära identiteter måste du bekräfta att de har stöd för dina användningsfall utan att orsaka profilkollisioner, som kan inträffa när olika personer delar samma identitetsvärde. Kundprofilen i realtid löser konflikter genom att tillämpa sammanslagningsprinciper som avgör vilka data som prioriteras när motstridiga poster sammanfogas.

### Datauppsättningens syfte

Aktivera endast en datauppsättning för profilen när den bidrar direkt till profilattribut eller Experience Events som används i arbetsflöden längre fram i kedjan. Undvik att aktivera datauppsättningar som innehåller sök- eller referensdata som inte används i segmentering, test- eller exempeldata eller operationssystemgenererade poster som inte är avsedda för aktivering. Dessa datatyper bidrar inte till enhetliga kundprofiler och skapar onödiga lagringskostnader. Om en datauppsättning inte innehåller identitetsfält eller kundbeteendedata som stöder segmentering och aktivering ska du inte aktivera den för profil.

**Exempel**:

Du aktiverar en&quot;Customer Purchase Events&quot;-datauppsättning som innehåller transaktionsdata med kund-ID:n. Kundprofilen i realtid använder dessa händelser för att bygga kundtidslinjer och aktivera segmentering baserat på inköpsbeteende.

Du aktiverar INTE en produktkatalogdatauppsättning som bara innehåller SKU-referensdata utan kundidentifierare. Om du aktiverar den här typen av datauppsättning skapas onödig lagringskapacitet utan att bidra till enhetliga kundprofiler.

## Checklista för föraktivering {#pre-enablement-checklist}

Använd den här checklistan för att bekräfta beredskapen innan du aktiverar ett schema eller en datauppsättning för profilen. Slutför varje objekt innan du aktiverar Profil.

### Kontroller på schemanivå

Börja med att verifiera att schemats design är fullständig och stabil. Granska schemat för att bekräfta att alla obligatoriska fält för ditt användningsfall finns och att inga experimentella eller temporära fält inkluderas. Läs [metoddesignens bästa praxis](./best-practices.md) för att se till att ditt schema följer rekommenderade mönster. Få ditt team godkänt i den slutliga fältlistan (se [begränsningar för oföränderliga scheman](#why-planning-matters)).

Verifiera sedan att din primära identitetskonfiguration är korrekt. Öppna ditt schema i **[!UICONTROL Schema Editor]** och leta upp fältet som är markerat med identitetsikonen. Bekräfta att det här fältet är ifyllt i källdata och att identitetsnamnutrymmet är lämpligt för ditt användningsfall. Den primära identiteten måste vara stabil, unik och tillförlitlig i alla poster för att säkerställa korrekt sammanfogning av profiler.

Bekräfta slutligen att du inte behöver byta namn på eller ordna om schemastrukturen. Ändringar av schemastrukturen är begränsade till enbart additiva uppdateringar (se [begränsningar för immutabilitet i schema](#why-planning-matters)). Långsiktig tvetydighet i namngivning eller organisation kan inte korrigeras senare, så åtgärda problemen innan aktivering.

### Kontroller på datauppsättningsnivå

För varje datauppsättning som du planerar att aktivera börjar du med att bekräfta att den innehåller profilrelevanta data. Granska exempelposter för att kontrollera att de innehåller kund- eller händelsedata i stället för enbart operativ eller referensinformation. Se till att posterna innehåller identitetsvärden som länkar till kundprofiler. Datauppsättningar utan identitetsfält eller kundbeteendedata ska inte aktiveras för profilen.

Avgör om datauppsättningen ska bidra till identitetssammanfogning eller -segmentering genom att förstå hur dess identitetsvärden relaterar till andra datauppsättningar i din profilaktiverade miljö. Fundera på om posterna i den här datauppsättningen ska sammanfogas med befintliga profiler eller skapa nya profilfragment. Granska dokumentationen för [sammanfogningsprincipen](../../profile/merge-policies/overview.md) för att förstå hur kundprofilen i realtid sammanfogar poster mellan datauppsättningar och hur den här datauppsättningen passar in i din övergripande identitetsstrategi.

Innan du aktiverar datauppsättningen bör du uppskatta antalet unika identitetsvärden som den innehåller och verifiera att dessa identitetsvärden representerar faktiska kunder i stället för att testa konton eller systemidentifierare. Bekräfta att aktiveringen av den här datauppsättningen passar era licensrättigheter eftersom varje unik identitet bidrar till det adresserbara antalet målgrupper. Profilaktivering ökar lagrings- och bearbetningskostnaderna, så se till att datauppsättningen ger ett värde som motiverar investeringen.

Om du slutför den här checklistan kan du förhindra problem som inte kan ångras efter aktiveringen.

## Aktivera profil för ditt schema och din datamängd {#enable-profile}

När du har slutfört föraktiveringskontrollen följer du de här stegen för att aktivera profilen. Så som förklaras i [Om du förstår aktiveringsarbetsflödet](#why-planning-matters) måste du aktivera schemat innan du aktiverar datauppsättningar som använder det schemat.

### Aktivera ditt schema för profil

Aktivera först profilen i ditt schema:

1. Navigera till **[!UICONTROL Schemas]** i Experience Platform-gränssnittet.
2. Välj ditt schema från listan för att öppna det i **[!UICONTROL Schema Editor]**.
3. Välj växlingsknappen **[!UICONTROL Profile]** i den högra listen. Panelen Schemaegenskaper visar en bekräftelsedialogruta.
4. Bekräfta genom att välja **[!UICONTROL Enable]**. Schemat är nu aktiverat för profilen.

Detaljerade instruktioner finns i [guiden för schemaaktivering](../ui/resources/schemas.md#profile) i dokumentationen för Schemaredigeraren.

### Aktivera datauppsättningar för profil

När schemat har aktiverats för profilen aktiverar du varje datauppsättning som ska bidra till enhetliga profiler:

1. Navigera till **[!UICONTROL Datasets]** i Experience Platform-gränssnittet.
2. Välj en datauppsättning i listan för att öppna sidan med datauppsättningsinformation.
3. Välj växlingsknappen **[!UICONTROL Profile]** i den högra listen. Panelen för datauppsättningsegenskaper uppdateras och visar profil är aktiverad.

Upprepa den här processen för varje datauppsättning som ska bidra till kundprofilen i realtid. Detaljerade instruktioner och API-aktiveringsalternativ finns i användarhandboken för datauppsättningen som det refereras till i avsnittet Krav.

### Varför beställa?

Så som förklaras i [Om du förstår aktiveringsarbetsflödet](#why-planning-matters) måste du aktivera schemat innan du aktiverar datauppsättningar. Detta garanterar att kundprofilen i realtid validerar schemastrukturen så att den stöder profilåtgärder innan datauppsättningsaktivering tillåts, och att alla datauppsättningar som använder schemat ärver rätt fältdefinitioner för segmentering och identitetssammanfogning.

När du har aktiverat både schemat och datauppsättningarna börjar kundprofilen i realtid bearbeta poster och skapa enhetliga kundprofiler. Poster som har importerats före aktivering inkluderas inte i profiler om du inte ändrar data.

## Nästa steg {#next-steps}

Du har granskat de permanenta effekterna av profilaktivering, bekräftat att ditt schema och dina datauppsättningar är klara och kontrollerat att din identitetskonfiguration stöder dina användningsfall. Om du vill få en djupare förståelse för schemastruktur och fältrelationer kan du gå igenom [Grunderna i schemakomposition](../schema/composition.md) som förklarar schemaförändringsregler och hur fält interagerar inom datamodellen. Om du stöter på problem under eller efter aktiveringen kan du läsa [XDM-felsökningsguiden](../troubleshooting-guide.md) för att få information om vanliga problem och lösningar. Mer information om hur identitetsnamnutrymmen påverkar sammanfogning och upplösning av profiler finns i [Översikt över identitetsnamnutrymmen](../../identity-service/features/namespaces.md).
