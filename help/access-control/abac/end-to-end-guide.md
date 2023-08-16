---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;
title: Attributbaserad åtkomstkontroll - från början till slut
description: Det här dokumentet innehåller en komplett guide om attributbaserad åtkomstkontroll i Adobe Experience Platform
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: cf10eb11773320d10ece53f192beacc8da83e980
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Attributbaserad åtkomstkontroll från början till slut

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger kunder med flera varumärken och integritet större flexibilitet när det gäller att hantera användaråtkomst. Åtkomst till enskilda objekt, t.ex. schemafält och segment, kan beviljas/nekas med profiler som baseras på objektets attribut och roll. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Med den här funktionen kan du kategorisera schemafält, segment och så vidare med etiketter som definierar användningsområde för organisation eller data. Du kan använda samma etiketter på resor, erbjudanden och andra objekt i Adobe Journey Optimizer. Samtidigt kan administratörer definiera åtkomstprinciper runt XDM-schemafält (Experience Data Model) och bättre hantera vilka användare och grupper (interna, externa eller externa användare) som har åtkomst till dessa fält.

>[!NOTE]
>
>Det här dokumentet fokuserar på användningen av åtkomstkontrollprinciper. Om du försöker konfigurera profiler som styr **use** mer information än vilka plattformsanvändare som har åtkomst till den finns i handboken från början till slut på [datastyrning](../../data-governance/e2e.md) i stället.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande plattformskomponenter:

