---
title: Privacy Service felkoder i Adobe Experience Platform
description: Förstå Privacy Service felkoder så att du kan diagnostisera fel, hantera jobbresultat programmatiskt och avgöra nästa steg när du skickar eller övervakar sekretessjobb.
keywords: sekretesstjänst, felkoder, sekretessjobb, API-fel
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 2%

---

# Privacy Service-felkoder {#privacy-service-error-codes}

Använd den här referensen för att identifiera Privacy Service jobbresultat, diagnostisera fel och avgöra lämpliga nästa steg när du skickar eller övervakar sekretessjobb i **Adobe Experience Platform**. Mer information om hur du skapar, skickar och övervakar sekretessjobb finns i [slutpunktshandboken för sekretessjobb](./privacy-jobs.md) eller [användarhandboken för Privacy Service UI](../ui/user-guide.md).

Privacy Service felkoder är ett stabilt offentligt kontrakt. Varje felkod identifierar ett feltillstånd eller ett slutförandetillstånd som du kan förlita dig på för programmatisk hantering och operativa arbetsflöden.

Följande garantier gäller vid automatisering och övervakning av arbetsflöden:

* Felkoder är stabila när de har publicerats.
* Felmeddelanden kan ändras för att förbättra klarheten, men kodvärdet gör det inte.
* Nya felkoder kan läggas till över tid. Befintliga koder återanvänds inte.

Använd felkoder, inte meddelandetext, för att implementera automatisering eller beslutslogik. Mer information om hur du effektivt hanterar sekretessjobb, övervakar jobbstatus och hanterar fel utan att förlita dig på avsöknings- eller meddelandesträngar finns i [Privacy Service bästa praxis](../best-practices.md).

## Felsvarsformat {#error-response-format}

Privacy Service returnerar felinformation i jobbet och begär svar. Svaret innehåller en numerisk felkod och ett läsbart meddelande i svarsnyttolasten.

Felkoden anger det officiella resultatet. Meddelandet innehåller ytterligare kontext för felsökning.

I det här dokumentet beskrivs innebörden och avsikten med varje felkod. Information om svarsscheman på fältnivå och förfrågningsinformation finns i [Privacy Service API-dokumentationen](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Feldomäner {#error-domains}

Felkoder grupperas efter funktionell domän för att hjälpa dig att diagnostisera problem snabbare.

Domänerna som används i det här dokumentet är:

* **Begärandevalidering**: Begäran har felaktigt format eller innehåller ogiltiga värden. I [slutpunktshandboken för sekretessjobb](./privacy-jobs.md) finns information om begärandestruktur och valideringskrav.
* **Autentisering och etablering**: Din organisation eller användare saknar nödvändig åtkomst. Se [hantera behörigheter](../permissions.md) för att granska rollbaserade behörighetskrav.
* **Identitet och tillämplighet**: Identifierare eller namnutrymmen kan inte användas för begäran. Mer information om vilka identitetstyper och namnområdeskrav som stöds finns i [identitetsdata för sekretesskrav](../identity-data.md).
* **Hastighetsbegränsning**: Sändningsvolymen överskrider plattformsgränserna. När det här felet inträffar ska du minska överföringshastigheten och försöka igen.
* **Dataåtkomst och databearbetning**: Systemet kan inte komma åt eller bearbeta begärda data. I [felsökningsguiden](../troubleshooting-guide.md) finns vanliga orsaker och reparationssteg.
* **Kryptering och nyckelhantering**: Nödvändiga krypteringsnycklar är inte tillgängliga. Se [Kundhanterade nycklar](../../landing/governance-privacy-security/customer-managed-keys/overview.md) för vägledning om nyckelåtkomst, konfiguration och återställning.
* **Jobbkörningstillstånd**: Jobbet slutfördes helt, delvis eller med fel. I [slutpunktshandboken för sekretessjobb](./privacy-jobs.md#status-categories) finns beskrivningar av jobbstatuskategorier och deras innebörd.

>[!NOTE]
>
>Domäntilldelningar återspeglar felkodens avsikt, inte interna tjänstgränser.

## Felkodreferens {#error-code-reference}

I följande tabell visas alla offentliga felkoder för Privacy Service.

| Felkod | HTTP-status | Titel | Beskrivning |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Formateringsfel | Ett eller flera datavärden för det angivna programmet har formateringsproblem. Mer information finns i jobbinformationen. |
| 1001-400 | 400 | Ej auktoriserad | Din organisation har inte etablerats. Kontakta administratören om du vill ha mer information. |
| 1010-400 | 400 | Behörigheter saknas | Du har inte behörighet att utföra den här åtgärden. Kontakta administratören för att begära åtkomst. |
| 1020-400 | 400 | Överförings- och arkiveringsfel | Ett problem uppstod vid överföring och arkivering av åtkomstdata. Ladda upp åtkomstdata och försök igen. |
| 1021-400 | 400 | Jobbfel | Ett eller flera sekretessjobb som skapats från begäran misslyckades. Mer information finns i informationen om de misslyckade jobben. |
| 1022-400 | 400 | Dataåtkomstfel | Ett problem uppstod vid åtkomst av angivna data. Mer information finns i jobbinformationen. |
| 1023-400 | 400 | Dataåtkomstfel | Ett problem uppstod vid åtkomst till eller sökning efter de angivna datauppsättnings-ID:na. Kontrollera att de angivna ID:n är giltiga och försök sedan igen. |
| 1024-400 | 400 | Oväntat fel | Ett oväntat fel uppstod. Mer information finns i jobbinformationen. |
| 1030-400 | 400 | Gränsen för dokumenthastighet har överskridits | Arbetsbelastningen överskred dokumenthastighetsgränsen. Minska överföringshastigheten och försök igen. |
| 1040-400 | 400 | Åtkomstfel för nyckelkryptering | Det gick inte att bearbeta data eftersom datalagret är krypterat och nyckelåtkomsten återkallades. Kontakta nyckelvalsadministratören om du vill återställa åtkomsten till kundnyckeln. |
| 6000-200 | 200 | Lyckades | Jobbet har slutförts. Granska jobbinformationen för att bekräfta bearbetade poster och resultat. |
| 6051-200 | 200 | Inte etablerat | Din organisation har inte etablerats för det begärda programmet. Begäran är inte tillämplig. |
| 6052-200 | 200 | Användar-ID:n hittades inte | Vissa användar-ID:n hittades inte och okända användar-ID:n kan inte användas för den här produkten. Kontrollera att användar-ID:n är giltiga och försök sedan igen. |
| 6053-200 | 200 | Ogiltigt namnutrymme | Det angivna ID-namnutrymmet är inte giltigt för det här programmet. Använd ett namnutrymme som känns igen av systemet. |
| 6054-200 | 200 | Delvis slutförd | Jobbet slutfördes för tillämpliga data, men vissa data kunde inte tillämpas på begäran. Mer information finns i jobbinformationen. |

{style="table-layout:auto"}
