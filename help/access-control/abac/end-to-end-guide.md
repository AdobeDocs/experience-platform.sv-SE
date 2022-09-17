---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;
title: Attributbaserad åtkomstkontroll - från början till slut
description: Det här dokumentet innehåller en komplett guide om attributbaserad åtkomstkontroll i Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: f7a8f9a5eb0ef3c961f9524057ff01564f88dec3
workflow-type: tm+mt
source-wordcount: '2099'
ht-degree: 0%

---

# Attributbaserad åtkomstkontroll från början till slut

Attributbaserad åtkomstkontroll är en Adobe Experience Platform-funktion som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Med den här funktionen kan du kategorisera schemafält, segment och så vidare med etiketter som definierar användningsområde för organisation eller data. I Adobe Journey Optimizer kan du använda samma etiketter på resor och erbjudanden. Samtidigt kan administratörer definiera åtkomstprinciper runt XDM-schemafält och bättre hantera vilka användare eller grupper (interna, externa eller externa användare) som har åtkomst till dessa fält.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [[!DNL Experience Data Model (XDM)] System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Segmenteringsmotorn i [!DNL Platform] används för att skapa målgruppssegment utifrån era kundprofiler utifrån kundbeteenden och attribut.

### Använd ärendeöversikt

I den här handboken används ett exempel för att begränsa åtkomsten till känsliga data för att demonstrera arbetsflödet. Du kommer att gå igenom ett exempel på ett attributbaserat arbetsflöde för åtkomstkontroll där du kan skapa och tilldela roller, etiketter och profiler för att konfigurera om användarna kan eller inte kan komma åt vissa resurser i organisationen. Det här användningsexemplet beskrivs nedan:

Du är vårdgivare och vill konfigurera åtkomst till resurser i din organisation.

* Ditt interna marknadsföringsteam bör kunna komma åt **[!UICONTROL PHI/ Regulated Health Data]** data.
* Din externa myndighet bör inte kunna komma åt **[!UICONTROL PHI/ Regulated Health Data]** data.

För att kunna göra detta måste du konfigurera roller, resurser och principer.

Du kommer att:

* [Ange en etikett för rollerna för användarna]{#label-roles}: Använd exemplet med en vårdleverantör (ACME Business Group) vars marknadsföringsgrupp arbetar med externa byråer.
* [Märk upp dina resurser (schemafält och segment)]{#label-resources}: Tilldela **[!UICONTROL PHI/ Regulated Health Data]** för att schemalägga resurser och segment.
* [Skapa en profil som länkar ihop dem]{#policy}: Skapa en profil för att länka etiketterna på dina resurser till etiketterna i din roll och neka åtkomst till schemafält och segment. Detta nekar åtkomst till schemafältet och segmentet i alla sandlådor för användare som inte har matchande etiketter.

## Behörigheter

[!UICONTROL Permissions] är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram.

Via [!UICONTROL Permissions]kan du skapa och hantera roller samt tilldela önskade resursbehörigheter för rollerna. [!UICONTROL Permissions] gör det även möjligt att hantera etiketter, sandlådor och användare som är kopplade till en viss roll.

Om du inte har administratörsbehörighet kontaktar du systemadministratören för att få åtkomst.

När du har administratörsbehörighet går du till [Adobe Experience Cloud](https://experience.adobe.com/) och logga in med dina inloggningsuppgifter för Adobe. När du är inloggad visas **[!UICONTROL Overview]** visas för din organisation som du har administratörsbehörighet för. På den här sidan visas de produkter som din organisation prenumererar på, tillsammans med andra kontroller för att lägga till användare och administratörer i organisationen som helhet. Välj **[!UICONTROL Permissions]** för att öppna arbetsytan för din plattformsintegrering.

![Bild som visar den behörighetsprodukt som väljs i Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Arbetsytan Behörigheter för plattformsanvändargränssnittet visas på **[!UICONTROL Roles]** sida.

## Använd etiketter för en roll {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="Vad är etiketter?"
>abstract="Med etiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Plattformen har flera Adobe-definierade etiketter för dataanvändning, som omfattar ett stort antal vanliga begränsningar för datastyrning. Känsliga&quot;S&quot;-etiketter, till exempel RHD (Regulated Health Data), gör att du kan kategorisera data som hänvisar till Skyddad hälsoinformation (PHI). Du kan också definiera egna etiketter som passar organisationens behov."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Översikt över etiketter för dataanvändning"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Skapa ny etikett"
>abstract="Du kan skapa egna etiketter som passar organisationens behov. Anpassade etiketter kan användas för att tillämpa både datastyrning och åtkomstkontrollskonfigurationer på dina data."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Hantera anpassade etiketter"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Vad är roller?"
>abstract="Roller är sätt att kategorisera de typer av användare som interagerar med din plattformsinstans och är byggstenar för åtkomstkontrollprinciper. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Hantera roller"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Skapa ny roll"
>abstract="Du kan skapa en ny roll för att kategorisera användare som har åtkomst till din Platform-instans bättre. Du kan till exempel skapa en roll för ett internt marknadsföringsteam och använda RHD-etiketten på den rollen, vilket gör att ditt interna marknadsföringsteam kan komma åt informationen om den skyddade hälsan (PHI). Du kan också skapa en roll för ett externt organ och neka rollåtkomst till PHI-data genom att inte använda RHD-etiketten på den rollen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Skapa en ny roll"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Rollöversikt"
>abstract="I dialogrutan för rollöversikt visas de resurser och sandlådor som en viss roll har åtkomst till."

Roller är sätt att kategorisera de typer av användare som interagerar med din plattformsinstans och är byggstenar för åtkomstkontrollprinciper. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilken typ av åtkomst de behöver.

För att komma igång väljer du **[!UICONTROL ACME Business Group]** från **[!UICONTROL Roles]** sida.

![Bild som visar ACME Business Role som väljs i Roller](../images/abac-end-to-end-user-guide/abac-select-role.png)

Nästa, välj **[!UICONTROL Labels]** och sedan markera **[!UICONTROL Add Labels]**.

![Bild som visar Lägg till etiketter som markeras på fliken Etiketter](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

En lista över alla etiketter i organisationen visas. Välj **[!UICONTROL RHD]** för att lägga till etiketten för **[!UICONTROL PHI/Regulated Health Data]**. Tillåt en liten stund för en blå bockmarkering att visas bredvid etiketten och välj sedan **[!UICONTROL Save]**.

![Bild som visar den RHD-etikett som markeras och sparas](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## Tillämpa etiketter på schemafält {#label-resources}

Nu när du har konfigurerat en användarroll med [!UICONTROL RHD] label är nästa steg att lägga till samma etikett till de resurser som du vill styra för den rollen.

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen och välj **[!UICONTROL ACME Healthcare]** från listan med scheman som visas.

![Bild som visar ACME Healthcare-schemat som väljs på fliken Scheman](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Nästa, välj **[!UICONTROL Labels]** för att visa en lista som visar de fält som är kopplade till ditt schema. Härifrån kan du tilldela etiketter till ett eller flera fält samtidigt. Välj **[!UICONTROL BloodGlucose]** och **[!UICONTROL InsulinLevel]** fält och sedan markera **[!UICONTROL Edit governance labels]**.

![Bild som visar den BloodGlukos och InsulinLevel som väljs och redigerar styrningsetiketter som väljs](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

The **[!UICONTROL Edit labels]** visas så att du kan välja de etiketter som du vill använda i schemafälten. I det här fallet väljer du **[!UICONTROL PHI/ Regulated Health Data]** etikett, markera **[!UICONTROL Save]**.

![Bild som visar den RHD-etikett som markeras och sparas](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>När en etikett läggs till i ett fält används den etiketten på den överordnade resursen för det fältet (antingen en klass eller en fältgrupp). Om den överordnade klassen eller fältgruppen används av andra scheman ärver dessa scheman samma etikett.

## Använd etiketter på segment

När du har etiketterat dina schemafält kan du nu börja märka segmenten.

Välj **[!UICONTROL Segments]** från vänster navigering. En lista över segment som är tillgängliga i din organisation visas. I det här exemplet ska följande två segment märkas som om de innehåller känsliga hälsodata:

* Blodglukos >100
* Insulin &lt;50

Välj **[!UICONTROL Blood Glucose >100]** för att börja märka segmentet.

![Bild som visar den blodglukos >100 som väljs på fliken Segment](../images/abac-end-to-end-user-guide/abac-select-segment.png)

Segmentet **[!UICONTROL Details]** visas. Välj **[!UICONTROL Manage Access]**.

![Bild som visar urvalet av hanteraråtkomst](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

The **[!UICONTROL Edit labels]** visas så att du kan välja de etiketter som du vill använda på segmentet. I det här fallet väljer du **[!UICONTROL PHI/ Regulated Health Data]** etikett, markera **[!UICONTROL Save]**.

![Bild som visar markeringen av RHD-etiketten och spara som markeras](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Upprepa stegen ovan med **[!UICONTROL Insulin <50]**.

## Skapa en åtkomstkontrollprincip {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Vad är policyer?"
>abstract="Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Alla organisationer har en standardprofil som du måste aktivera för att definiera regler för resurser som segment och schemafält. Standardprofiler kan varken redigeras eller tas bort. Standardprofiler kan dock aktiveras eller inaktiveras."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Hantera profiler"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Skapa en profil"
>abstract="Skapa en profil för att definiera de åtgärder som dina användare kan och inte kan vidta mot dina segment och schemafält."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Skapa en profil"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Konfigurera tillåtna och otillåtna åtgärder för en princip"
>abstract="Välj Tillåt åtkomst till för att konfigurera tillåtna åtgärder som dina användare kan utföra mot resurser. Markera Neka åtkomst till om du vill konfigurera otillåtna åtgärder som användarna inte kan utföra mot resurser."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Redigera en profil"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Konfigurera behörigheter för en resurs"
>abstract="En resurs är den resurs eller det objekt som en användare kan eller inte kan komma åt. Resurser kan vara segment eller scheman. Du kan konfigurera skriv-, läs- och borttagningsbehörigheter för segment och schemafält."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Redigera villkor"
>abstract="Använd villkorssatser i din profil för att konfigurera användaråtkomst till vissa resurser. Välj Matcha alla om du vill att användare ska ha roller med exakt samma etiketter som en resurs för att få åtkomst. Välj Matcha alla om du bara vill att användare ska ha en roll med bara en etikett som matchar en resurs. Etiketter kan antingen definieras som kärnetiketter eller egna etiketter, med etiketter som representerar etiketter som skapats och tillhandahållits av Adobe och anpassade etiketter som representerar etiketter som du har skapat för din organisation."

Åtkomstkontrollprinciper använder etiketter för att definiera vilka användarroller som har åtkomst till specifika plattformsresurser. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler. I det här exemplet nekas åtkomst till schemafält och segment i alla sandlådor för användare som inte har motsvarande etiketter i schemafältet.

Om du vill skapa en åtkomstkontrollprincip väljer du **[!UICONTROL Permissions]** i den vänstra navigeringen och välj **[!UICONTROL Policies]**. Nästa, välj **[!UICONTROL Create policy]**.

![Bild som visar principen Skapa som väljs i Behörigheter](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** visas och du uppmanas att ange ett namn och en valfri beskrivning. Välj **[!UICONTROL Confirm]** när du är klar.

![Bild som visar dialogrutan Skapa ny profil och väljer Bekräfta](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Om du vill neka åtkomst till schemafälten använder du listrutepilen och väljer **[!UICONTROL Deny access to]** och sedan markera **[!UICONTROL No resource selected]**. Nästa, välj **[!UICONTROL Schema Field]** och sedan markera **[!UICONTROL All]**.

![Bild som visar Neka-åtkomst och valda resurser](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

Tabellen nedan visar de villkor som är tillgängliga när du skapar en profil:

| Villkor | Beskrivning |
| --- | --- |
| Följande är false | När Neka åtkomst till är inställt begränsas åtkomsten om användaren inte uppfyller de valda villkoren. |
| Följande är sant | När Tillåten åtkomst till har angetts, begränsas åtkomsten om användaren uppfyller de valda villkoren. |
| Matchar alla | Användaren har en etikett som matchar alla etiketter som används på en resurs. |
| Matchar alla | Användaren har alla etiketter som matchar alla etiketter som används på en resurs. |
| Kärnetikett | En kärnetikett är en Adobe-definierad etikett som är tillgänglig i alla plattformsinstanser. |
| Egen etikett | En anpassad etikett är en etikett som har skapats av din organisation. |

Välj **[!UICONTROL The following being false]** och sedan markera **[!UICONTROL No attribute selected]**. Välj sedan användaren **[!UICONTROL Core label]** väljer **[!UICONTROL Matches all]**. Välj resurs **[!UICONTROL Core label]** och slutligen markera **[!UICONTROL Add resource]**.

![Bild som visar villkoren som väljs och Lägg till resurs som väljs](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>En resurs är den resurs eller det objekt som ett ämne kan eller inte kan komma åt. Resurser kan vara segment eller scheman.

Om du vill neka åtkomst till segmenten använder du listrutepilen och väljer **[!UICONTROL Deny access to]** och sedan markera **[!UICONTROL No resource selected]**. Nästa, välj **[!UICONTROL Segment]** och sedan markera **[!UICONTROL All]**.

Välj **[!UICONTROL The following being false]** och sedan markera **[!UICONTROL No attribute selected]**. Välj sedan användaren **[!UICONTROL Core label]** väljer **[!UICONTROL Matches all]**. Välj resurs **[!UICONTROL Core label]** och slutligen markera **[!UICONTROL Save]**.

![Bild som visar markerade villkor och Spara markeras](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Välj **[!UICONTROL Activate]** om du vill aktivera profilen visas en dialogruta där du uppmanas att bekräfta aktiveringen. Välj **[!UICONTROL Confirm]** och sedan markera **[!UICONTROL Close]**.

![Bild som visar principen som aktiveras ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Nästa steg

Du har slutfört användningen av etiketter för en roll, schemafält och segment. Den externa byrå som tilldelats de här rollerna är begränsad från att visa dessa etiketter och deras värden i schemat, datauppsättningen och profilvyn. Dessa fält är också begränsade från att användas i segmentdefinitionen när segmentbyggaren används.

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](./overview.md).
