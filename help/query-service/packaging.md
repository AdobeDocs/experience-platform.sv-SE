---
title: Paketering av frågetjänst
description: I följande dokument beskrivs paketeringen av funktioner och produkter som är tillgängliga för Query Service och skillnaderna mellan ad hoc- och batchfrågor beskrivs.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Paket för frågetjänst

I det här dokumentet beskrivs de olika typerna av paketerings- och frågekörningsfunktioner som finns i Query Service.

Adobe Experience Platform Query Service kan delas upp i två funktioner baserat på de frågemönster som kan köras:

- **Ad hoc-frågor** är SQL-frågor som används för att utforska inkapslade datauppsättningar för verifiering, validering, experimenterande och så vidare. Dessa frågor skriver inte tillbaka data till Experience Platform datasjön.
- **Batchfrågor** är SQL-frågor som används för att bearbeta inkapslade datauppsättningar efter importen. Dessa frågor rensar, formar, manipulerar och berikar data, vars resultat skrivs tillbaka till Experience Platform datasjön. Dessa frågor kan schemaläggas, hanteras och övervakas som batchjobb.

Frågetjänstfunktionerna paketeras med följande produkter och tillägg:

- **Experience Platform-baserade program** (Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten ger åtkomst till att köra ad hoc-frågor från början med alla varianter och skikt av Experience Platform-baserade program.
- **[!DNL Data Distiller]** (tilläggspaket som kan köpas med Adobe Real-Time CDP, Customer Journey Analytics och Adobe Journey Optimizer): Frågetjänsten har åtkomst till att köra gruppfrågor i [!DNL Data Distiller].

## Berättiganden {#entitlements}

Följande tabell visar nyckelfrågetjänstens berättiganden baserat på hur de paketeras:

| Tillstånd för frågetjänst | Paketerat med Experience Platform-baserade program | Packat med [!DNL Data Distiller] |
|---|---|---|
| Frågemönster som stöds | Endast ad hoc-frågor | Batchfråga |
| Användningsfall stöds | <ul><li>&#x200B;</li><li>&#x200B; för dataidentifiering</li><li>Dataverifiering</li><li>Experimentation</li></ul> | <ul><li>Rengöring</li><li>Form</li><li>Manipulera</li><li>Förbättring</li></ul> |
| Semantik som stöds | <ul><li>SELECT-frågor</li></ul> | <ul><li>CTAS- och ITAS-frågor</li></ul> |
| Maximal körningstid | 10 minuter | 24 timmar |
| Licensmått | **Fråga om användarsamtidighet**: <ul><li>1 samtidig användare (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 samtidiga användare (Customer Journey Analytics) &#x200B;</li></ul> **Frågesamtidighet**: <ul><li>1 fråga som körs samtidigt (alla program) &#x200B;</li></ul> **Ytterligare ett tillägg för ad hoc-frågeanvändarpaket** kan köpas för att öka ditt auktoriserade ad ad hoc-frågeberättigande. <ul><li>+5 ytterligare samtidiga användare per paket</li><li>+1 ytterligare fråga som körs samtidigt per paket</li></ul> | **Beräkningstimmar**: <ul><li>Variabel (omfång baserat på ditt programberättigande)</li></ul> **Beräkningstimmar** är ett mått på hur lång tid det tar för fråge-tjänstmotorn att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs. <br>Med Data Distiller SKU får du även ytterligare en samtidighet för användare och frågor, som kan användas för att köra ad hoc-frågor.  Data Distiller SKU innehåller:<br><ul><li>+5 ytterligare samtidiga användare</li><li>+1 ytterligare samtidig fråga</li></ul> |
| Snabbare användning av frågor och rapporter | Nej | Ja - Med samtidiga accelererade frågor kan du läsa data från det accelererade arkivet och visa dem på dina instrumentpaneler. Ett dedikerat berättigande för lagring av rapportmodeller och datauppsättningar i det accelererade arkivet tillhandahålls också. |
| Lagringskapacitet för Data Lake | Ditt totala lagringsberättigande beror på era plattformsbaserade programlicenser. Exempel: Real-Time CDP, AJO, CJA osv. | Ja - Ytterligare ett lagringsberättigande tillhandahålls för att behålla dina råa och härledda datauppsättningar för dataanvändning i Distiller efter ett sju dagars utgångsdatum.<br>Din lagringsutrymme i datasjön mäts i terabyte (TB) och beror på hur många beräkningstimmar du har köpt. Mer information finns i produktbeskrivningen. |
| Dataexportavdrag | Ditt totala exportberättigande beror på era plattformsbaserade programlicenser. Exempel: Real-Time CDP, AJO, CJA osv. | Ja - Ett ytterligare exporttillstånd ges för att tillåta export av härledda datauppsättningar som skapats med Data Distiller.<br>Din årliga dataexportförmån mäts i terabyte (TB) och beror på hur många datortimmar du har köpt. Mer information finns i produktbeskrivningen. |
| Frågekörningsgränssnitt | <ul><li>Användargränssnitt för frågetjänst</li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL]-klientgränssnitt</li></ul> | <ul><li>Användargränssnitt för frågetjänst </li><li>Klientgränssnitt från tredje part</li><li>[!DNL PostgresSQL]-klientgränssnitt</li><li>REST API:er</li></ul> |
| Frågeresultat returnerade via | Klientgränssnitt | Härledd datauppsättning lagrad i datasjön |
| Resultatgräns | <ul><li>Användargränssnitt för frågetjänst - Antalet utdatarader kan [konfigureras med en användargränssnittsinställning ](./ui/user-guide.md#result-count) på mellan 50 och 500 rader.</li><li>Tredjepartsklienter - 50 000</li><li>[!DNL PostgresSQL] klient - 50 000</li></ul> | CTAS- och ITAS-frågor genererar endast slutförda meddelanden eftersom frågans utdata lagras i härledda datauppsättningar. |
| Läs datauppsättningens kapacitet | Ja | Ja |
| Skriva datauppsättningskapacitet | Nej | Ja |
| Planeringskapacitet | Nej | Ja |
| Övervakningskapacitet | Ja | Ja |
| Inställningskapacitet för frågeavisering | Nej | Ja |

{style="table-layout:auto"}

## Åtkomstkontroll {#access-control}

Åtkomstkontroll för Experience Platform administreras via [Adobe Admin Console](https://adminconsole.adobe.com/) där produktprofiler länkar användare med behörigheter och sandlådor. Mer information finns i [åtkomstkontrollsöversikten](../access-control/home.md).

Se [Hantera behörigheter för en produktprofil](../access-control/ui/permissions.md) och [Hantera användare för en produktprofil](../access-control/ui/users.md) -dokument för detaljerade instruktioner om hur du begär åtkomst till produktprofilbehörigheter

### Behörigheter för frågetjänst {#query-service-permissions}

Om du vill använda frågetjänsten måste behörigheten **[!DNL Manage Queries]** aktiveras i Admin Console. Med den här behörigheten kan användare köra ad hoc- och batchfrågor.

Följande tabell visar effekterna av behörigheten [!DNL Manage Queries]:

| Behörighet | Funktion |
|---|---|
| [!DNL Manage Queries] (utan skrivbehörighet) | Ger åtkomst till att köra ad hoc-frågor |
| [!DNL Manage Queries] (med behörighet att skriva data) | Ger åtkomst till att köra batchfrågor |

{style="table-layout:auto"}

### Behörigheter för relevanta SQL-insikter {#sql-insights-permissions}

Om du vill skapa [SQL-insikter](./data-distiller/sql-insights/overview.md) för Data Distiller i kontrollpaneler måste **följande behörigheter** vara aktiverade i Admin Console.

| Behörighet | Funktion |
|---|---|
| [!DNL View Custom Dashboard] | Ger visningsåtkomst till användardefinierade instrumentpaneler |
| [!DNL Manage Custom Dashboard] | Ger åtkomst till användardefinierade instrumentpaneler |

{style="table-layout:auto"}

## Stöd för sandlådor {#sandbox-support}

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje instans av Experience Platform har stöd för flera produktions- och icke-produktionssandlådor, och alla har sina egna bibliotek med Experience Platform-resurser. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka dina produktionssandlådor. Mer information om sandlådor finns i översikten över [sandlådor](../sandboxes/home.md). Alla frågetjänstberättiganden delas över alla sandlådor.

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för de olika paketeringstyper och funktioner för frågekörning som finns i Query Service. Läs [falldokumentationen](./use-cases/abandoned-browse.md) om du vill veta mer om frågetjänsten, t.ex. välkända användningsfall i branschen. Mer allmän information finns i [Översikt över frågetjänsten](./home.md).

