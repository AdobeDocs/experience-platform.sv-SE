---
title: Totalt datavolym - mått
description: Lär dig mer om det nya måttet Total Data Volume och hur det ersätter det tidigare måttet för genomsnittlig profilrikedom.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Totalt datavolym-mått

Från och med den 24 september 2024 kommer det totala datavolym-måttet att ersätta det tidigare måttet för genomsnittlig profilnoggrannhet.

Total datavolym representerar den totala mängden data som är tillgängliga för Adobe Experience Platform kundprofil i realtid och som kan användas i engagemangsarbetsflöden. Det här värdet motsvarar det adresserbara målgruppsmåttet multiplicerat med medelprofilens noggrannhet.

## Vanliga frågor och svar {#faq}

I följande avsnitt visas vanliga frågor om uppdateringen.

### Varför har den här ändringen gjorts?

Den här ändringen har gjorts för att förenkla processen att uppfylla kraven i licensberättigandemåtten. Vi har ofta hört från kunderna att de tycker att medelhög profilrikedom är svårt att förstå och hantera. Med den här förändringen hoppas vi att du bättre kan förstå och hantera din licensierade användning av kundprofilen i realtid.

### Ändrar den här förändringen i mätvärden mitt tillstånd för profilarkivet?

Nej. Ditt tillstånd för profilarkivet förblir detsamma som tidigare, eftersom den totala datavolymen motsvarar den adresserbara målgruppen multiplicerad med din giltiga genomsnittliga profilprecision.

### Påverkar den här ändringen berättigandepaketen som jag har köpt?

Nej. Du får fortfarande tillgång till förmånspaketen som du tidigare köpt.

### Hur kommer det sig att jag ser ett annat värde för min totala datavolym jämfört med min profilbutik?

Den totala datavolymen representerar den **totala** mängden data som är tillgängliga för profilen som ska användas i engagemangsarbetsflöden. Mätningen har uppdaterats för att vara mer deterministisk och förklarlig. De flesta användare bör **inte** se en betydande förändring mellan sin totala datavolym och sin totala profillagring. Om du är orolig kontaktar du en kundtjänstrepresentant.

### Måste jag återskapa mina ändringar för att fortsätta hantera min genomsnittliga profilprecision?

Nej. Alla åtgärder, som filtrering, inaktivering av profiler för datauppsättningar, samt inställning av förfallodatum för Experience-händelser och förfallodatum för pseudonyma profildata fortsätter att vara en del av hanteringen av den totala datavolymen.

### Varför är den fil jag har infogat i sandlådan en annan storlek än den totala datavolymen?

Profilen optimerar data för snabb bearbetning för att köra de personaliserings- och engagemangsarbetsflöden som systemet är utformat för. Filstorleken på klientsidan kan skilja sig från den totala datavolymen på grund av faktorer som typ av kodning, komprimering och format.

### Gäller den här ändringen SKU:er som har en delad gräns för både profil- och datasjön?

Kunder som använder SKU:er som har delad genomsnittlig profilnoggrannhet mellan profil och datavinje kommer att fortsätta att se måttet för total förbrukning av lagring och **inte** kommer att se måttet för genomsnittlig profilnoggrannhet.
