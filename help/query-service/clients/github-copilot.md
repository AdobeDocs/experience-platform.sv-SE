---
title: Anslut GitHub Copilot och Visual Studio Code till Query Service
description: Lär dig hur du ansluter GitHub Copilot och Visual Studio Code med Adobe Experience Platform Query Service.
exl-id: c5b71cc8-1d30-48c0-a8e2-135445a66639
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Anslut [!DNL GitHub Copilot] och [!DNL Visual Studio Code] till frågetjänsten

>[!IMPORTANT]
>
>Innan du använder det här integrerade verktyget måste du förstå vilka data som delas med GitHub. Delade data innehåller sammanhangsberoende information om koden och de filer som redigeras (&quot;prompts&quot;) och information om användaråtgärder (&quot;användarinteraktionsdata&quot;).  Läs sekretesspolicyn ](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement#github-privacy-statement) för [[!DNL GitHub Copilot] om du vill veta mer om de data som samlas in. Ni måste också tänka på säkerhetsaspekterna av att involvera tredjepartstjänster, eftersom ni ansvarar för att se till att organisationens policyer för datastyrning följs. Adobe ansvarar inte för eventuella datarelaterade problem eller problem som kan uppstå vid användning av detta verktyg. Mer information finns i dokumentationen för GitHub.

[!DNL GitHub Copilot], som drivs av OpenAI Codex, är ett AI-drivet verktyg som förbättrar din kodningsupplevelse genom att föreslå kodfragment och hela funktioner direkt i redigeraren. Integrerat med [!DNL Visual Studio Code] ([!DNL VS Code]) kan [!DNL Copilot] avsevärt snabba upp ditt arbetsflöde, särskilt när du arbetar med komplexa frågor. Följ den här vägledningen när du vill lära dig hur du ansluter [!DNL GitHub Copilot] och [!DNL VS Code] till frågetjänsten för att skriva och hantera dina frågor effektivare. Mer information om [!DNL Copilot] finns på [GitHub&#39;s Copilot ](https://github.com/pricing) och i [officiell [!DNL Copilot] dokumentation](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot).

Det här dokumentet innehåller de steg som krävs för att ansluta [!DNL GitHub Copilot] och [!DNL VS Code] med Adobe Experience Platform Query Service.

## Kom igång {#get-started}

Den här guiden kräver att du redan har åtkomst till ett GitHub-konto och har registrerat dig för [!DNL GitHub Copilot]. Du kan [registrera dig från GitHub-webbplatsen](https://github.com/github-copilot/signup). Du behöver också [!DNL VS Code]. Du kan [hämta [!DNL VS Code] från deras officiella webbplats](https://code.visualstudio.com/download).

När du har installerat [!DNL VS Code] och aktiverat din [!DNL Copilot]-prenumeration måste du hämta dina anslutningsautentiseringsuppgifter för Experience Platform. Dessa autentiseringsuppgifter finns på fliken [!UICONTROL Credentials] på arbetsytan [!UICONTROL Queries] i Experience Platform-gränssnittet. Läs referenshandboken för att [lära dig hur du hittar de här värdena i användargränssnittet för Experience Platform](../ui/credentials.md). Kontakta din organisationsadministratör om du inte har tillgång till arbetsytan [!UICONTROL Queries].

### [!DNL Visual Studio Code] tillägg som krävs {#required-extensions}

Följande [!DNL Visual Studio Code] tillägg krävs för att effektivt hantera och fråga dina Experience Platform SQL-databaser direkt i kodredigeraren. Hämta och installera dessa tillägg.

- [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools): Använd SQLTools-tillägget för att hantera och fråga efter flera SQL-databaser. Den innehåller funktioner som frågekörare, SQL-formatering och anslutningsutforskare, med stöd för ytterligare drivrutiner för att öka utvecklingsproduktiviteten. Läs översikten om Visual Studio Marketplace för mer information.
- [SQLTools PostgreSQL/Cockroach Driver](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg): Med det här tillägget kan du ansluta, fråga efter och hantera PostgreSQL- och CockroachDB-databaser direkt i kodredigeraren.

Nästa tillägg aktiverar [!DNL GitHub Copilot] och dess chattfunktioner.

- [[!DNL GitHub Copilot]](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot): Visar inline-kodningsförslag medan du skriver.
- [[!DNL GitHub Copilot] Chatt](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat): Ett tillägg som ger konversationshjälp.

## Skapa anslutning {#create-connection}

Välj cylinderikonen (![Cylinderikonen.](../images/clients/github-copilot/cylinder-icon.png)) i den vänstra navigeringen för [!DNL VS Code], följt av **[!DNL Add New Connection]** eller cylinderplustecknet (![cylinderplustecknet.](../images/clients/github-copilot/cylinder-plus-icon.png)).

![Gränssnittet för Visual Studio-koden med SQL-verktygstillägget och Lägg till ny anslutning markerat.](../images/clients/github-copilot/add-new-connection.png)

**[!DNL Connection Assistant]** visas. Välj databasdrivrutinen **[!DNL PostgreSQL]**.

![Inställningssidan för SQLTools i [!DNL VS Code] med PostgreSQl markerad.](../images/clients/github-copilot/postgres-database-driver.png)

### Inställningar för indataanslutning {#input-connection-settings}

Vyn [!DNL Connection Settings] visas. Ange dina Experience Platform-anslutningsautentiseringsuppgifter i lämpliga fält för SQLTools [!DNL Connection Assistant]. De värden som krävs förklaras i tabellen nedan.

| Egenskap | Beskrivning |
| --- |--- |
| [!DNL Connection name] | Ange en [!DNL Connection name]-typ `Prod_MySQL_Server` som är beskrivande och tydligt anger dess syfte (till exempel en produktionsmiljö för en MySQL-server). Bästa tillvägagångssätt är:<br><ul><li>Följ din organisations namngivningskonventioner för att säkerställa att den är unik i systemet.</li><li>Behåll det kortfattat för att behålla klarheten och undvika förvirring med andra kopplingar.</li><li>Inkludera relevant information om anslutningsens funktion eller miljö i namnet.</li></ul> |
| [!DNL Connect using] | Använd alternativet **[!DNL Server and Port]** för att ange serveradressen (värdnamnet) och portnumret för att upprätta en direktanslutning till Experience Platform |
| [!DNL Server address] | Ange värdet **[!UICONTROL Host]** som anges i dina Experience Platform Postgres-autentiseringsuppgifter, till exempel `acmeprod.platform-query.adobe.io`. |
| [!DNL Port] | Det här värdet är vanligtvis `80` för Experience Platform-tjänster. |
| [!DNL Database] | Ange värdet **[!UICONTROL Database]** som anges i dina Experience Platform Postgres-autentiseringsuppgifter, till exempel `prod:all`. |
| [!DNL Username] | Den här egenskapen refererar till ditt organisations-ID. Ange värdet **[!UICONTROL Username]** som anges i dina Experience Platform Postgres-autentiseringsuppgifter. |
| [!DNL Password] | Den här egenskapen är din åtkomsttoken. Ange värdet **[!UICONTROL Password]** som anges i dina Experience Platform Postgres-autentiseringsuppgifter. |

![Anslutningsassistentens arbetsyta med flera inställningar markerade.](../images/clients/github-copilot/connection-settings.png)

Välj sedan **[!DNL Use Password]** följt av **[!DNL Save as plaintext in settings]** i listrutan som visas. Fältet [!DNL Password] visas. Använd det här textinmatningsfältet för att ange din åtkomsttoken.

![Lösenordet, listrutan och lösenordsfältet är markerade.](../images/clients/github-copilot/access-token.png)

Om du vill aktivera SSL markerar du indatafältet [!DNL SSL] och väljer [!DNL Enabled] i listrutan som visas.

![SSL-fältet med aktiverad i listrutan är markerat.](../images/clients/github-copilot/ssl-enabled.png)

>[!TIP]
>
>När du har angett alla inloggningsuppgifter kan du testa anslutningen innan du sparar anslutningen. Bläddra nedåt till arbetsytans nederkant och välj **[!DNL Test Connection]**.
>
>![Arbetsytan Anslutningsassistenten med Test Connection markerad.](../images/clients/github-copilot/test-connection.png "Arbetsytan Anslutningsassistenten med Test Connection är markerad."){width="100" zoomable="yes"}

När du har angett anslutningsinformationen korrekt kan du bekräfta inställningarna genom att välja **[!DNL Save Connection]**.

![Arbetsytan Anslutningsassistenten med Spara anslutning är markerad.](../images/clients/github-copilot/save-connection.png)

Vyn [!DNL Review connection details] visas och visar dina anslutningsautentiseringsuppgifter. När du är säker på att dina anslutningsdetaljer är korrekta väljer du **[!DNL Connect Now]**.

![Vyn Granska anslutningsinformation med Connect Now markerad.](../images/clients/github-copilot/review-and-connect.png)

Arbetsytan [!DNL VS Code] visas med ett förslag från [!DNL GitHub Copilot].

![En ansluten SQL-session i [!DNL VS Code].](../images/clients/github-copilot/connected.png)

## Snabbguide för [!DNL GitHub Copilot]

När du är ansluten till din Experience Platform-instans kan du använda [!DNL Copilot] som en AI-kodningsassistent för att skriva kod snabbare och med större tillförsikt. I det här avsnittet beskrivs de viktigaste funktionerna och hur du använder dem.

## Kom igång med [!DNL GitHub Copilot] {#get-started-with-copilot}

Kontrollera först att du har den senaste versionen av [!DNL VS Code] installerad. En inaktuell version av [!DNL VS Code] kan förhindra att viktiga funktioner i [!DNL Copilot] fungerar som de ska. Kontrollera sedan att inställningen [!DNL Enable Auto Completions] är aktiverad. Om [!DNL Copilot] körs på rätt sätt visas **[!DNL Copilot]icon** (![Copilot-ikonen ](../images/clients/github-copilot/copilot-icon.png)) i statusfältet (om det finns ett problem visas felikonen [!DNL Copilot] i stället). Välj ikonen **[!DNL Copilot]** för att öppna menyn [!DNL [!DNL GitHub Copilot]]. Välj **[!DNL Edit Settings]** på **[!DNL [!DNL GitHub Copilot]-menyn]**

![Redigeraren [!DNL VS Code] med [!DNL GitHub Copilot Menu] och ikonen [!DNL Copilot] och Redigera inställningar är markerade.](../images/clients/github-copilot/github-copilot-menu.png)

Bläddra bland alternativen och kontrollera att kryssrutan är aktiverad för inställningen [!DNL Enable Auto Completions].

![Inställningspanelen för [!DNL GitHub Copilot] med kryssrutan Aktivera automatiska kompileringar markerad och markerad.](../images/clients/github-copilot/enable-auto-completions.png)

## Kodkompletteringar {#code-completions}

När du har installerat tillägget [!DNL GitHub Copilot] och loggat in aktiveras automatiskt funktionen **Ghost Text** som föreslår kodkomplettering medan du skriver. Med dessa förslag kan du skriva kod effektivare och med färre avbrott. Du kan också använda kommentarer som vägledning för AI-kodförslagen. Detta innebär att icke-tekniska användare kan konvertera enkelt tal till kod för att utforska sina data.

![VSCode-gränssnittet med ett kodförslag och ikonen [!DNL GitHub Copilot] markerad.](../images/clients/github-copilot/ghost-text.png)

>[!TIP]
>
>Om du vill inaktivera [!DNL Copilot] för en viss fil eller ett visst språk markerar du ikonen i statusfältet och inaktiverar den.

### Acceptera fullständiga eller partiella förslag på Ghost-text {#accept-suggestions}

När [!DNL GitHub Copilot] föreslår kodkomplettering kan du acceptera antingen partiella eller fullständiga förslag. Välj **Tabb** om du vill acceptera hela förslaget eller håll ned **Ctrl (eller Cmd på Mac)** och tryck på **högerpilen** om du vill acceptera en del av texten. Om du vill stänga ett förslag trycker du på **Esc**.

>[!TIP]
>  
>Om du inte får några förslag kontrollerar du att [[!DNL Copilot] är aktiverat i filens språk](#get-started-with-copilot).

![Redigeraren [!DNL VS Code] visar ett svagt grått textförslag från [!DNL GitHub Copilot] som Ghost-text bredvid delvis typbestämd kod.](../images/clients/github-copilot/accept-partial-suggestions.png)

### Alternativ förslag {#alternative-suggestions}

Om du vill bläddra igenom alternativa kodförslag markerar du pilarna i dialogrutan [!DNL Copilot].

![Redigeraren [!DNL VS Code] som visar panelen med alternativa förslag för Kopiera.](../images/clients/github-copilot/code-suggestions.png)


## Använd intern chatt {#inline-chat}

Du kan också chatta med [!DNL Copilot] direkt om din kod. Använd **Kontroll (eller Kommando) + I** för att utlösa den infogade chattdialogrutan. Den här funktionen används för att iterera i koden och förfina förslag i sitt sammanhang. Du kan markera ett kodblock och använda intern chatt för att se en annan lösning som föreslås av AI innan du godkänner den.

![Det infogade chattfönstret med diff-vyn](../images/clients/github-copilot/inline-chat.png)

<!-- THis section is poss unnecessary:
There are inline features for chat including doc, expalin, fix and test
![fix, document, explain](../images/clients/github-copilot/fix-document-explain.png)
 -->

## Dedikerad chattvy {#dedicated-chat}

Du kan använda ett mer traditionellt chattgränssnitt med ett dedikerat sidofält för chatt för att utforma idéer och strategi, lösa kodningsproblem och diskutera implementeringsdetaljer. Välj chattikonen (![Ikonen Copilot Chat.](../images/clients/github-copilot/chat-icon.png)) i sidofältet [!DNL VS Code] för att öppna ett dedikerat chattfönster.

![Chatt-sidofältet [!DNL GitHub Copilot] med chattikonen markerad.](../images/clients/github-copilot/chat-sidebar.png)

Du kan även komma åt chatthistoriken genom att välja historikikonen (![Historikikonen.](../images/clients/github-copilot/history-icon.png)) högst upp på chattpanelen.

## Nästa steg

Nu kan du effektivt söka i dina Experience Platform-databaser direkt från kodredigeraren och använda [!DNL GitHub Copilot]s AI-baserade kodförslag för att effektivisera skrivandet och optimeringen av SQL-frågor. Mer information om hur du skriver och kör frågor finns i [vägledningen för frågekörning](../best-practices/writing-queries.md).
