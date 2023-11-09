---
title: Paketering av frågetjänst
description: I följande dokument beskrivs paketeringen av funktioner och produkter som är tillgängliga för Query Service och skillnaderna mellan ad hoc- och batchfrågor beskrivs.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 1%

---

# Paket för frågetjänst

I det här dokumentet beskrivs de olika typerna av paketerings- och frågekörningsfunktioner som finns i Query Service.

Adobe Experience Platform Query Service kan delas upp i två funktioner baserat på de frågemönster som kan köras:

- **Ad hoc-frågor** är SQL-frågor som används för att utforska inkapslade datauppsättningar för verifiering, validering, experimenterande och så vidare. Dessa frågor skriver inte tillbaka data till datasjön för plattformen.
- **Gruppfrågor** är SQL-frågor som används för att utföra efterbearbetningsprocessen för kapslade datauppsättningar. Dessa frågor rensar, formar, manipulerar och berikar data, vars resultat skrivs tillbaka till datasjön för plattformen. Dessa frågor kan schemaläggas, hanteras och övervakas som batchjobb.

Frågetjänstfunktionerna paketeras med följande produkter och tillägg:

- **Plattformsbaserade program** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten ger åtkomst till tillfälliga frågor redan från början med alla varianter och nivåer av plattformsbaserade program.
- **[!DNL Data Distiller]** (tilläggspaket som kan köpas med Adobe Real-Time CDP, Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten har åtkomst till att köra batchfrågor [!DNL Data Distiller].

## Terminologi {#terminology}

I följande avsnitt finns definitioner för nyckeltermer relaterade till paketering av frågetjänsten:

- **Data Lake-lagring**: Datasjön har i första hand följande syften:
   - fungerar som mellanlagringsområde för information om introduktion på Experience Platform,
   - fungerar som långsiktig datalagring för alla data från Experience Platform,
   - Möjliggör användningsfall som dataanalys och datavetenskap.
- **Dataexport**: [datauppsättning](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) typer som du kan exportera beroende på vilket program du använder, produktnivå och vilka tillägg du har köpt. Härledda datauppsättningar kan skapas med tillägget Query Service Data Distiller, och kan [exporterat från Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activation-overview.html) till ett stort antal destinationer, inklusive [molnlagringsdestinationer](/help/destinations/ui/export-datasets.md).
- **Snabbare frågor**: Snabbare frågor returnerar resultat baserat på aggregerade data för att minska väntetiden för resultaten och ge ett mer interaktivt informationsutbyte. Tillståndslösa frågor som skapas i det accelererade arkivet är bara tillgängliga som en del av tillägget Data Distiller.
- **Beräkningstimmar**: Beräkningstimmar är det mått som används för att spåra skanning och skrivning av data med batchfrågor med hjälp av API:t för frågetjänsten. Den beräknas i timmar per år och mäts i alla sandlådor. Antalet beräkningstimmar som din organisation får definieras i avtalsprocessen.

## Berättiganden {#entitlements}

Följande tabell visar nyckelfrågetjänstens berättiganden baserat på hur de paketeras:

| Tillstånd för frågetjänst | Paketerat med plattformsbaserade program | Packat med [!DNL Data Distiller] |
|---|---|---|
| Frågemönster som stöds | Endast ad hoc-frågor | Batchfråga |
| Användningsfall stöds | <ul><li>&#x200B;</li><li>&#x200B; för dataidentifiering</li><li>Dataverifiering</li><li>Experimentation</li></ul> | <ul><li>Rengöring</li><li>Form</li><li>Manipulera</li><li>Förbättring</li></ul> |
| Semantik som stöds | <ul><li>SELECT-frågor</li></ul> | <ul><li>CTAS- och ITAS-frågor</li></ul> |
| Maximal körningstid | 10 minuter | 24 timmar |
| Licensmått | **Fråga om samtidighet för användare**: <ul><li>1 samtidig användare (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 samtidiga användare (Customer Journey Analytics) &#x200B;</li></ul> **Frågesamtidighet**: <ul><li>1 fråga som körs samtidigt (alla program) &#x200B;</li></ul> **Ytterligare tillägg för ad hoc-frågeanvändare** kan köpas för att öka kundernas behörigheter för ad hoc-frågor. <ul><li>+5 ytterligare samtidiga användare per paket</li><li>+1 ytterligare fråga som körs samtidigt per paket</li></ul> | **Beräkna timmar**: <ul><li>Variabel (omfång baserad på kundens ansökningsrättigheter)</li></ul> **Beräkna timmar** är ett mått på hur lång tid det tar för Query Service-motorn att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs. |
| Snabbare användning av frågor och rapporter | Nej | Ja - Med samtidiga accelererade frågor kan du läsa data från det accelererade arkivet och visa dem på dina instrumentpaneler. Ett dedikerat berättigande för lagring av rapportmodeller och datauppsättningar i det accelererade arkivet tillhandahålls också. |
| Lagringskapacitet för Data Lake | Ja - Ditt totala lagringsberättigande beror på era plattformsbaserade programlicenser. Exempel: Real-Time CDP, AJO, CJA och så vidare. | Ja - Ytterligare ett lagringsberättigande tillhandahålls för att behålla dina råa och härledda datauppsättningar för dataanvändning i Distiller efter ett sju dagars utgångsdatum.<br>Din datalagringskapacitet mäts i terabyte (TB) och beror på hur många beräkningstimmar du har köpt. |
| Dataexportavdrag | Ja - Din totala exportbehörighet beror på dina plattformsbaserade programlicenser. Exempel: Real-Time CDP, AJO, CJA och så vidare. | Ja - Ytterligare exporträttigheter tillhandahålls för att tillåta export av härledda datauppsättningar som skapats med Data Distiller.<br>Din årliga dataexportersättning mäts i terabyte (TB) och beror på hur många beräkningstimmar du har köpt. |
| Frågekörningsgränssnitt | <ul><li>Användargränssnitt för frågetjänst</li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL] klientgränssnitt</li></ul> | <ul><li>Användargränssnitt för frågetjänst </li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL] klientgränssnitt</li><li>REST API:er </li></ul> |
| Frågeresultat returnerade via | Klientgränssnitt | Härledd datauppsättning lagrad i datasjön |
| Resultatgräns | <ul><li>Användargränssnitt för frågetjänst - 100 rader</li><li>Tredjepartsklienter - 50 000</li><li>[!DNL PostgresSQL] klient - 50 000</li></ul> | <ul><li>Användargränssnitt för frågetjänst - antalet utdatarader kan vara [konfigurerad med en gränssnittsinställning](./ui/user-guide.md#result-count) till mellan 50 och 500 rader.</li><li>Tredjepartsklienter (ingen övre gräns för rader)</li><li>[!DNL PostgresSQL] klient (ingen övre gräns till rader)</li><li>REST API:er (ingen övre gräns för rader)</li></ul> |
| Läs datauppsättningens kapacitet | Ja | Ja |
| Skriva datauppsättningskapacitet | Nej | Ja |
| Planeringskapacitet | Nej | Ja |
| Övervakningskapacitet | Ja | Ja |
| Inställningskapacitet för frågeavisering | Nej | Ja |

{style="table-layout:auto"}

## Åtkomstkontroll {#access-control}

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com/) där produktprofiler länkar användare med behörigheter och sandlådor. Se [åtkomstkontroll - översikt](../access-control/home.md) för mer information.

