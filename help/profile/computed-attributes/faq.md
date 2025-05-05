---
title: Vanliga frågor om beräknade attribut
description: Få svar på vanliga frågor om hur du använder beräknade attribut.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Vanliga frågor och svar

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Nedan följer en lista med vanliga frågor om beräknade attribut.

## Hur får jag åtkomst till beräknade attribut?

För att få åtkomst till beräknade attribut måste du ha rätt behörighet (**Visa beräknade attribut** och **Hantera beräknade attribut**). Mer information om vilka behörigheter som krävs finns i [åtkomstkontrollsdokumentationen](../../access-control/home.md). Om du vill lära dig hur du tillämpar de här behörigheterna läser du [handboken om att hantera behörigheter](../../access-control/ui/permissions.md).

## Vilka datauppsättningar bidrar till beräknade attributberäkningar?

Beräknade attribut behandlar realtidsdata om kundupplevelsehändelser som aktiverats av kundprofiler för beräkning av beräknade attribut.

## Vilka XDM-fält (Experience Data Model) kan användas för att skapa beräknade attribut?

Alla XDM-fält i Experience Event-föreningsschemat kan användas för att skapa beräknade attribut.

## Vad betyder&quot;senaste utvärdering&quot; och&quot;senaste utvärderingsstatus&quot;?

Senast utvärderad avser tidsstämpeln till vilken händelser övervägs i den senaste lyckade körningen. Senaste utvärderingsstatus avser huruvida den senaste utvärderingskörningen lyckades eller inte.

## Kan jag välja uppdateringsfrekvens? Hur bestäms det här?

