---
title: Adobe-hanterade värdar - översikt
description: Läs mer om standardvärdalternativet för distribution av kodbiblioteksbyggen i Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Översikt över värdar som hanteras i Adobe

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Värdar som hanteras av Adobe är standardvärdinställningen för att distribuera taggbiblioteksbyggen i Adobe Experience Platform. När du skapar en ny egenskap via användargränssnittet i datainsamlingen skapas en Adobe-hanterad standardvärd.

Med värdar som hanteras av Adobe levereras biblioteksbyggen till ett tredjepartsnätverk för innehållsleverans (CDN) som Adobe har ingått avtal med. Dessa CDN:er fungerar oberoende av Adobe, så även när Platform genomgår underhåll eller på annat sätt inte fungerar din driftsatta kod som vanligt på dina webbplatser och tillämpningar. Inbäddningskoden för en värddator som hanteras av Adobe refererar till huvudbiblioteksfilen på CDN så att en klientenhet kan hämta filerna vid körning.

I det här dokumentet finns en översikt över värddatorer som hanteras av Adobe i Platform och anvisningar om hur du skapar en ny värddator som hanteras av Adobe i användargränssnittet.

## Akamai

För närvarande är den primära CDN-leverantören för Adobe [Akamai](https://www.akamai.com/). Akamai robusta CDN är framtagen för att leverera innehåll till en global, stor publik av webbbesökare. CDN har redundanta nätverk av belastningsbalanserade, geooptimerade noder för att leverera innehåll så snabbt som möjligt till besökare som finns i hela världen.

Akamai har över 137 000 servrar i 87 länder i över 1 150 nätverk. När det gäller redundans dirigerar CDN inte bara från en server till en annan utan kan även dirigera från en servernod till en annan servernod efter behov. Med andra ord består varje nod av flera servrar, så att en server som går ned aldrig blir ett problem eftersom de andra servrarna på samma nod kan ta över.

Om en hel nod kraschar, kommer Akamai från nästa närmast nod med samma cachelagrade innehåll. Noderna väljs dynamiskt baserat på besökarnas plats, trafikbelastning och andra faktorer så att innehållet hanteras konsekvent från den bästa lokala noden för varje besökare.

Filer som lagras på Akamai har domänen `assets.adobedtm.com`. Detta kan refereras på ett säkert sätt eller inte (`http://` eller `https://`) baserat på hur det anropas i inbäddade `<script>` kod.

>[!WARNING]
>
>Om ditt bibliotek inte är tillgängligt från Akamai-nätverket kan inte Platform förhindra fel som kan uppstå på grund av det.

## Cachelagring av bibliotek

När du använder värdar som hanteras med Adobe cachelagras dina biblioteksbyggen på två platser:

* [Edge-cachning](#edge)
* [Webbläsarcachelagring](#browser)

### Edge-cachning {#edge}

Det främsta syftet med ett CDN är att på ett intelligent sätt distribuera innehåll till servrar som ligger geografiskt närmare slutanvändarna så att innehållet kan hämtas snabbare av klientenheter. CDN:er uppnår detta genom att göra kopior av innehållet tillgängligt på geografiskt spridda servrar runt om i världen (&quot;edge nodes&quot;).

När ditt bygge har distribuerats till värddatorn som hanteras av Adobe distribuerar CDN bygget på flera centraliserade servrar (&quot;original&quot;) som sedan skickar kopior av bygget till många olika edge-noder runt om i världen för cachelagring. De cachelagrade versionerna av bygget som lagras på dessa edge-noder skickas sedan till klientenheterna.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>För värdar som hanteras av Adobe kan det ta upp till fem minuter innan det allra första publicerade biblioteket kan sprida sig till det globala nätverket för CDN.

När en edge-nod tar emot en begäran om en viss fil (till exempel biblioteksbygget) kontrollerar noden först TTL-värdet (time-to-live) för filen. Om TTL-värdet inte har upphört att gälla används den cachelagrade versionen som edge-nod. Om TTL-värdet har gått ut begär edge-noden en ny kopia från närmaste ursprung, visar den uppdaterade kopian och cachelagrar sedan den uppdaterade kopian med en ny TTL.

>[!NOTE]
>
>Förutom cachelagring av edge-noder kan det också finnas mellanliggande nätverk (t.ex. företagsnätverk eller mobila nätverk) som utför sin egen cachelagring. Om dina byggen inte cachelagras som förväntat kan dessa nätverk vara den underliggande orsaken.

#### Invalidering av kantcache {#invalidation}

När du överför en ny biblioteksversion blir cacheminnen på alla relevanta kantnoder ogiltiga. Det innebär att varje nod anser att dess cachelagrade version är ogiltig, oavsett hur nyligen den hämtade en ny kopia. Nästa gång en edge-nod tar emot en begäran för den filen hämtar noden en ny kopia från ursprungsläget.

Eftersom Akamai har flera ursprungliga servrar som replikerar filer mellan varandra, och eftersom det inte finns något sätt att veta vilket ursprung som tog emot filen först, kan dessa nodförfrågningar påverka ett ursprung som inte har den senaste versionen. Den gamla versionen cachelagras sedan igen. För att förhindra detta utförs flera cacheogiltigförklaringar för varje ny version med följande intervall:

* Omedelbart efter överföring
* 5 minuter efter överföring
* 60 minuter efter överföring

Dessa inaktiva cacheminnen gör att de ursprungliga servergrupperna får tid att replikera den senaste versionen av filen mellan sig så att alla får den senaste versionen när filen hämtas.

### Webbläsarcachelagring {#browser}

Biblioteksbyggen cachelagras också i webbläsaren med `cache-control` HTTP-huvud. När du använder värdar som hanteras med Adobe har du inte kontroll över de rubriker som returneras i API-svar, så Adobe används som standard för cachning. Du kan alltså inte använda anpassade rubriker för värdar som hanteras av Adobe. Om du behöver en anpassad `cache-control` header, du kanske vill överväga [värdtjänster](self-hosting-libraries.md) i stället.

TTL-värde (time-to-live) för webbläsarens cachelagrade bibliotek (bestäms av `cache-control` ) varierar beroende på vilken taggmiljö du använder:

| Miljö | `cache-control` value |
| --- | --- |
| Utveckling | `max-age=0, no-cache, no-store` |
| Mellanlagring | `max-age=0, no-cache, no-store` |
| Produktion | `max-age=3600` |

Som framgår av tabellen ovan stöds inte webbläsarcachelagring i utvecklings- och mellanlagringsmiljöer. Därför bör du inte använda utvecklingskoder eller mellanlagringsinbäddningskoder i hög trafik- eller produktionskontext.

Cachekontrollhuvuden används bara för huvudbiblioteksbygget. Alla underresurser under huvudbiblioteket betraktas alltid som nästa och därför behöver de inte cachelagras i webbläsaren.

## Använda värdtjänster som hanteras av Adobe i användargränssnittet för datainsamling

När du först skapar en egenskap i [Användargränssnitt för datainsamling](https://experience.adobe.com/#/data-collection/)skapas en värddator som hanteras av Adobe automatiskt åt dig. Alla tillgängliga miljöer som har omedelbart användbara egenskaper tilldelas som standard till värddatorn som hanteras av Adobe.

>[!NOTE]
>
>Om den Adobe-hanterade standardvärden inte har tilldelats från alla miljöer kan värden tas bort. Om du vill växla tillbaka till en värddator som hanteras av Adobe efter att du har gjort detta kan du skapa en ny värd genom följande steg:
>
>1. Välj **[!UICONTROL Hosts]** -flik i din egenskap och sedan väljer **[!UICONTROL Add Host]**.
>1. Ange ett namn för värden, välj **[!UICONTROL Managed by Adobe]** som värdtyp, välj sedan **[!UICONTROL Save]**.

>
>Du kan sedan tilldela om dina miljöer till den värddator som hanteras av Adobe efter behov.

## Nästa steg

Det här dokumentet innehåller en översikt över värdtjänster som hanteras av Adobe för taggbibliotek i Adobe Experience Platform. Mer information om andra värdalternativ finns i följande dokumentation:

* [SFTP-värdtjänst](./sftp-host.md)
* [Självvärdande bibliotek](./self-hosting-libraries.md)

Mer information om hur du hanterar värdar för dina miljöer finns i [miljöguide](../environments.md).
