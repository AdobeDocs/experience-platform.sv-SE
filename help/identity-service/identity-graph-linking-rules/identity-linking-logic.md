---
title: Länkningslogik för identitetstjänst
description: Läs om hur identitetstjänsten länkar olika identiteter för att skapa en heltäckande bild av en kund.
hide: true
hidefromtoc: true
badge: Alfa
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 2%

---

# Länkningslogik för identitetstjänst

>[!IMPORTANT]
>
>Länkningsregler för identitetsdiagram finns för närvarande i Alpha. Funktionen och dokumentationen kan komma att ändras.

En länk mellan två identiteter skapas när identitetsnamnutrymmet och identitetsvärdena matchar.

Det finns två typer av identiteter som länkas:

* **Profilposter**: Dessa identiteter kommer vanligtvis från CRM-system.
* **Experience Events**: Dessa identiteter kommer vanligtvis från WebSDK-implementering eller Adobe Analytics-källan.

## Länkningslogik för identitetstjänsten

En identitet består av ett identitetsnamnutrymme och ett identitetsvärde.

* Ett identitetsnamnutrymme är kontexten för ett givet identitetsvärde. Vanliga exempel på identitetsnamnutrymmen är CRM-ID, E-post och Telefon.
* Ett identitetsvärde är den sträng som representerar en faktisk enhet. Till exempel: &quot;julien<span>@acme.com kan vara ett identitetsvärde för ett e-postnamnutrymme och 555-555-1234 kan vara ett motsvarande identitetsvärde för ett Phone-namnområde.

>[!TIP]
>
>Identitetsnamnutrymmet är viktigt eftersom identitetsvärdet förlorar sitt sammanhang och inte har tillräckligt med information för att matcha identiteter.

Se följande diagram för en visuell representation av hur länkningslogiken i identitetstjänsten fungerar:

>[!BEGINTABS]

>[!TAB Befintligt diagram]

Anta att du har ett befintligt identitetsdiagram med tre länkade identiteter:

* PHONE:(555)-555-1234
* EMAIL:julien<span>@acme.com
* CRM-ID:60013ABC

![befintligt diagram](../images/identity-settings/existing-graph.png)

>[!TAB Inkommande data]

Ett par identiteter är inkapslade i diagrammet och det här paret innehåller:

* CRM-ID:60013ABC
* ECID:100066526

![inkommande data](../images/identity-settings/incoming-data.png)

>[!TAB Uppdaterat diagram]

Identitetstjänsten känner igen att CRM ID:60013ABC redan finns i diagrammet och länkar därför bara det nya ECID:t

![uppdaterat diagram](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Kundscenario

Du är datatekniker och du importerar följande CRM-datauppsättning (profilpost) till Experience Platform.

| CRM-ID** | Telefon* | E-post* | Förnamn | Efternamn |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Anger fält som har markerats som primär identitet.
>* `*` - Anger fält som har markerats som sekundär identitet.
>
>Identitetstjänsten skiljer inte mellan primär och sekundär identitet. Så länge ett fält är markerat som en identitet, hämtas det till identitetstjänsten.

Du har också implementerat WebSDK och importerat en WebSDK-datauppsättning (Experience Event) med följande datatabeller:

| Tidsstämpel | Identiteter i evenemanget* | Händelse |
| --- | --- | --- |
| `t=1` | ECID:38652 | Visa hemsida |
| `t=2` | ECID:38652, CRM ID:31260XYZ | Sök efter skor |
| `t=3` | ECID:44675 | Visa hemsida |
| `t=4` | ECID:44675, CRM ID: 31260XYZ | Visa köphistorik |

>[!NOTE]
>
>* `*` - Anger fält som är markerade som identiteter, där ECID är markerat som primärt.
>* Som standard anges personidentifieraren (i det här fallet CRM-ID) som primär identitet. Om personidentifieraren inte finns blir cookie-identifieraren (i det här fallet ECID) den primära identiteten.

I detta exempel:

* `t=1`, använde en stationär dator (ECID:38652) och för att visa hemsidan anonymt.
* `t=2`, använde samma stationära dator, loggade in (CRM ID:31260XYZ) och sökte sedan efter skor.
   * När en användare är inloggad skickar händelsen både ECID och CRM ID till identitetstjänsten.
* `t=3`, använde en bärbar dator (ECID:44675) och bläddrade anonymt.
* `t=4`, använde samma bärbara dator, loggade in (CRM ID: 31260XYZ) och visade sedan inköpshistoriken.


>[!BEGINTABS]

>[!TAB timestamp=0]

At `timestamp=0`har du två identitetsdiagram för två olika kunder. Båda representeras av tre länkade identiteter.

| | CRM-ID | E-post | Telefon |
| --- | --- | --- | --- |
| Kund en | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Kund två | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

At `timestamp=1`, en kund använder en bärbar dator för att besöka din e-handelswebbplats, visa din hemsida och surfa anonymt. Den här anonyma surfhändelsen identifieras som ECID:38652. Eftersom identitetstjänsten bara lagrar händelser med minst två identiteter lagras inte den här informationen.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

At `timestamp=2`, en kund använder samma bärbara dator för att besöka din e-handelswebbplats. De loggar in med kombinationen av användarnamn och lösenord och bläddrar efter skor. Identitetstjänsten identifierar kundens konto när de loggar in eftersom det motsvarar deras CRM-ID: 31260XYZ. Dessutom relaterar identitetstjänsten ECID:38562 till CRM ID:31260XYZ eftersom båda använder samma webbläsare på samma enhet.

![tidsstämpel-två](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

At `timestamp=3` en kund använder en surfplatta för att besöka din e-handelswebbplats och surfa anonymt. Den här anonyma surfhändelsen identifieras som ECID:44675. Eftersom identitetstjänsten bara lagrar händelser med minst två identiteter lagras inte den här informationen.

![timestamp-three](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

At `timestamp=4`, en kund använder samma surfplatta, loggar in på sitt konto (CRM-ID:31260XYZ) och visar sin inköpshistorik. Den här händelsen länkar deras CRM-ID:31260XYZ till cookie-identifieraren som tilldelats anonym surfaktivitet, ECID:44675, och länkar ECID:44675 till kundens identitetsdiagram.

![tidsstämpel-fyra](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md)
* [Identitetstjänst och kundprofil i realtid](identity-and-profile.md)