Uppdateringsfrekvensen bestäms automatiskt utifrån det beräknade attributets uppslagsperiod. Mer information finns i avsnittet [uppslagsperiod](./overview.md#lookback-periods) i översikten över beräknade attribut.

## Hur påverkas beräkningarna av när Experience Event-data förfaller?

Beräknade attributberäkningar är efterfyllda för den definierade uppslagstiden i den första utvärderingen och uppdateras baserat på inkrementella händelser för efterföljande uppdateringar. Därför påverkas dessa beräkningar **inte** av Experience Event-datans förfallodatum för gamla data efter den första utvärderingen.

Om du till exempel skapar ett beräknat attribut som utvärderas månadsvis med en 3 månaders uppslagsperiod, för den första utvärderingen, beräknas det beräknade attributet för alla händelser inom den 3-månaders uppslagsperioden. Även om Experience Event-datauppsättningen har ett dataförfallodatum på en månad, kommer detta dataförfallodatum **inte** att påverka den månatliga beräknade attributuppdateringen, eftersom nästa månads utvärderingskörning stegvis sammanställer händelser och uppdaterar beräkningen.

>[!NOTE]
>
>Utgångna data **kan inte** fyllas i senare av ett beräknat attribut. Utgångsdatum för händelsedatamängd **kan** begränsa möjligheten att validera det beräknade attributets värde vid en senare tidpunkt. Om du vill validera det beräknade attributvärdet ska din uppslagsperiod vara **inom** gränserna för dataförfallodatumen.

## Kan jag skapa ett beräknat attribut baserat på ett annat beräknat attribut?

Eftersom beräknade attribut skapas med Experience Event-fält och finns i ett Profile-fält går det inte att använda ett beräknat attribut direkt för att skapa ett annat beräknat attribut.

## Finns det några begränsningar för hur många beräknade attribut jag kan skapa?

Ja, det finns en gräns för hur många beräknade attribut du kan skapa. Den här gränsen gäller endast för **aktiva** beräknade attribut. Se produktbeskrivningen eller kontakta kontogruppen på Adobe för mer information.

## Kommer det att påverka nedladdningen av ett beräknat attribut?

Innan du inaktiverar ditt beräknade attribut bör du **ta** bort dem från dina underordnade system (till exempel segmentering, resor eller destinationer), eftersom det kan finnas komplikationer som uppstår om de inte tas bort.

## Vad händer när jag inaktiverar ett beräknat attribut? {#inactive-status}

När ett beräknat attribut är inaktiverat eller inaktiverat uppdateras det inte längre. Därför kan det här beräknade attributet **inte** användas i profilsökning eller andra underordnade användningar.

## Hur bidrar beräknade attribut till ökat engagemang?

Beräknade attribut driver profilberikning genom att samla dina händelseattribut på en sammanslagen profilnivå. Du kan till exempel anpassa e-postmeddelanden för marknadsföring med den senast visade produkten.

## Hur ofta utvärderas beräknade attribut? Är detta relaterat till målgruppens utvärderingsschema?

Beräknade attribut utvärderas i en **batch**-frekvens som är **oberoende** av schemat för målgrupps-, mål- och reseutvärderingen. Det innebär att oavsett segmenteringstyp (gruppsegmentering eller direktuppspelningssegmentering) kommer det beräknade attributet att utvärderas enligt ett eget schema (timme, dag, vecka eller månad).

Första gången du utvärderar ditt beräknade attribut sker det inom 24 timmar efter att det **skapades**. De efterföljande batchutvärderingarna görs varje timme, dag, vecka eller månad beroende på den definierade uppslagsperioden.

Om t.ex. en första utvärdering görs kl. 12 UTC den 9 oktober kommer efterföljande utvärderingar att ske vid följande tidpunkter:

- Nästa dagliga uppdatering: 12:00 UTC den 10 oktober
- Nästa veckouppdatering: 12:00 UTC den 15 oktober
- Nästa månadsuppdatering: 12:00 UTC den 1 november

>[!IMPORTANT]
>
>Detta gäller endast om snabbuppdatering är **inte** aktiverad. Läs avsnittet [fast uppdatering](./overview.md#fast-refresh) om du vill veta hur uppslagsperioden ändras när snabb uppdatering är aktiverad.

Uppdateringarna **veckovis** och **månadsvis** äger rum i början av **kalenderveckan** (söndagen i den nya veckan) eller i början av **kalendermånaden** (den första i den nya månaden), i motsats till exakt en vecka eller en månad efter det första utvärderingsdatumet.

>[!NOTE]
>
>Det beräknade attributvärdet **uppdateras inte** omedelbart i profilen efter varje utvärderingskörning. För att säkerställa att det uppdaterade värdet finns i dina profiler bör du överväga en buffert på några timmar mellan utvärderingstiden och beräknad attributanvändning. Det beräknade uppdateringsschemat för attribut är **systembestämt** och **kan inte** ändras. Kontakta Adobe kundtjänst om du vill ha mer information.

## Hur interagerar beräknade attribut med målgrupper som utvärderas genom direktuppspelningssegmentering?

Om en målgrupp som utvärderas av en direktuppspelningssegmentering använder ett beräknat attribut, kommer det att ta det **senaste värdet** för det beräknade attributet medan målgruppen utvärderas. Om publiken till exempel letar efter köphändelser, kommer publiken att referera till det senast utvärderade beräknade attributvärdet när köphändelsen inträffar.

## Kan jag använda beräknade attribut på Edge?

I likhet med andra profilattribut är beräknade attribut tillgängliga och kan användas på kanterna. Observera att beräknade attribut **inte** beräknas på kanten.

## Hur används dataanvändningsetiketter på beräknade attribut?

Beräknade attribut härleder automatiskt dataanvändningsetiketter från de källfält och datamängder som användes för att definiera de beräknade attributen. Detta garanterar att dina beteendedata används på rätt sätt.

## Hur använder jag beräknade attribut med Adobe Journey Optimizer?

Om du vill använda beräknade attribut i resor måste du lägga till fältgruppen `SystemComputedAttributes` i Experience Platform-datakällan. Mer information om hur du konfigurerar datakällan för Experience Platform finns i [Adobe Experience Platform-guiden för datakälla](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=sv-SE).
