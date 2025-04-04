---
title: Adobe-hanterade värdar - översikt
description: Läs mer om standardvärdalternativet för distribution av kodbiblioteksbyggen i Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 4%

---

# Översikt över värdtjänster som hanteras av Adobe

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Adobe-hanterade värdar är standardvärdinställningen för distribution av dina taggbiblioteksbyggen i Adobe Experience Platform. När du skapar en ny egenskap via användargränssnittet i datainsamlingen skapas en Adobe-hanterad standardvärd åt dig.

Med värdar som hanteras av Adobe levereras biblioteksbyggen till ett tredjepartsnätverk för innehållsleverans (CDN) som Adobe har avtalat med. Dessa CDN:er fungerar oberoende av Adobe, så även när Experience Platform genomgår underhåll eller på annat sätt inte fungerar din driftsatta kod som vanligt på dina webbplatser och i dina program. Inbäddningskoden för en Adobe-hanterad värd refererar till huvudbiblioteksfilen på CDN så att en klientenhet kan hämta filerna vid körning.

I det här dokumentet finns en översikt över Adobe-hanterade värdar i Experience Platform och anvisningar om hur du skapar en ny Adobe-hanterad värd i användargränssnittet.

## Akamai

För närvarande är den primära CDN-providern för Adobe [Akamai](https://www.akamai.com/). Akamai robusta CDN är framtagen för att leverera innehåll till en global, stor publik av webbbesökare. CDN har redundanta nätverk av belastningsbalanserade, geooptimerade noder för att leverera innehåll så snabbt som möjligt till besökare som finns i hela världen.

Akamai har över 137 000 servrar i 87 länder i över 1 150 nätverk. När det gäller redundans dirigerar CDN inte bara från en server till en annan utan kan även dirigera från en servernod till en annan servernod efter behov. Med andra ord består varje nod av flera servrar, så att en server som går ned aldrig blir ett problem eftersom de andra servrarna på samma nod kan ta över.

Om en hel nod kraschar kommer Akamai att användas från nästa närmast nod med samma cachelagrade innehåll. Noderna väljs dynamiskt baserat på besökarnas plats, trafikbelastning och andra faktorer så att innehållet hanteras konsekvent från den bästa lokala noden för varje besökare.

Filer på Akamai har domänen `assets.adobedtm.com`. Detta kan refereras säkert eller inte (`http://` eller `https://`) baserat på hur det anropas i den inbäddade `<script>`-koden.

>[!WARNING]
>
>Om ditt bibliotek inte är tillgängligt från Akamai-nätverket kan Experience Platform inte förhindra fel som kan uppstå på grund av det.

## Cachelagring av bibliotek

När du använder Adobe-hanterade värdar cachelagras dina biblioteksbyggen på två platser:

* [Edge cachning](#edge)
* [Webbläsarcache](#browser)

### Edge cachning {#edge}

Det främsta syftet med ett CDN är att på ett intelligent sätt distribuera innehåll till servrar som ligger geografiskt närmare slutanvändarna så att innehållet kan hämtas snabbare av klientenheter. CDN:er uppnår detta genom att göra kopior av innehållet tillgängligt på geografiskt spridda servrar runt om i världen (&quot;edge nodes&quot;).

När ditt bygge har distribuerats till den Adobe-hanterade värden distribuerar CDN bygget på flera centraliserade servrar (&quot;original&quot;) som sedan skickar kopior av bygget till många olika edge-noder runt om i världen för cachelagring. De cachelagrade versionerna av bygget som lagras på dessa edge-noder skickas sedan till klientenheterna.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>För Adobe-hanterade värdar kan det allra första publicerade biblioteket till vilken ny miljö som helst ta upp till fem minuter att sprida ut sig till det globala nätverket för CDN.

När en edge-nod tar emot en begäran om en viss fil (till exempel ditt bibliotek) kontrollerar noden först filens förfallotid. Om tiden inte har gått ut fungerar edge-noden som den cachelagrade versionen. Om tiden har gått ut begär edge-noden en ny kopia från närmaste ursprung, visar den uppdaterade kopian och cachelagrar sedan den uppdaterade kopian med en ny förfallotid.

>[!NOTE]
>
>Förutom cachelagring av edge-noder kan det också finnas mellanliggande nätverk (t.ex. företagsnätverk eller mobila nätverk) som utför sin egen cachelagring. Om dina byggen inte cachelagras som förväntat kan dessa nätverk vara den underliggande orsaken.

#### Invalidering av Edge-cache {#invalidation}

När du överför en ny biblioteksversion blir cacheminnen på alla tillämpliga kantnoder ogiltiga. Det innebär att varje nod anser att dess cachelagrade version är ogiltig, oavsett hur nyligen den har hämtat en ny kopia. Nästa gång en edge-nod tar emot en begäran för den filen hämtar noden en ny kopia från ursprungsläget.

Eftersom Akamai har flera ursprungliga servrar som replikerar filer mellan varandra, och eftersom det inte finns något sätt att veta vilket ursprung som tog emot filen först, kan dessa nodförfrågningar påverka ett ursprung som inte har den senaste versionen. Den gamla versionen cachelagras sedan igen. För att förhindra detta utförs flera cacheogiltigförklaringar för varje ny version med följande intervall:

* Omedelbart efter överföring
* 5 minuter efter överföring
* 60 minuter efter överföring

Dessa inaktiva cacheminnen gör att de ursprungliga servergrupperna får tid att replikera den senaste versionen av filen mellan sig så att alla får den senaste versionen när filen hämtas.

### Webbläsarcache {#browser}

Biblioteksbyggen cachelagras också i webbläsaren med hjälp av HTTP-huvudet `cache-control`. När du använder Adobe-hanterade värdar har du inte kontroll över de rubriker som returneras i API-svar, så Adobe standardvärde för cachning används. Du kan alltså inte använda anpassade rubriker för värdar som hanteras av Adobe. Om du behöver ett anpassat `cache-control`-huvud kan du överväga [självvärdskap](self-hosting-libraries.md) istället.

Förfallotiden för det cachelagrade biblioteket (som bestäms av rubriken `cache-control`) varierar beroende på vilken taggmiljö du använder:

| Miljö | `cache-control` värde |
| --- | --- |
| Utveckling | `max-age=0, no-cache, no-store` |
| Mellanlagring | `max-age=0, no-cache, no-store` |
| Produktion | `max-age=3600` |

Som framgår av tabellen ovan stöds inte webbläsarcachelagring i utvecklings- och mellanlagringsmiljöer. Därför bör du inte använda utvecklingskoder eller mellanlagringsinbäddningskoder i hög trafik- eller produktionskontext.

Cachekontrollhuvuden används bara för huvudbiblioteksbygget. Alla underresurser under huvudbiblioteket betraktas alltid som nästa och därför behöver de inte cachelagras i webbläsaren.

## Använda värdtjänster som hanteras av Adobe i användargränssnittet

När du först skapar en egenskap i användargränssnittet för Experience Platform eller datainsamlingen skapas en Adobe-hanterad värd automatiskt åt dig. Alla tillgängliga miljöer som har omedelbart användbara egenskaper tilldelas som standard till den Adobe-hanterade värden.

>[!NOTE]
>
>Om standardvärden som hanteras av Adobe inte tilldelas från alla miljöer kan värden tas bort. Om du vill växla tillbaka till en Adobe-hanterad värd efter att du har gjort detta kan du skapa en ny värd genom följande steg:
>
>1. Välj fliken **[!UICONTROL Hosts]** i egenskapen och välj sedan **[!UICONTROL Add Host]**.
>1. Ange ett namn för värden, välj **[!UICONTROL Managed by Adobe]** som värdtyp och välj sedan **[!UICONTROL Save]**.
>
>Du kan sedan tilldela om dina miljöer till den Adobe-hanterade värden efter behov.

## Nästa steg

Det här dokumentet innehåller en översikt över Adobe-hanterade värdtjänster för taggbibliotek i Adobe Experience Platform. Mer information om andra värdalternativ finns i följande dokumentation:

* [SFTP-värdtjänst](./sftp-host.md)
* [Självvärdande bibliotek](./self-hosting-libraries.md)

Mer information om hur du hanterar värdar för dina miljöer finns i [miljöguiden](../environments.md).