* [[!DNL Experience Data Model (XDM)] System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Segmenteringsmotorn i [!DNL Platform] används för att skapa målgruppssegment utifrån era kundprofiler utifrån kundbeteenden och attribut.

### Använd ärendeöversikt

Du kommer att gå igenom ett exempel på ett attributbaserat arbetsflöde för åtkomstkontroll där du kan skapa och tilldela roller, etiketter och profiler för att konfigurera om användarna kan eller inte kan komma åt specifika resurser i organisationen. I den här handboken används ett exempel på hur åtkomsten till känsliga data begränsas för att demonstrera arbetsflödet. Det här användningsexemplet beskrivs nedan:

Du är vårdgivare och vill konfigurera åtkomst till resurser i din organisation.

* Ditt interna marknadsföringsteam bör kunna komma åt **[!UICONTROL PHI/ Regulated Health Data]** data.
* Din externa myndighet bör inte kunna komma åt **[!UICONTROL PHI/ Regulated Health Data]** data.

För att kunna göra detta måste du konfigurera roller, resurser och principer.

Du kommer att:

* [Ange en etikett för rollerna för användarna](#label-roles): Använd exemplet med en vårdleverantör (ACME Business Group) vars marknadsföringsgrupp arbetar med externa byråer.
* [Märk upp dina resurser (schemafält och segment)](#label-resources): Tilldela **[!UICONTROL PHI/ Regulated Health Data]** för att schemalägga resurser och segment.
* 
   * [Aktivera profilen som ska länka ihop dem:](#policy): Aktivera standardprincipen för att förhindra åtkomst till schemafält och segment genom att ansluta etiketterna på dina resurser till etiketterna i din roll. Användare med matchande etiketter får sedan tillgång till schemafältet och segmentet i alla sandlådor.

## Behörigheter

[!UICONTROL Permissions] är det område i Experience Cloud där administratörer kan definiera användarroller och profiler för att hantera behörigheter för funktioner och objekt i ett produktprogram.

Via [!UICONTROL Permissions]kan du skapa och hantera roller och tilldela önskade resursbehörigheter för dessa roller. [!UICONTROL Permissions] gör det även möjligt att hantera etiketter, sandlådor och användare som är kopplade till en viss roll.

Kontakta systemadministratören för att få åtkomst om du inte har administratörsbehörighet.

När du har administratörsbehörighet går du till [Adobe Experience Cloud](https://experience.adobe.com/) och logga in med dina inloggningsuppgifter för Adobe. När du är inloggad visas **[!UICONTROL Overview]** visas för din organisation som du har administratörsbehörighet för. På den här sidan visas vilka produkter din organisation prenumererar på, tillsammans med andra kontroller för att lägga till användare och administratörer i organisationen. Välj **[!UICONTROL Permissions]** för att öppna arbetsytan för din plattformsintegrering.

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
>abstract="Du kan skapa en ny roll för att kategorisera användare som har åtkomst till din Platform-instans bättre. Du kan till exempel skapa en roll för ett internt marknadsföringsteam och använda RHD-etiketten på den rollen, så att ditt interna marknadsföringsteam kan komma åt informationen om den skyddade hälsan (PHI). Du kan också skapa en roll för ett externt organ och neka rollåtkomst till PHI-data genom att inte använda RHD-etiketten på den rollen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Skapa en ny roll"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Rollöversikt"
>abstract="I dialogrutan för rollöversikt visas de resurser och sandlådor som en viss roll har åtkomst till."

Roller är sätt att kategorisera de typer av användare som interagerar med din plattformsinstans och är byggstenar för åtkomstkontrollprinciper. En roll har en given uppsättning behörigheter, och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilken typ av åtkomst de behöver.

För att komma igång väljer du **[!UICONTROL ACME Business Group]** från **[!UICONTROL Roles]** sida.

![Bild som visar ACME Business Role som väljs i Roller](../images/abac-end-to-end-user-guide/abac-select-role.png)

Nästa, välj **[!UICONTROL Labels]** och sedan **[!UICONTROL Add Labels]**.

![Bild som visar Lägg till etiketter som markeras på fliken Etiketter](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

En lista över alla etiketter i organisationen visas. Välj **[!UICONTROL RHD]** för att lägga till etiketten för **[!UICONTROL PHI/Regulated Health Data]**. Tillåt en liten stund för en blå bockmarkering att visas bredvid etiketten och välj sedan **[!UICONTROL Save]**.

![Bild som visar den RHD-etikett som markeras och sparas](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>När du lägger till en organisationsgrupp i en roll läggs alla användare i gruppen till i rollen. Alla ändringar i organisationsgruppen (användare som har tagits bort eller lagts till) uppdateras automatiskt i rollen.

## Tillämpa etiketter på schemafält {#label-resources}

Nu när du har konfigurerat en användarroll med [!UICONTROL RHD] label är nästa steg att lägga till samma etikett till de resurser som du vill styra för den rollen.

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen och sedan väljer **[!UICONTROL ACME Healthcare]** från listan med scheman som visas.

![Bild som visar ACME Healthcare-schemat som väljs på fliken Scheman](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Nästa, välj **[!UICONTROL Labels]** för att visa en lista som visar de fält som är kopplade till ditt schema. Härifrån kan du tilldela etiketter till ett eller flera fält samtidigt. Välj **[!UICONTROL BloodGlucose]** och **[!UICONTROL InsulinLevel]** fält och sedan markera **[!UICONTROL Apply access and data governance labels]**.

![Bild som visar den BloodGlukos och InsulinLevel som väljs och som använder de etiketter för åtkomst och datastyrning som väljs](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

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

## Aktivera åtkomstkontrollprincipen {#policy}

Standardprincipen för åtkomstkontroll använder etiketter för att definiera vilka användarroller som har åtkomst till specifika plattformsresurser. I det här exemplet nekas åtkomst till schemafält och segment i alla sandlådor för användare som inte är i en roll som har motsvarande etiketter i schemafältet.

Om du vill aktivera åtkomstkontrollprincipen väljer du [!UICONTROL Permissions] i den vänstra navigeringen och sedan väljer **[!UICONTROL Policies]**.

![Lista över profiler som visas](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Välj sedan ellipsen (`...`) bredvid profilnamnet och en listruta med kontroller för att redigera, aktivera, ta bort eller duplicera rollen. Välj **[!UICONTROL Activate]** i listrutan.

![Listruta för att aktivera princip](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Dialogrutan för aktiveringspolicy visas. Där uppmanas du att bekräfta aktiveringen. Välj **[!UICONTROL Confirm]**.

![Dialogrutan Aktivera princip](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Bekräftelse på att profilen har aktiverats har tagits emot och du återgår till [!UICONTROL Policies] sida.

![Aktivera principbekräftelse](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Nästa steg

Du har slutfört användningen av etiketter för en roll, schemafält och segment. Den externa byrå som tilldelats de här rollerna är begränsad från att visa dessa etiketter och deras värden i schemat, datauppsättningen och profilvyn. Dessa fält är också begränsade från att användas i segmentdefinitionen när segmentbyggaren används.

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](./overview.md).
