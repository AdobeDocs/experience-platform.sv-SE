---
solution: Experience Platform
title: Navigera till Använd fallspelningsböcker
description: Lär dig navigera i ett galleri med spelböcker och komma igång med en inspirerande sandlåda.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Navigera till Använd fallspelningsböcker

Använd fallspelsböcker är tillgängliga utan extra kostnad för alla Adobe Experience Platform-kunder. Om du vill få tillgång till ett omfattande galleri med fallspelningsböcker i Experience Platform-gränssnittet väljer du **[!UICONTROL Playbooks]** i den vänstra navigeringen.

![Använd galleri för fallspelningsböcker.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Direktåtkomst för att använda fallspelningsböcker i det vänstra navigeringsfältet.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Välj en spelningsbok som du vill gå till informationssidan och välj sedan **[!UICONTROL Go to an inspirational sandbox]**. En bekräftelse visas. Välj **Bekräfta** om du vill gå till den inspirerande sandlådan där du kan utforska och experimentera med olika användningsfall.

Om du inte har behörighet att skapa sandlådor kontaktar du administratören för att få hjälp med att skapa en inspirerande sandlåda.

>[!TIP]
>
>En inspirerande sandlåda är en utvecklingssandlåda i Adobe Experience Platform där du kan skapa, testa och experimentera med olika användningsfall innan du implementerar dem i en liveproduktionsmiljö.

![Gå till inspirerande sandlåda.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Om du inte redan har konfigurerat några inspirerande sandlådor väljer du **[!UICONTROL Create an inspirational Sandbox]**. En modal visas. Ange **Namn** och **Titel** i de obligatoriska fältrutorna och välj **Skapa**. När du har skapat den inspirerande sandlådan ska du [definiera behörigheter](/help/access-control/home.md) innan du går tillbaka till informationssidan för användningsfallspelningsböcker för att skapa en instans.

![Skapa en inspirerande sandlåda.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Ange namn och titel för att skapa en inspirerande sandlåda.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Om du väljer en fallspelningsbok utanför en inspirerande sandlåda kan du inte skapa en instans. På informationssidan väljer du **Gå till inspirerande sandlåda** för att gå till en befintlig inspirerande sandlåda och sedan **[!UICONTROL Create instance]**.

Om du inte har behörighet att skapa sandlådor kontaktar du administratören för att få hjälp med att skapa en inspirerande sandlåda.

![Inga behörigheter att skapa sandlådan.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Om du har nått gränsen för hur många sandlådor som har tilldelats dig visas ett meddelande där du ombeds kontakta organisationens administratör för att öka gränsen eller inaktivera eller ta bort några aktiva sandlådor. När din sandlådegräns har justerats eller antalet aktiva sandlådor har reducerats kan du fortsätta att skapa den inspirerande sandlådan.

![Sandlådegränsen har nåtts.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Observera att kanalytor för e-post, push och SMS-meddelanden inte skapas automatiskt när du skapar en inspirerande sandlåda. Kontakta din IT-administratör för att konfigurera dem manuellt, annars kan det hända att instansen inte kan skapas.

![Konfigurera kanalförinställningar.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Konfigurera sandbox- och kanalytor i Journey Optimizer {#configure-channel-surfaces}

Om din organisation har licens för [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) och du vill använda de spelböcker som är utformade för Journey Optimizer, måste du konfigurera kanalförinställningarna i sandlådan, som definierar de tekniska parametrar som krävs för dina meddelanden. [Lär dig hur du ställer in kanalytor i Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Om du vill skapa instanser av spelböcker i Journey Optimizer måste du konfigurera kanalytor för e-post-, push- och SMS-meddelanden.

### E-postkanalens yta

Gå till `Channels` i Journey Optimizer-gränssnittet. Konfigurera separata underdomäner och IP-pooler för marknadsföringsmeddelanden och transaktionsmeddelanden, om de inte redan har konfigurerats. Det här är de bästa sätten att se till att transaktionsmeddelanden, som e-postmeddelanden med orderbekräftelse, når fram till dina kunder. Ange namn, e-postadresser och andra inställningar. Välj **Skicka** längst upp till höger på sidan för att skapa marknadskanalsytan. Läs dokumentationen om [hur du konfigurerar e-postkanalsytor](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-kanalsyta

Om du vill skapa en SMS-kanalyta skapar du först en SMS API-autentiseringsuppgift och väljer önskad leverantör (till exempel Sinch). Ge SMS-kanalen ett namn (till exempel SMS Marketing), markera konfigurationen och ange ett avsändarnummer. Välj **Skicka** längst upp till höger på sidan om du vill spara SMS-kanalens yta. Läs dokumentationen om [hur du konfigurerar SMS-kanalsytor](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=en#message-preset-sms).

Konfigurera även kanaler för spelböcker som innehåller transaktionsmeddelanden som orderbekräftelser.

### Tryck kanalyta

Bekräfta att kanalkonfigurationerna har konfigurerats antingen från Experience Platform eller datainsamlingsgränssnittet. Så här ser kanalkonfigurationer ut i datainsamlingsmiljön.

## Nästa steg {#next-steps}

Nu när du har läst det här dokumentet bör du känna till hur du konfigurerar en inspirerande sandlåda och känna till olika sätt att få tillgång till fallspelsböcker i Experience Platform. Som ett nästa steg kan du läsa om hur du [väljer](/help/use-case-playbooks/playbooks/choose.md) rätt spelbok.
