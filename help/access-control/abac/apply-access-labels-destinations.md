---
title: Använd åtkomstetiketter för att hantera användaråtkomst till måldataflöden
description: Lär dig hur du använder åtkomstetiketter för att hantera användaråtkomst till måldataflöden så att bara en delmängd av användarna i organisationen får åtkomst till specifika måldataflöden.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Använd åtkomstetiketter för att hantera användaråtkomst till måldataflöden

Som en del av funktionen [!UICONTROL Attribute-based access control] i Real-Time CDP kan du nu använda åtkomstetiketter i måldataflöden. På så sätt kan du se till att bara en delmängd av användarna i organisationen får tillgång till specifika måldataflöden.

När du lägger till en åtkomstetikett till ett visst mål kan bara användare som har tillgång till en roll som är tilldelad den etiketten se och redigera måldataflödet. Om ett måldataflöde inte har någon etikett visas det för alla användare som tillhör din organisation.

Läs den här sidan om du vill veta mer om exempel på användning, krav innan du kan använda åtkomstetiketter på måldataflöden och andra viktiga pratbubblor när du använder den här funktionen.

## Förhandskrav {#prerequisites}

Observera följande krav innan du börjar använda den här funktionen. Om du vill bekanta dig med funktionen [!UICONTROL Attribute-based access control] rekommenderar Adobe att du läser följande artiklar:

* [Attributbaserad åtkomstkontroll - översikt](/help/access-control/abac/overview.md)
* [Attributbaserad åtkomstkontroll från början till slut](/help/access-control/abac/end-to-end-guide.md)

### Åtkomst till behörighetsgränssnittet {#access-permissions-ui}

[!UICONTROL Permissions] är det område på Experience Cloud där administratörer kan definiera användarroller och profiler för att hantera behörigheter för funktioner och objekt i ett produktprogram. Läs avsnittet [permissions](/help/access-control/abac/end-to-end-guide.md#permissions) för att komma igång.

### Skapa roller, etiketter och tilldela användare {#create-roles-labels-assign-users}

När du har fått åtkomst till användargränssnittet för [!UICONTROL permissions] måste du eller en medlem i ditt team konfigurera roller och lägga till de nödvändiga etiketterna till de rollerna. Slutligen måste de användare som ska ha åtkomst till resurser som är märkta med de specifika etiketterna läggas till i rollen. Läs följande dokumentationsavsnitt:

* [Skapa en ny roll](/help/access-control/abac/ui/roles.md)
* [Lägg till etiketter i en roll](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Lägga till användare i en roll](/help/access-control/ui/users.md)

### Skapa måldataflöden {#create-dataflow}

Du måste först ansluta till det önskade målet och skapa ett dataflöde för att exportera data, innan du kan använda åtkomstetiketter för dataflödet.

Läs stödlinjerna för [att ansluta till ett mål](/help/destinations/ui/connect-destination.md) och [aktivera data till målet](/help/destinations/ui/activation-overview.md). Välj sedan önskat mål i [katalogen med tillgängliga kopplingar](/help/destinations/catalog/overview.md).

## Redan tillgängligt: Använd åtkomstetiketter på andra Experience Platform-resurser {#apply-labels-other-resources}

I den här versionen kan du ge användare åtkomst på objektnivå till specifika måldataflöden, men funktionen att bevilja åtkomstkontroll på objektnivå är redan allmänt tillgänglig för andra Experience Platform-resurser, som [målgrupper](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Exempel på användningsfall {#use-case-example}

Med åtkomstkontroll på objektnivå för destinationer kan du begränsa specifika grupper av marknadsförare så att de bara får tillgång till sina specifika destinationer. Om din organisation till exempel har kunddata på flera geografiska platser, som USA och Storbritannien, kan du begränsa ett marknadsföringsteam så att de kan visa och redigera dataflödena enbart för USA:s plats, och ett annat marknadsföringsteam kan visa och redigera dataflödena för den brittiska platsen.

## Tillämpa åtkomstetiketter på måldataflöden {#apply-labels-to-destination-dataflow}

Så här använder du åtkomstetiketter för ett specifikt dataflöde:

1. Navigera till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och leta reda på måldataflödet som du vill begränsa användarnas åtkomst till.
1. Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Redigera detaljer](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL Apply access labels]** för att lägga till nya etiketter och hantera befintliga etiketter för dataflödet.
   ![Välj Använd åtkomstetiketter i sökvyn på arbetsytan för mål.](/help/access-control/images/olac/apply-access-labels.png)
1. Markera etiketterna som du vill lägga till i måldataflödet och välj **[!UICONTROL Save]**.
   ![Välj de åtkomstetiketter i som ska gälla för måldataflödet.](/help/access-control/images/olac/view-access-labels.png)
1. Observera hur dataflödet nu har en åtkomstetikett som visas i användargränssnittet.
   ![Vy över flera måldataflöden med det valda dataflödet, hur en åtkomstetikett visas.](/help/access-control/images/olac/dataflow-with-access-label.png)

Om ett måldataflöde inte är markerat med några etiketter visas det för alla användare. Om dataflödet är markerat med en eller flera åtkomstetiketter visas det bara för användare som tillhör en roll som har samma etikett eller kombination av etiketter.

Du kan lägga till standardetiketter och anpassade etiketter i måldataflöden. När du har lagt till en etikett i måldataflödena:

* Användare som tilldelas roller med åtkomst till samma etikett kan visa dataflödet med den nya etiketten i användargränssnittet. De kan visa och redigera måldataflödet i användargränssnittet eller via API:er.

* Användare som *inte* har tilldelats roller med åtkomst till samma etikett har inte åtkomst till måldataflödet för att visa eller redigera det i användargränssnittet eller via API:er.

## Viktiga hänvisningar och objekt att känna till {#important-callouts}

Åtkomstetiketter kan för närvarande bara användas på befintliga dataflöden. Det innebär att någon måste skapa dataflödet till målet innan åtkomstetiketter kan användas.

Du kan inte använda en åtkomstetikett för ett måldataflöde om du inte har tillgång till den etiketten.

När du lägger till flera etiketter i ett måldataflöde måste användare som ska kunna visa och redigera dataflödet läggas till i en roll med minst samma kombination av etiketter. Om du till exempel använder etiketterna C1, I2 och en annan anpassad etikett på ett måldataflöde, kan bara användare som har lagts till i roller med åtkomst till kombinationen av dessa tre etiketter visa och redigera det här specifika måldataflödet.

![Venndiagram som visar hur bara vissa användare har åtkomst till mål med flera etiketter.](/help/access-control/images/olac/multiple-labels-venn.png)

## Nästa steg {#next-steps}

Genom att följa stegen i det här dokumentet vet du nu hur du använder åtkomstetiketter i måldataflöden, så att bara en delmängd av användarna i organisationen får tillgång till specifika måldataflöden.

Därefter kan du läsa mer om andra funktioner som stöds av [!UICONTROL Attribute-based access control] när du aktiverar data till mål. Du kan till exempel begränsa användarnas åtkomst till [vyn och endast aktivera specifika fält](/help/access-control/abac/overview.md#destinations).
