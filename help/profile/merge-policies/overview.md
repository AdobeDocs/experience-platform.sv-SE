---
keywords: Experience Platform;profil;kundprofil i realtid;sammanfogningsprinciper;användargränssnitt;tidsstämpelordning;prioritet för datauppsättning
title: Översikt över kopplingsprofiler
type: Documentation
description: Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en helhetsbild av era enskilda kunder. När du sammanför dessa data är sammanslagningsprinciper de regler som används av Platform för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en enhetlig vy.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# Översikt över kopplingsprofiler

Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. Sammanslagningsprinciper är reglerna som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en enhetlig vy.

Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. I det här dokumentet finns en översikt över sammanfogningsprinciper och vilken roll de spelar i Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse för flera viktiga [!DNL Experience Platform] funktioner. Innan du följer den här guiden och arbetar med sammanfogningsprinciper bör du läsa dokumentationen för följande tjänster:

* [Kundprofil i realtid](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Aktiverar kundprofil i realtid genom att överbrygga identiteter från olika datakällor som hämtas in till [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.

## Förstå kopplingsprofiler

Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en fullständig, enhetlig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som används av Platform för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn.

Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de för att skapa en enda profil för kunden.

När data från flera källor står i konflikt (t.ex. ett fragment listar kunden som&quot;enkel&quot; medan det andra listar kunden som&quot;gift&quot;) avgör sammanfogningspolicyn vilken information som ska inkluderas i profilen för den enskilda personen.

Sammanslagningsprinciper är privata för din organisation, vilket gör att du kan skapa olika profiler för att sammanfoga scheman på de specifika sätt som du behöver. Du kan också ange en standardprincip för sammanfogning som ska användas om en sådan inte uttryckligen anges. Se avsnittet om [standardprinciper för sammanfogning](#default-merge-policy) senare i det här dokumentet om du vill veta mer. Observera att högst fem sammanslagningsprinciper tillåts per organisation.

## Sammanfogningsmetoder {#merge-methods}

Varje profilfragment innehåller information för endast en identitet av det totala antalet identiteter som kan finnas för en individ. När data sammanfogas till en kundprofil finns det en risk för att informationen hamnar i konflikt och prioriteten måste anges.

Om du väljer en sammanfogningsmetod kan du ange vilka datauppsättningsattribut som ska prioriteras om en sammanfogningskonflikt uppstår mellan datauppsättningar.

Det finns två möjliga sammanfogningsmetoder för sammanfogningsprinciper. Var och en av dessa metoder sammanfattas nedan med ytterligare information i följande avsnitt:

* **[!UICONTROL Dataset precedence]:** I händelse av en konflikt ska du prioritera profilfragment baserat på den datauppsättning som de kommer från. När du väljer det här alternativet måste du välja relaterade datauppsättningar och deras prioritetsordning. Läs mer om [datauppsättningens prioritet](#dataset-precedence) sammanfogningsmetod.
* **[!UICONTROL Timestamp ordered]:** I händelse av en konflikt prioriteras profilfragmentet som uppdaterades senast. Läs mer om [tidsstämpel beställd](#timestamp-ordered) sammanfogningsmetod.

### Datauppsättningsprioritet {#dataset-precedence}

När **[!UICONTROL Dataset precedence]** är vald som sammanfogningsmetod för en sammanfogningsprincip, kan du prioritera profilfragment baserat på den datauppsättning som de kommer från. Ett exempel är om din organisation har information i en datauppsättning som är att föredra eller lita på framför data i en annan datauppsättning.

För att skapa en sammanfogningsprincip med **[!UICONTROL Dataset precedence]** måste du välja de profil- och ExperienceEvent-datamängder som ingår och sedan manuellt beställa profildatamängderna. När datauppsättningarna har valts och beställts får den översta datauppsättningen högsta prioritet, den andra datauppsättningen den näst högsta och så vidare.

### Tidsstämpel beställd {#timestamp-ordered}

När profilposter hämtas till Experience Platform hämtas en systemtidsstämpel vid tidpunkten för inmatningen och läggs till i posten. När **[!UICONTROL Timestamp ordered]** är markerat som sammanfogningsmetod för en sammanfogningsprincip, sammanfogas profiler baserat på systemets tidsstämpel. Sammanfogningen görs med andra ord baserat på den tidsstämpel som användes när posten hämtades till Platform.

## Identitetssammanfogning {#id-stitching}

Stygg identitet ([!UICONTROL ID stitching]) är processen att identifiera databragment och kombinera dem för att skapa en fullständig profilpost. För att illustrera de olika sammanfogningsbeteendena bör du överväga en enskild kund som interagerar med ett varumärke med hjälp av två olika e-postadresser.

* **[!UICONTROL None]:** När det här alternativet är markerat sammanfogas inte ID:n. När segmentering sker kommer identiteter som kan tillhöra samma person inte att sammanfogas och segmentering kommer endast att beakta de attribut som är kopplade till varje enskilt ID när man avgör om en kund är berättigad till medlemskap i en målgrupp. Detta kan leda till att en enskild kund har flera profiler och att varje profil kan kvalificera sig för olika målgrupper, vilket resulterar i att flera marknadsföringsmeddelanden skickas till samma kund.
* **[!UICONTROL Private graph]:** När det privata diagrammet är markerat sammanfogas flera identiteter som hör till samma individ. Detta leder till att kunden har en enda profil och möjliggör segmentering för att ta hänsyn till flera attribut från flera relaterade identiteter när man fastställer segmentens kvalifikationer. I det här scenariot har kunden sannolikt en enda profil, kvalificerar sig för en målgrupp baserat på en kombination av attribut mellan identiteter och får bara ett marknadsföringsmeddelande.

Om du vill veta mer om identiteter och deras roll när det gäller att generera profiler och målgrupper börjar du med att läsa [Översikt över identitetstjänsten](../../identity-service/home.md).

## Standardprincip för sammanslagning {#default-merge-policy}

En organisation kan skapa en standardsammanfogningsprincip som används i organisationen när profilfragment sammanfogas. På så sätt kan användarna enkelt välja standardpolicy när de utför åtgärder i Experience Platform, t.ex. att visa kundprofiler eller skapa målgrupper. I de flesta fall används standardprincipen för sammanfogning om inte en annan princip anges.

Varje organisation kan skapa flera sammanfogningsprinciper som är relaterade till en enda XDM-schemaklass, men de kan bara ha en standardsammanfogningsprincip deklarerad för varje klass. Din organisation kan till exempel ha en standardprincip för sammanslagning som är relaterad till [!DNL XDM Individual Profile] och en annan standardpolicy för sammanfogning för en anpassad produktinventeringsklass.

Om du skapar en ny sammanfogningsprincip och anger den som standard, uppdateras den tidigare standardprincipen automatiskt av systemet till att inte längre vara standard.

>[!WARNING]
>
>Profilantal och målgrupper med en befintlig associerad standardsammanfogningsprincip kan påverkas. Alla målgrupper som har en standardprincip för sammanslagning kommer att uppdateras till den nya standardprincipen för sammanslagning.

## Nästa steg

När du har läst den här guiden vet du nu vilken sammanfogningspolicy som är och vilken roll de spelar i Experience Platform. För att börja arbeta med kopplingsregler i användargränssnittet i Experience Platform, se [gränssnittshandbok för sammanslagningsprinciper](ui-guide.md). Om du vill arbeta med sammanfogningsprinciper med API:t går du till [API-slutpunktshandbok för sammanslagningsprinciper](../api/merge-policies.md).
