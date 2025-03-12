---
title: Access AI Assistant i Experience Platform
description: Lär dig hur du får tillgång till AI Assistant i Experience Cloud-gränssnittet.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 9010f430f432c5ead708c1cb01803abd7ffd86b3
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Access AI Assistant i Experience Platform

Du kan öppna AI Assistant i flera program i Adobe Experience Cloud.

>[!IMPORTANT]
>
>Om du får ett popup-meddelande i behörighetsgränssnittet som informerar dig om att din organisation först måste godkänna ytterligare juridiska villkor för att få tillgång till AI Assistant kontaktar du ditt Adobe-kontoteam för vägledning om dessa villkor.

## Kom igång {#get-started}

Du måste slutföra två nödvändiga steg innan du kan komma åt AI-assistenten.

1. Din organisation måste först godkänna de juridiska villkoren. Kontakta Adobe Account Team om du vill ha mer information.
2. Administratörerna måste ge dig behörighet att komma åt AI Assistant.

Om du inte har utfört något av dessa två nödvändiga steg kommer du att se följande meddelanden när du väljer AI Assistant-chattikonen i Experience Platform användargränssnitt.

>[!BEGINTABS]

>[!TAB Din organisation kan inte använda AI Assistant]

Följande meddelande visas om du använder en organisation som inte är juridiskt berättigad att använda AI Assistant. I så fall måste du kontakta ditt Adobe-kontoteam för att lösa problemet med åtkomsten.

![Popup-meddelandet som visas i Experience Platform UI om organisationen inte kan använda AI Assistant.](./images/access/modal-one.png)

>[!TAB Du har inte rätt behörigheter]

Om din organisation har laglig rätt att använda AI Assistant och du fortfarande inte kan komma åt funktionen visas följande meddelande i Experience Platform UI. Detta scenario innebär att du inte har tillräcklig behörighet för att komma åt funktionen och du måste kontakta dina administratörer för att lösa behörigheterna.

![Popup-meddelandet som visas i Experience Platform UI om du inte har de behörigheter som krävs för AI Assistant.](./images/access/modal-two.png)

>[!ENDTABS]

## Få tillgång till AI Assistant

Åtkomst till AI Assistant styrs av följande parametrar:

* **Kom åt programmet:** Du kan komma åt AI Assistant i Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer och [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **Behörigheter:** Använd [Behörighetsgränssnittet](../access-control/abac/ui/permissions.md) för att bevilja eller återkalla åtkomst till AI Assistant i organisationen. För att kunna använda AI Assistant måste en viss användare tillhöra en roll som har etablerats med behörigheterna **Aktivera AI-assistenten** och **Visa driftsinsikter** .
   * Som administratör kan du lägga till **Aktivera AI-assistenten** i en viss roll och lägga till en användare i den rollen, så att de kan komma åt AI-assistenten i organisationen. **Obs!**: Den här behörigheten ger den aktuella användaren åtkomst till AI Assistant, den ger inte användaren någon administrativ kapacitet att ge andra åtkomst till AI Assistant.
   * Som administratör kan du lägga till **Visa driftsinsikter** i en viss roll och lägga till en användare i den rollen, så att de kan använda AI Assistants funktionsinsikter. Driftsinsikter är för närvarande i betaversion.

Använd [behörighetsgränssnittet](../access-control/abac/ui/roles.md) för att bevilja behörigheter att använda AI-assistenten i Experience Platform och Journey Optimizer. Mer information om hur du får tillgång till AI Assistant i Customer Journey Analytics. Läs dokumentationen i [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

![Behörighetsgränssnittssidan med behörigheterna Aktivera AI-assistenten och Visa driftsinsikter i en viss roll.](./images/access/access-permissions.png)

När du har de behörigheter som krävs kan du komma åt AI-assistenten genom att välja AI-assistentikonen i det övre huvudet i programmet som du använder.

![AI-assistenten med förstagångsupplevelse.](./images/access/access-home.png)

Titta på följande video och lär dig hur du konfigurerar åtkomst till AI Assistant för dina organisationer och användare.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## Nästa steg

När du har fullständig åtkomst till AI Assistant kan du fortsätta att använda funktionen under dina arbetsflöden. Mer information finns i [gränssnittsguiden för AI Assistant](./ui-guide.md).
