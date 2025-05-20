---
title: Migrera från JWT till OAuth Server-till-server-autentiseringsuppgifter
description: Lär dig hur du migrerar JWT-inloggningsuppgifter som inte upphör att gälla till OAuth Server-till-Server-autentiseringsuppgifter i Adobe Experience Platform för att upprätthålla säker, oavbruten åtkomst till Query Service innan stödet för JWT upphör 30 juni 2025. Den här guiden innehåller stegvisa instruktioner, förklarar beteendet efter migrering och besvarar vanliga frågor.
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Migrera från JWT till OAuth Server-till-Server-autentiseringsuppgifter

>[!IMPORTANT]
>
>Adobe har ersatt stödet för JWT-autentiseringsuppgifter som används av frågetjänsten. Efter 30 juni 2025 kommer inloggningsuppgifter som inte upphör att gälla baserat på JWT inte längre att uppdatera eller autentisera API-begäranden. För att förhindra avbrott i tjänsten måste du migrera alla giltiga autentiseringsuppgifter till OAuth Server-till-Server-autentisering.

Den här guiden visar hur du migrerar JWT-inloggningsuppgifter som inte upphör att gälla till OAuth Server-till-Server-inloggningsuppgifter i Adobe Experience Platform. Genom att slutföra den här processen får du tillgång till Query Service utan avbrott innan stödet för JWT-autentiseringsuppgifter upphör den 30 juni 2025.

Det här dokumentet innehåller stegvisa instruktioner för att utföra migreringen, förstå effekten och verifiera dina uppdaterade inloggningsuppgifter.

## Vem behöver migrera {#who-needs-to-migrate}

Om du använder inloggningsuppgifter som inte upphör att gälla i frågetjänsten måste du migrera var och en av dem. Detta gäller autentiseringsuppgifter som används i automatiserade arbetsflöden, schemalagda frågor eller anpassade API-integreringar.

Om du ser autentiseringsuppgifter som listas under avsnittet **[!UICONTROL Non-expiring Credentials]** på fliken **[!UICONTROL Credentials]** påverkas dessa.

## Så här migrerar du en autentiseringsuppgift {#how-to-migrate}

Du kan migrera autentiseringsuppgifter direkt i Experience Platform-gränssnittet. Navigera till **[!UICONTROL Queries]** i den vänstra navigeringen och välj sedan fliken **[!UICONTROL Credentials]**. Identifiera en autentiseringsuppgift som är markerad som giltig för migrering i avsnittet **[!UICONTROL Non-expiring Credentials]** och välj **[!UICONTROL Migrate]** bredvid den.

>[!NOTE]
>
>Migreringen tar 8 till 10 sekunder och kan inte avbrytas när den har startats.

![Arbetsytan Autentiseringsuppgifter för frågetjänsten med frågor, autentiseringsuppgifter och migrering markerad.](../images/ui/migrate-jwt-to-oauth/migrate.png)

Efter migreringen uppdaterar systemet autentiseringsuppgifterna för att använda OAuth Server-till-Server-autentisering. Den JWT-baserade metoden tas automatiskt ur bruk och statusen uppdateras till **[!UICONTROL Migrated]**.

Ingen omkonfiguration krävs. Befintliga jobb och integreringar fortsätter att fungera utan avbrott.

## Vad händer efter migrering {#after-migration}

När migreringen är klar:

- Dina autentiseringsuppgifter fortsätter att fungera sömlöst, så inga ändringar behövs i dina jobb eller integreringar.
- Frågetjänsten använder automatiskt OAuth Server-till-Server-autentisering.
- Den JWT-baserade autentiseringsmetoden har tagits bort och används inte längre.

>[!IMPORTANT]
>
>Du kan inte ångra den här ändringen. När autentiseringsuppgifterna har migrerats kan de inte återställas till JWT.

## Vanliga frågor och svar {#faq}

Dessa frågor tar upp vanliga problem och hjälper dig att säkerställa en smidig, avbrottsfri migrering.

### Varför tar Adobe bort JWT-autentiseringsuppgifter?

OAuth Server-till-Server är en säkrare och standardiserad autentiseringsmetod. Den ger bättre livscykelhantering och har stöd för en bredare plattformskonsekvens.

### Vad händer om jag inte migrerar före 30 juni 2025?

JWT-inloggningsuppgifterna avbryter uppdateringen och integreringar som är beroende av dem misslyckas. Adobe kan inte migrera autentiseringsuppgifter för din räkning om du inte initierar processen.

### Hur vet jag om jag behöver migrera?

Om en autentiseringsuppgift visas under avsnittet **[!UICONTROL Non-expiring Credentials]** på fliken Autentiseringsuppgifter måste dessa autentiseringsuppgifter migreras.

### Behöver jag uppdatera mina integreringar eller konfigurera om någonting?

Nej. Efter migreringen tar OAuth-autentiseringsuppgifterna över automatiskt. Inga manuella ändringar krävs i dina jobb eller integreringar.

### Kan jag migrera alla autentiseringsuppgifter samtidigt?

Nej. Du måste migrera varje autentiseringsuppgift individuellt med knappen **[!UICONTROL Migrate]**.

### Kan jag fortsätta att använda utgångna autentiseringsuppgifter?

Ja. Utgångna autentiseringsuppgifter påverkas inte av den här ändringen. Endast JWT-autentiseringsuppgifter som inte förfaller får migreras.

### Jag ser ett meddelande som säger &quot;[!UICONTROL No non-expiring credentials found.]&quot; Vad betyder det? Måste jag vidta någon åtgärd?

Det här meddelandet betyder att du inte har skapat några inloggningsuppgifter som inte går ut än, så du behöver inte göra något.

### Jag ser ett meddelande som säger [!UICONTROL AEP admin verification failed].. Vad betyder det? Måste jag vidta någon åtgärd?

Det här meddelandet anger att du antingen inte är administratör eller inte har de behörigheter som krävs för att skapa autentiseringsuppgifter som inte förfaller.

- Om dina behörigheter inte har ändrats nyligen innebär det att du aldrig har haft behörighet att skapa autentiseringsuppgifter, så ingen åtgärd behövs.
- Om dina behörigheter nyligen har ändrats kontaktar du organisationens administratör och ber dem migrera autentiseringsuppgifterna åt dig.

### Kan jag migrera autentiseringsuppgifter som inte förfaller för någon annan?

Ja, men bara om du är administratör. Endast administratörer har de behörigheter som krävs för att skapa och migrera autentiseringsuppgifter som inte upphör att gälla för andra användare, så att de kan fortsätta arbeta utan avbrott.

## Nästa steg {#next-steps}

Granska alla ej förfallna autentiseringsuppgifter på fliken [!UICONTROL Credentials] och migrera dem individuellt före 30 juni 2025. Kontakta Adobe om du har frågor eller support.
