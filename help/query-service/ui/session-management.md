---
title: Hantera frågetjänstsessioner i Adobe Experience Platform
description: Läs om hur administratörer kan visa, övervaka och avsluta aktiva Query Service-sessioner för att frigöra ledig kapacitet och upprätthålla tillförlitliga arbetsflöden för Data Distiller.
keywords: Experience Platform;Query Service;sessioner;sessionshantering;Data Distiller;admin
solution: Experience Platform
source-git-commit: 1d2a8ef649c4454da7cf0949192b8b1eb3696e5a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Hantera sessioner med frågetjänsten

Använd den här vägledningen när du vill hantera aktiva Query Service-sessioner från Adobe Experience Platform användargränssnitt. Sessionshantering hjälper administratörer att övervaka samtidiga frågeredigeringssessioner över sandlådor och frigöra kapacitet när användare lämnar sessioner öppna.

## Behörigheter krävs för sessionshantering {#permissions}

>[!AVAILABILITY]
>
>Sessionshantering är endast tillgänglig för organisationer med Data Distiller-berättiganden.

>[!IMPORTANT]
>
>Den här funktionen är avsedd för administratörer. Slutanvändare som kör frågor kan inte hantera sessioner.

Om du vill visa och avsluta sessioner måste du tillhöra en organisation med åtkomst till Data Distiller och ha behörigheten **[!UICONTROL Manage Query Session]** tilldelad. Användare utan nödvändig behörighet kan komma åt frågetjänsten men kan inte visa eller hantera aktiva sessioner.

## Visa aktiva sessioner {#view-active-sessions}

Administratörer kan visa alla aktiva frågetjänstsessioner över sandlådor i organisationen. I Experience Platform väljer du **[!UICONTROL Queries]** i den vänstra navigeringen för att öppna arbetsytan för frågetjänsten och sedan fliken **[!UICONTROL Admin]** för att få åtkomst till sessionshanteringen.

![Arbetsytan för frågetjänsten med fliken Admin vald. Registret Sessionshantering visas och visar aktiva och inaktiva sessioner över flera sandlådor i organisationen.](../images/ui/session-management/session-management-admin-tab.png)

Sessionshanteringstabellen uppdateras automatiskt i realtid och visar alla sessioner som för närvarande förbrukar samtidigt med frågetjänstens sessionskapacitet som tilldelats din organisation. Varje rad representerar en session som öppnas i Frågeredigeraren.

## Sessionsstatus och inaktiv tid {#session-status}

Sessionstabellen innehåller information som hjälper dig att avgöra om en session kan avslutas på ett säkert sätt.

| Kolumn | Beskrivning |
| --- | --- |
| Användar-ID | Adobe ID för den användare som äger sessionen |
| Användarnamn | Namnet som är associerat med Adobe ID |
| Sandbox | Anger sandlådan där sessionen körs |
| Sessionsstatus | Visar om sessionen är **[!UICONTROL Active]** eller **[!UICONTROL Inactive]** |
| Inaktivitetstid | Visar hur länge sessionen har öppnats utan interaktion |
| Återstående sessionstid | Anger hur länge sessionen kan vara öppen innan den automatiskt går ut |

### Sessionsstatus

**[!UICONTROL Inactive]** anger att användaren inte aktivt kör en fråga. Dessa sessioner kan avslutas. **[!UICONTROL Active]** anger att en fråga körs. Kontrollen **[!UICONTROL End session]** är inte tillgänglig förrän frågekörningen har slutförts.

### Inaktivitetstid och återstående sessionstid

Väntetiden visar hur länge en session har öppnats utan användarinteraktion. Återstående sessionstid anger hur länge sessionen kan vara öppen innan den stängs automatiskt av systemet. Sessionerna förfaller automatiskt efter den maximala tillåtna tidsperioden (två timmars inaktivitet). Varaktigheten är systemdefinierad och kan inte konfigureras.

## Avsluta inaktiva sessioner {#end-idle-sessions}

Du kan avsluta inaktiva sessioner för att frigöra kapacitet för samtidiga sessioner för andra användare. Överväg att avsluta sessioner med hög väntetid när användarna inte längre arbetar aktivt.

I sessionshanteringstabellen väljer du **[!UICONTROL End session]** för att välja den inaktiva session som du vill avsluta.

![Sessionshanteringstabellen visar en inaktiv session med End session markerat.](../images/ui/session-management/end-session.png)

En bekräftelsedialogruta visas för att förhindra oavsiktlig avslutning. Bekräfta åtgärden genom att välja **[!UICONTROL End session]** i dialogrutan.

![Bekräftelsedialogrutan för slutsessionen med ett varningsmeddelande och slutsessionen markerat.](../images/ui/session-management/end-session-confirmation-dialog.png)

När sessionen är slut tas sessionen bort från tabellen, kapaciteten blir omedelbart tillgänglig och åtgärden registreras för granskning.

>[!NOTE]
>
>Sessioner med statusen **[!UICONTROL Active]** kan inte avslutas. Detta skydd förhindrar avbrott i pågående arbetsbelastningar.

## Sessionsbeteende efter avslutning {#session-behavior-after-termination}

När en administratör avslutar en session finns den berörda användarens kod kvar i redigeraren utan att förlora något arbete. Om användaren försöker köra en fråga efter avslutad session, upptäcker systemet den avslutade sessionen, återupprättar anslutningen automatiskt och håller innehållet i Frågeredigeraren intakt.

Det här beteendet säkerställer att användarna inte förlorar arbete som skrivits i redigeraren och kan fortsätta när en ny session har etablerats.

## Granskningsloggar för sessionshantering {#audit-logs}

Systemet loggar sessionshanteringsåtgärder för att ge synlighet och ansvar. Granskningsloggar registrerar sessions-ID, den användare vars session avslutades, den administratör som utförde åtgärden samt tidpunkten för åtgärden.

Använd granskningsloggar för att granska sessionens avslutningshistorik och undersöka oväntade frånkopplingar.

Mer information om hur du visar granskningsloggar finns i [Handboken för frågetjänstens granskningslogg](../data-governance/audit-log-guide.md).

## Nästa steg {#next-steps}

Använd följande resurser för att utöka din användning av Query Service och Data Distiller:

* [Lär dig hur användare skapar och kör frågor i användarhandboken för Frågeredigeraren](user-guide.md)
* [Övervaka schemalagda arbetsbelastningar med hjälp av dokumentation för övervakning av schemalagda frågor](monitor-queries.md)

