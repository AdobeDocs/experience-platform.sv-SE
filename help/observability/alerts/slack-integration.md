---
title: Slack-integrering för kundmotstående varningar
description: Lär dig ansluta Adobe I/O Events till Slack med Adobe App Builder.
source-git-commit: c0fa0320b32e1bfe286d47a2e1af5ea1dcf74cb9
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# Slack-integrering för kundtillvända aviseringar

Med Adobe Experience Platform kan du använda en webkrok-proxy på [Adobe App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app) för att ta emot [Adobe I/O Events](https://developer.adobe.com/events/docs/guides/) i [!DNL Slack]. Proxyn hanterar Adobe handskakning för verifiering och förvandlar händelsenyttolaster till [!DNL Slack] meddelanden så att du kan få kundtillvända aviseringar levererade till din arbetsyta.

## Förhandskrav {#prerequisites}

Innan du börjar bör du kontrollera följande:

* **Adobe Developer Console-åtkomst**: En systemadministratör eller utvecklarroll i en organisation där App Builder är aktiverat.
* **Node.js och npm**: Node.js (LTS rekommenderas), som innehåller npm för installation av Adobe CLI och projektberoenden. Mer information finns i guiden [Ladda ned Node.js](https://nodejs.org/) och [npm Getting Started](https://docs.npmjs.com/getting-started).
* **Adobe I/O CLI**: Installera Adobe I/O CLI från terminalen: `npm install -g @adobe/aio-cli`.
* **Slack-app med inkommande webkrok**: En Slack-app på arbetsytan med en **inkommande Webkrok** aktiverad. Se [Skapa en Slack-app](https://api.slack.com/apps) och guiden [Slack Inkommande webbhooks](https://api.slack.com/messaging/webhooks) för att skapa appen och hämta webkroks-URL:en (format: `https://hooks.slack.com/...`).

## Konfigurera ett mallprojekt {#templated-project}

Om du vill konfigurera ett mallprojekt loggar du in på Adobe Developer Console och väljer sedan **[!UICONTROL Create project from template]** på fliken **[!UICONTROL Home]**.

![Developer Console markerar fliken Hem och skapar projekt från mall.](../images/alerts/slack-integration/developer-console-home.png)

Välj mallen **[!UICONTROL App Builder]**, ange en **[!UICONTROL Project Title]** och välj **[!UICONTROL Add workspace]**. Välj slutligen **[!UICONTROL Save]**.

![Developer Console markerar Project Title, Add Workspace, and Save.](../images/alerts/slack-integration/developer-console-save.png)

Du får en bekräftelse på att ditt projekt har skapats och att det kommer till fliken **[!UICONTROL Project overview]**. Härifrån kan du lägga till en **[!UICONTROL Project description]**.

![Fliken Projektöversikt som visar projektinformation.](../images/alerts/slack-integration/developer-console-project.png)

## Initiera projekt {#initialize-project}

Initiera projektet när du har konfigurerat det mallade projektet.

1. Öppna terminalen och ange följande kommando för att logga in på Adobe I/O.

   ```bash
   aio login
   ```

1. Initiera programmet och ange ett namn.

   ```bash
   aio app init slack-webhook-proxy
   ```

1. Markera `Organization` med piltangenterna och markera sedan `Project` som du skapade tidigare i Developer Console. Välj `Only Templates Supported By My Org` för de mallar som ska sökas igenom.

   ![Terminal som visar val av organisation och projekt och endast mallar som stöds av min organisation.](../images/alerts/slack-integration/terminal-organization-project.png)

1. Tryck sedan på **Enter** för att hoppa över mallar och installera ett fristående program.

   ![Terminal som visar val av organisation och projekt och endast mallar som stöds av min organisation.](../images/alerts/slack-integration/terminal-skip-templates.png)

1. Ange de Adobe I/O App-funktioner som du vill aktivera för det här projektet. Använd piltangenterna för att rulla och välj `Actions: Deploy Runtime actions`.

   ![Terminal som visar appfunktioner med åtgärder: Distribuera körningsåtgärder har valts.](../images/alerts/slack-integration/terminal-app-features.png)

1. Använd piltangenterna för att rulla och välj `Adobe Experience Platform: Realtime Customer Profile` för den typ av exempelåtgärder som du vill skapa.

   ![Terminal som visar exempelåtgärdstyp med Adobe Experience Platform: Kundprofil för realtid vald.](../images/alerts/slack-integration/terminal-sample-actions.png)

1. Rulla och välj `Pure HTML/JS` för det användargränssnitt som du vill lägga till i mallen. Tryck på **Retur** om du vill lämna exempelåtgärderna som standard och tryck sedan på **Retur** igen om du vill lämna namnet som standard.

   ![Terminal som visar gränssnittsval med Ren HTML/JS vald.](../images/alerts/slack-integration/terminal-ui-template.png)

   Du får en bekräftelse på att appinitieringen har slutförts.

1. Navigera till projektkatalogen.

   ```bash
   cd slack-webhook-proxy
   ```

1. Lägg till webbåtgärden.

   ```bash
   aio app add action
   ```

1. Välj `Only Action Templates Supported By My Org`.  En lista med mallar visas.

   ![Terminal som visar listan över åtgärdsmallar.](../images/alerts/slack-integration/terminal-action-templates.png)

1. Välj mallen genom att trycka på blankstegstangenten och navigera sedan till `@adobe/generator-add-publish-events` med hjälp av pilarna **Upp** och **Ned**. Markera slutligen mallen genom att trycka på **blankstegstangenten** och trycka på **Retur**.

   ![Terminal visar mallen.](../images/alerts/slack-integration/terminal-action-select-template.png)

   En bekräftelse på att `npm package @adobe/generator-add-publish-events` har installerats visas.

1. Namnge åtgärden `webhook-proxy`.

   ![Terminal som visar åtgärden webkrok-proxy.](../images/alerts/slack-integration/terminal-add-action-name.png)

   En bekräftelse på att mallen har installerats visas.

## Skapa filåtgärder och distribuera {#create-file-actions}

Lägg till proxykoden, ange miljövariabler och distribuera sedan. Åtgärden blir sedan tillgänglig i Developer Console för registrering.

### Implementera körningsproxyn {#runtime-proxy}

>[!NOTE]
>
>Signaturverifiering och utmaningshantering sker automatiskt när körningsåtgärdsregistrering används.

Navigera till projektmappen och öppna filen `actions/webhook-proxy/index.js`. Ta bort innehållet och ersätt med följande:

```
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("runtime-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Konfigurera åtgärden i app.config.yaml {#app-config}

>[!IMPORTANT]
>
>Åtgärdskonfigurationen i `app.config.yaml` är viktig. Du måste använda `web: no` för att skapa en icke-webbåtgärd som kan registreras som en körningsåtgärd i Developer Console.

Navigera till projektmappen och öppna `app.config.yaml`. Ersätt innehållet med följande:

```
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

### Miljövariabler {#environment-variables}

>[!IMPORTANT]
>
>Programmet körs inte utan en korrekt konfigurerad .env-fil.

Använd systemvariabler om du vill hantera inloggningsuppgifter på ett säkert sätt. Ändra filen `.env` i projektets rot och lägg till:

```
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Distribuera åtgärden {#deploy-action}

Distribuera åtgärden när systemvariablerna har angetts. Kontrollera att du är i roten för projektet (`slack-webhook-proxy`) när du kör det här kommandot i terminalen:

```bash
aio app deploy
```

En bekräftelse på att distributionen lyckades visas.

>[!IMPORTANT]
>
>Din åtgärd distribueras till Adobe I/O Runtime. Nu kan du registrera dig i Developer Console.

## Registrera åtgärden hos Adobe I/O Events {#register-events}

När åtgärden har distribuerats registrerar du den som mål för Adobe I/O Events.

Öppna ditt App Builder-projekt i Developer Console och välj sedan din **[!UICONTROL Workspace]**.

På översiktssidan för Workspace väljer du **[!UICONTROL Add service]** och **[!UICONTROL Event]**.

![Workspace översiktssida markerar Lägg till tjänst och händelse.](../images/alerts/slack-integration/workspace-service-event.png)

På sidan Lägg till händelser väljer du **[!UICONTROL Experience Platform]** och **[!UICONTROL Platform notifications]** och sedan **[!UICONTROL Next]**.

![Sidan Lägg till händelser visar Experience Platform- och plattformsmeddelanden markerade.](../images/alerts/slack-integration/add-events.png)

Markera de händelser som du vill ta emot meddelanden för och välj sedan **[!UICONTROL Next]**.

![Sidan Lägg till händelser som innehåller en lista över händelser som ska prenumereras på.](../images/alerts/slack-integration/select-events.png)

Välj autentiseringsuppgifter för server-till-server och välj sedan **[!UICONTROL Next]**.

![Sidan Lägg till händelser med autentiseringsuppgifter för server-till-server-autentisering.](../images/alerts/slack-integration/add-events-credentials.png)

Ange en **[!UICONTROL Event registration name]** och en **[!UICONTROL Event registration description]** för registreringen och välj sedan **[!UICONTROL Next]**.

![Sidan Lägg till händelser som visar beskrivningsfält för händelseregistreringsnamn och händelseregistrering.](../images/alerts/slack-integration/add-events-registration.png)

Välj **[!UICONTROL Runtime Action]** som leveransmetod och den `slack-webhook-proxy/runtime-proxy`-åtgärd du skapade och välj sedan **[!UICONTROL Save configured events]**.

![Sidan Lägg till händelser visar leveransmetoden för körtidsåtgärd och Spara konfigurerade händelser.](../images/alerts/slack-integration/add-events-runtime.png)

Din webkrok-proxy är nu konfigurerad. Du återgår till webbkroks proxysida. Du kan testa hela flödet från början till slut genom att markera ikonen **[!UICONTROL Send sample event]** bredvid en konfigurerad händelse.

![Webbkrockens proxysida visar konfigurerade händelser och ikonen Skicka exempel på händelse.](../images/alerts/slack-integration/send-sample.png)
