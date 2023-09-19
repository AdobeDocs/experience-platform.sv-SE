---
title: Vanliga frågor om beräknade attribut
description: Få svar på vanliga frågor om hur du använder beräknade attribut.
source-git-commit: 631b67eb6609381235113009acefaf0d0cd8063c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---


# Frågor och svar

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Nedan följer en lista med vanliga frågor om beräknade attribut.

## Hur får jag åtkomst till beräknade attribut?

För att få åtkomst till beräknade attribut måste du ha rätt behörighet (**Visa beräknade attribut** och **Hantera beräknade attribut**). Mer information om vilka behörigheter som krävs finns i [dokumentation om åtkomstkontroll](../../access-control/home.md). Läs mer om hur du tillämpar dessa behörigheter i [hantera behörighetshandbok](../../access-control/ui/permissions.md).

## Vilka datauppsättningar bidrar till beräknade attributberäkningar?

Beräknade attribut behandlar realtidsdata om kundupplevelsehändelser som aktiverats av kundprofiler för beräkning av beräknade attribut.

## Vilka XDM-fält (Experience Data Model) kan användas för att skapa beräknade attribut?

Alla XDM-fält i Experience Event-föreningsschemat kan användas för att skapa beräknade attribut.

## Vad är den&quot;senaste utvärderingstiden&quot;?

Den senaste utvärderingstiden innebär att händelserna **föregående** till den tidsstämpeln beaktades i den senaste lyckade uppdateringen av det beräknade attributet.

## Kan jag välja uppdateringsfrekvens? Hur bestäms det här?

Uppdateringsfrekvensen bestäms automatiskt utifrån det beräknade attributets uppslagsperiod. Mer information finns i [avsnitt för uppslagsperiod](./overview.md#lookback-periods) av översikten över beräknade attribut.

## Hur påverkas beräkningarna av när Experience Event-data förfaller?

Beräknade attributberäkningar är efterfyllda för den definierade uppslagstiden i den första utvärderingen och uppdateras baserat på inkrementella händelser för efterföljande uppdateringar. Därför är dessa beräkningar **not** påverkas av att Experience Event-data upphör att gälla för gamla data efter den första utvärderingen.

Om du till exempel skapar ett beräknat attribut som utvärderas månadsvis med en 3 månaders uppslagsperiod, för den första utvärderingen, beräknas det beräknade attributet för alla händelser inom den 3-månaders uppslagsperioden. Även om Experience Event-datauppsättningen har ett förfallodatum på en månad kommer dessa data att upphöra att gälla **not** påverkar den månatliga uppdateringen av beräknade attribut, eftersom nästa månads utvärderingskörning stegvis sammanställer händelser och uppdaterar beräkningen.

>[!NOTE]
>
>Utgångna data **inte** senare fyllas i med ett beräknat attribut. Utgångsdatum för händelsedatamängd **kan** begränsade möjligheten att validera det beräknade attributets värde vid en senare tidpunkt. Om du vill validera det beräknade attributvärdet ska din uppslagsperiod vara kvar **inom** Gränserna för dataförfallodatum.

## Kan jag skapa ett beräknat attribut baserat på ett annat beräknat attribut?

Eftersom beräknade attribut skapas med Experience Event-fält och finns i ett Profile-fält går det inte att använda ett beräknat attribut direkt för att skapa ett annat beräknat attribut.

## Finns det några begränsningar för hur många beräknade attribut jag kan skapa?

Ja, det finns en gräns för hur många beräknade attribut du kan skapa. Se produktbeskrivningen eller kontakta kontogruppen på Adobe för mer information.

## Kommer det att påverka nedladdningen av ett beräknat attribut?

Innan du inaktiverar det beräknade attributet måste du **bör** ta bort dem från era system längre fram i kedjan (som segmentering, resor eller destinationer), eftersom det kan uppstå komplikationer om de inte tas bort.

## Vad händer när jag inaktiverar ett beräknat attribut? {#inactive-status}

När ett beräknat attribut är inaktiverat eller inaktiverat uppdateras det inte längre. Detta beräknade attribut resulterar i **inte** användas för profilsökning eller annan nedladdning.

## Hur bidrar beräknade attribut till ökat engagemang?

Beräknade attribut driver profilberikning genom att samla dina händelseattribut på en sammanslagen profilnivå. Du kan till exempel anpassa e-postmeddelanden för marknadsföring med den senast visade produkten.

## Hur ofta utvärderas beräknade attribut? Är detta relaterat till målgruppens utvärderingsschema?

Beräknade attribut utvärderas i grupper oberoende av segmenteringsschemat. Det innebär att oavsett segmenteringstyp (gruppsegmentering eller direktuppspelningssegmentering) kommer det beräknade attributet att utvärderas enligt ett eget schema (timme, dag, vecka eller månad).

När målgruppen utvärderas används **senaste** värdet för det beräknade tillgängliga attributet.

## Hur interagerar beräknade attribut med målgrupper som utvärderas genom direktuppspelningssegmentering?

Om en målgrupp som utvärderas med avseende på direktuppspelad segmentering använder ett beräknat attribut tar den **senaste värdet** av det beräknade attributet medan målgruppen utvärderas. Om publiken till exempel letar efter köphändelser, kommer publiken att referera till det senast utvärderade beräknade attributvärdet när köphändelsen inträffar.

## Kan jag använda beräknade attribut på Edge?

I likhet med andra profilattribut är beräknade attribut tillgängliga och kan användas på kanterna. Observera att beräknade attribut är **not** beräknas på kanten.

## Hur används dataanvändningsetiketter på beräknade attribut?

Beräknade attribut härleder automatiskt dataanvändningsetiketter från de källfält och datamängder som användes för att definiera de beräknade attributen. Detta garanterar att dina beteendedata används på rätt sätt.

## Hur använder jag beräknade attribut med Adobe Journey Optimizer?

Om du vill använda beräknade attribut under resor måste du lägga till `SystemComputedAttributes` fältgrupp till datakällan Experience Platform. Mer information om hur du konfigurerar datakällan för Experience Platform finns i [Adobe Experience Platform datakällguide](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=en).