Om du vill använda frågetjänsten måste du [!DNL Manage Queries] behörighet måste aktiveras i Admin Console. Med den här behörigheten kan användare köra ad hoc- och batchfrågor. Detaljerade instruktioner för att begära åtkomst till produktprofilen [!DNL Manage Queries] behörighet har angetts i [hantera behörigheter för en produktprofil](../access-control/ui/permissions.md) och [hantera användare för en produktprofil](../access-control/ui/users.md) dokument.

När du har köpt [!DNL Data Distiller] tillägg, [!DNL Write Dataset] tillstånd måste beviljas. Den här behörigheten tillåter [!DNL Data Distiller] användare för att köra gruppfrågor.

I följande tabell visas effekterna av [!DNL Manage Queries] behörighet:

| Behörighet |  -funktion |
|---|---|
| [!DNL Manage Queries] (utan skrivbehörighet) | Ger åtkomst till att köra ad hoc-frågor |
| [!DNL Manage Queries] (med skrivbehörighet) | Ger åtkomst till att köra batchfrågor |

{style="table-layout:auto"}

## Stöd för sandlådor {#sandbox-support}

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje Plattformsinstans har stöd för flera produktions- och icke-produktionssandlådor, och varje instans har ett eget bibliotek med plattformsresurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka dina produktionssandlådor. Mer information om sandlådor finns i [översikt över sandlådor](../sandboxes/home.md). Alla frågetjänstberättiganden delas över alla sandlådor.

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för de olika paketeringstyper och funktioner för frågekörning som finns i Query Service. Läs mer om frågetjänsten, t.ex. välkända användningsfall i branschen, i [falldokumentation](./use-cases/abandoned-browse.md). Mer allmän information finns på [Översikt över frågetjänsten](./home.md).
