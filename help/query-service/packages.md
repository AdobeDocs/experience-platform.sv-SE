---
title: Frågetjänstpaket
description: I följande dokument beskrivs vilka funktioner och produkter som är tillgängliga för frågetjänsten och skillnaderna mellan ad hoc- och batchfrågor är markerade.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 2%

---

# Frågetjänstpaket

I det här dokumentet beskrivs de olika typerna av paketerings- och frågekörningsfunktioner som finns i Query Service.

Adobe Experience Platform Query Service kan delas upp i två funktioner baserat på de frågemönster som kan köras:

- **Ad hoc-frågor** är SQL-frågor som används för att utforska inkapslade datauppsättningar för verifiering, validering, experimenterande och så vidare. Dessa frågor skriver inte tillbaka data till datasjön för plattformen.
- **Gruppfrågor** är SQL-frågor som används för att utföra efterbearbetningsprocessen för kapslade datauppsättningar. Dessa frågor rensar, formar, manipulerar och berikar data, vars resultat skrivs tillbaka till datasjön för plattformen. Dessa frågor kan schemaläggas, hanteras och övervakas som batchjobb.

Frågetjänstfunktionerna paketeras med följande produkter och tillägg:

- **Plattformsbaserade program** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten ger möjlighet att köra ad hoc-frågor redan från början med alla varianter och nivåer av plattformsbaserade program.
- **[!DNL Data Distiller]** (tilläggspaket som kan köpas med Adobe Real-Time CDP, Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten har åtkomst till att köra batchfrågor [!DNL Data Distiller].

Följande tabell visar nyckelfrågetjänstens berättiganden baserat på hur de paketeras:

| Tillstånd för frågetjänst | Paketerat med plattformsbaserade program | Packat med [!DNL Data Distiller] |
|---|---|---|
| Frågemönster som stöds | Endast Ad hoc-fråga | Batchfråga |
| Användningsfall som stöds | <ul><li>&#x200B;</li><li>&#x200B;</li><li>Dataverifiering</li><li>Experimentation</li></ul> | <ul><li>Rengöring</li><li>Form</li><li>Manipulera</li><li>Bättre</li></ul> |
| Semantik som stöds | <ul><li>SELECT-frågor</li></ul> | <ul><li>CTAS- och ITAS-frågor</li></ul> |
| Maximal körningstid | 10 minuter | 24 timmar |
| Licensmått | **Fråga om samtidighet för användare**: <ul><li>1 samtidig användare (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 samtidiga användare (Customer Journey Analytics) &#x200B;</li></ul> **Frågesamtidighet**: <ul><li>1 fråga som körs samtidigt (alla program) &#x200B;</li></ul> **Ytterligare tillägg för ad hoc-frågeanvändare** kan köpas för att öka kundernas behörigheter för ad hoc-frågor. <ul><li>+5 ytterligare samtidiga användare per paket</li><li>+1 ytterligare fråga som körs samtidigt per paket</li></ul> | **Beräkna timmar**: <ul><li>Variabel (omfång baserad på kundens ansökningsrättigheter)</li></ul> **Beräkna timmar** är ett mått på hur lång tid det tar för Query Service-motorn att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs. |
| Frågekörningsgränssnitt | <ul><li>Användargränssnitt för frågetjänst</li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL] klientgränssnitt</li></ul> | <ul><li>Frågegränssnitt </li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL] klientgränssnitt</li><li>REST API:er </li></ul> |
| Frågeresultat returnerade via | Klientgränssnitt | Härledd datauppsättning lagrad i datasjön |
| Resultatgräns | <ul><li>Frågegränssnitt - 100 rader</li><li>Tredjepartsklient - 50 000</li><li>[!DNL PostgresSQL] klient - 50 000</li></ul> | <ul><li>Frågegränssnitt (ingen övre gräns till rader)</li><li>Tredjepartsklienter (ingen övre gräns för rader)</li><li>[!DNL PostgresSQL] klient (ingen övre gräns till rader)</li><li>REST API:er (ingen övre gräns för rader)</li></ul> |
| Läs datauppsättningens kapacitet | Ja | Ja |
| Skriva datauppsättningskapacitet | Nej | Ja |
| Planeringskapacitet | Nej | Ja |
| Övervakningskapacitet | Ja | Ja |
| Inställningskapacitet för frågeavisering | Nej | Ja |

{style="table-layout:auto"}

## Åtkomstkontroll

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com/) där produktprofiler länkar användare med behörigheter och sandlådor. Se [åtkomstkontroll - översikt](../access-control/home.md) för mer information.

Om du vill använda frågetjänsten måste du [!DNL Manage Queries] behörighet måste aktiveras i Admin Console. Med den här behörigheten kan användare köra ad hoc- och batchfrågor. Detaljerade instruktioner för att begära åtkomst till produktprofilen [!DNL Manage Queries] behörighet har angetts i [hantera behörigheter för en produktprofil](../access-control/ui/permissions.md) och [hantera användare för en produktprofil](../access-control/ui/users.md) dokument.

När du har köpt [!DNL Data Distiller] tillägg, [!DNL Write Dataset] tillstånd måste beviljas. Den här behörigheten tillåter [!DNL Data Distiller] användare för att köra gruppfrågor.

Följande tabell visar effekterna av [!DNL Manage Queries] behörighet:

| Behörighet |  -funktion |
|---|---|
| [!DNL Manage Queries] (utan behörighet att skriva data) | Ger åtkomst till att köra ad hoc-frågor |
| [!DNL Manage Queries] (med behörighet att skriva data) | Ger åtkomst till att köra batchfrågor |

{style="table-layout:auto"}

## Stöd för sandlådor

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje Platform-instans har stöd för flera produktions- och icke-produktionssandlådor, och alla har sitt eget bibliotek med plattformsresurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka dina produktionssandlådor. Mer information om sandlådor finns i [översikt över sandlådor](../sandboxes/home.md). Alla frågetjänstberättiganden delas över alla sandlådor

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för de olika paketeringstyper och funktioner för frågekörning som finns i Query Service. Läs mer om frågetjänsten, t.ex. välkända användningsfall i branschen, i [falldokumentation](./use-cases/abandoned-browse.md). Mer allmän information finns på [Översikt över frågetjänsten](./home.md).
