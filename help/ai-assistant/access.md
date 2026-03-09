---
title: Access AI Assistant (äldre) i Experience Platform
description: Lär dig hur du får tillgång till AI Assistant i Experience Cloud-gränssnittet.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# Access AI Assistant (äldre) i Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet gäller för AI Assistant (äldre). Mer information om AI Assistant (Next-Gen) finns i [gränssnittsguiden för AI-assistenten](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) i [AI-dokumentationen i Experience Cloud](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/home).

I följande tabell finns en jämförelse mellan AI Assistant (äldre) och AI Assistant (nästa generation):

| Funktionsområde | AI Assistant (äldre) | AI Assistant (nästa generation) |
| --- | --- | --- |
| Användarupplevelse | AI Assistant (äldre) är endast tillgängligt på en panel på den högra listen. | AI Assistant (Next-Gen) finns både på den högra panelen och i en engagerande helskärmsupplevelse. |
| Funktionens omfattning | Du kan använda AI Assistant (äldre) för både produktkunskap och driftsinsikter. | Du kan använda AI Assistant (Next-Gen) för produktkunskap, driftsinsikter samt avancerade agetiska färdigheter och körning av uppgifter i flera steg. |
| Plattformsarkitektur | AI Assistant (äldre) är inte byggt på Agent Orchestrator-stacken. | AI Assistant (Next-Gen) drivs av [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) vilket möjliggör utbyggbarhet och avancerad samordning mellan funktioner. |
| Programtäckning | AI Assistant (äldre) är en programspecifik implementering. | Du kan använda AI Assistant (Next-Gen) för en enhetlig AI Assistant-upplevelse i alla Adobe Experience Cloud-program. |
| Åtkomst och behörighetsmodell | Åtkomstmodell som omfattas av programmet och som anpassas efter enskilda produktgränser. | Alla användare har tillgång till AI Assistant (Next-Gen) och tillhörande Experience Platform-agenter. **Obs!**: <ul><li>**Adobe Experience Manager**: Din administratör måste ge dig behörighet att komma åt AI Assistant (Next-Gen) via [Adobe Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics**: Din administratör måste ge dig behörighet att komma åt AI Assistant via [Customer Journey Analytics Access Control](https://experienceleague.adobe.com/en/docs/analytics-platform/using/technotes/access-control?lang=en). På så sätt kan du ställa frågor om produktkunskap och datainsikter. |

Du kan öppna AI Assistant (äldre) i flera program i Adobe Experience Cloud.

>[!NOTE]
>
>Om du får ett popup-meddelande i behörighetsgränssnittet som informerar dig om att din organisation först måste godkänna ytterligare juridiska villkor för att få tillgång till AI Assistant (äldre) kontaktar du ditt Adobe-kontoteam för vägledning om dessa villkor.

## Kom igång {#get-started}

Du måste slutföra två nödvändiga steg innan du kan komma åt AI Assistant (äldre).

1. Din organisation måste först godkänna de juridiska villkoren. Kontakta Adobe Account Team om du vill ha mer information.
2. Administratörerna måste ge dig behörighet att komma åt AI Assistant (äldre).

Om du inte har utfört något av dessa två nödvändiga steg kommer du att se följande meddelanden när du väljer ikonen för AI-assistenten (äldre) i Experience Platform användargränssnitt.

>[!BEGINTABS]

>[!TAB Din organisation kan inte använda AI Assistant (äldre)]

Följande meddelande visas om du använder en organisation som inte är juridiskt berättigad att använda AI Assistant (äldre). I så fall måste du kontakta ditt Adobe-kontoteam för att lösa problemet med åtkomsten.

![Popup-meddelandet som visas i Experience Platform UI om organisationen inte kan använda AI Assistant (äldre).](./images/access/modal-one.png)

>[!TAB Du har inte rätt behörigheter]

Om din organisation har laglig rätt att använda AI Assistant (äldre) och du fortfarande inte kan komma åt funktionen visas följande meddelande i Experience Platform UI. Detta scenario innebär att du inte har tillräcklig behörighet för att komma åt funktionen och du måste kontakta dina administratörer för att lösa behörigheterna.

![Popup-meddelandet som visas i Experience Platform-gränssnittet om du inte har de behörigheter som krävs för AI Assistant (äldre).](./images/access/modal-two.png)

>[!ENDTABS]

## Få tillgång till AI Assistant (äldre) {#get-access-to-ai-assistant}

Åtkomst till AI Assistant (äldre) styrs av följande parametrar:

* **Åtkomst till programmet:** Du kan komma åt AI Assistant (äldre) i Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer och [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **Behörigheter:** Använd [Behörighetsgränssnittet](../access-control/abac/ui/permissions.md) för att bevilja eller återkalla åtkomst till AI Assistant (äldre) i organisationen. För att kunna använda AI Assistant (äldre) måste en viss användare tillhöra en roll som har etablerats med behörigheterna **Aktivera AI-assistenten** och **Visa driftsinsikter** .
   * Som administratör kan du lägga till **Aktivera AI-assistenten** i en viss roll och lägga till en användare i den rollen, så att de kan komma åt AI-assistenten (äldre) i organisationen. **Obs!**: Den här behörigheten ger användaren åtkomst till AI Assistant (äldre), den ger inte användaren någon administrativ kapacitet att ge andra åtkomst till AI Assistant (äldre).
   * Som administratör kan du lägga till **Visa driftsinsikter** i en viss roll och lägga till en användare i den rollen, så att de kan använda AI Assistant (äldre)-funktioner.

Använd [behörighetsgränssnittet](../access-control/abac/ui/roles.md) för att bevilja behörigheter att använda AI Assistant (äldre) i Experience Platform och Journey Optimizer. Mer information om hur du kommer åt AI Assistant (äldre) i Customer Journey Analytics. Läs dokumentationen i [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

![Behörighetsgränssnittssidan med behörigheterna Aktivera AI-assistenten (äldre) och Visa Operational Insights i en viss roll.](./images/access/access-permissions.png)

När du har fått de behörigheter som krävs kan du komma åt AI Assistant (äldre) genom att välja AI Assistant (äldre)-ikonen i det övre huvudet i programmet som du använder.

![AI Assistant (äldre) med förstagångsupplevelse.](./images/access/access-home.png)

Titta på följande video och lär dig hur du konfigurerar åtkomst till AI Assistant (äldre) för organisationer och användare.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Nästa steg

När du har fullständig åtkomst till AI Assistant (äldre) kan du fortsätta att använda funktionen under dina arbetsflöden. Mer information finns i [AI Assistant (äldre)-gränssnittshandboken](./ui-guide.md).
