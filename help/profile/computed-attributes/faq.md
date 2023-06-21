---
title: Vanliga frågor om beräknade attribut
description: Få svar på vanliga frågor om hur du använder beräknade attribut.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Frågor och svar

>[!IMPORTANT]
>
>Beräknade attribut finns för närvarande **beta** och är **not** som är tillgängliga för alla användare.

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Nedan följer en lista med vanliga frågor om beräknade attribut.

## Vilka datauppsättningar bidrar till beräknade attributberäkningar?

Beräknade attribut behandlar realtidsdata om kundupplevelsehändelser som aktiverats av kundprofiler för beräkning av beräknade attribut.

## Vilka XDM-fält (Experience Data Model) kan användas för att skapa beräknade attribut?

Alla XDM-fält i Experience Event-föreningsschemat kan användas för att skapa beräknade attribut.

## Vad är den&quot;senaste utvärderingstiden&quot;?

Den senaste utvärderingstiden innebär att händelserna **föregående** till den tidsstämpeln beaktades i den senaste lyckade uppdateringen av det beräknade attributet.

## Kan jag välja uppdateringsfrekvens? Hur bestäms det här?

Uppdateringsfrekvensen bestäms automatiskt utifrån det beräknade attributets uppslagsperiod. Mer information finns i [avsnitt för uppslagsperiod](./overview.md#lookback-periods) av översikten över beräknade attribut.

## Hur påverkas beräkningarna av när Experience Event-data förfaller?

Beräknade attributberäkningar baseras på den definierade uppslagsperioden och de Experience Events som ligger inom den perioden. Därför är dessa beräkningar **not** påverkas av att Experience Event-data upphör att gälla. För att dina beräknade attribut ska bli korrekta bör du dock behålla uppslagsperioden **inom** Gränserna för era data som förfaller.

## Kan jag skapa ett beräknat attribut baserat på ett annat beräknat attribut?

Eftersom beräknade attribut skapas med Experience Event-fält och finns i ett Profile-fält går det inte att använda ett beräknat attribut direkt för att skapa ett annat beräknat attribut.

## Finns det några begränsningar för hur många beräknade attribut jag kan skapa?

Aktuellt maximalt antal **publicerad** beräknade attribut är 25.

## Kommer det att påverka nedladdningen av ett beräknat attribut?

Innan du inaktiverar det beräknade attributet måste du **bör** ta bort dem från era system längre fram i kedjan (som segmentering, resor eller destinationer), eftersom det kan uppstå komplikationer om de inte tas bort.

## Vad händer när jag inaktiverar ett beräknat attribut? {#inactive-status}

När ett beräknat attribut är inaktiverat eller inaktiverat uppdateras det inte längre. Därför är det här beräknade attributet **inte** användas för profilsökning eller annan nedladdning.

## Hur bidrar beräknade attribut till ökat engagemang?

Beräknade attribut driver profilberikning genom att samla dina händelseattribut på en sammanslagen profilnivå. Du kan till exempel anpassa e-postmeddelanden för marknadsföring med den senast visade produkten.
