---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Maskininlärning i realtid - översikt
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Maskininlärning i realtid - översikt

>[!IMPORTANT]
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

Med Adobe Experience Platforms ramverk för maskininlärning i realtid kan ni använda maskininlärning för att leverera rätt upplevelse till rätt slutanvändare vid rätt tidpunkt i rätt kanaler med en subsekundär tidsram.

## Fördelar

Maskininlärning i realtid kan dramatiskt öka relevansen i ert innehåll för digitala upplevelser för era slutanvändare. Detta blir möjligt genom att utnyttja realtidsinterferenser och kontinuerlig inlärning på Experience Edge.

En kombination av sömlös beräkning på både hubben och Edge minskar dramatiskt den latens som traditionellt används för att driva hyperpersonaliserade upplevelser som är både relevanta och responsiva. Maskininlärning i realtid ger därmed en otroligt låg latens för synkront beslutsfattande. Exempel på detta är återgivning av anpassat webbsidesinnehåll eller visning av ett erbjudande eller en rabatt för att minska bortfallet och öka antalet konverteringar i en webbutik.

## Maskininlärningsarkitektur i realtid

I följande diagram visas en översikt över Machine Learning-arkitekturen i realtid.

![Förenklad översikt](../images/rtml/simple-overview.png)

## Arbetsflöde för maskininlärning i realtid (alfa)

I följande arbetsflöde beskrivs de vanliga stegen och resultaten för att skapa och använda en Machine Learning-modell i realtid.

### Intag av data och preparat

Data importeras och omvandlas med Experience Data Model (XDM) på Adobe Experience Platform. Dessa data används för modellutbildning. Mer information om XDM finns i [XDM-översikten](../../xdm/home.md).

### Redigering

Skapa en maskininlärningsmodell i realtid genom att skapa den från grunden eller ta in den som en förutbildad serialiserad ONNX-modell i Adobe Experience Platform Jupyter Notebooks.

### Distribution

Distribuera din modell till Experience Edge för att skapa en maskininlärningstjänst i realtid i tjänstgalleriet med API-slutpunkten för förutsägelse.

### Inledning

Använd REST API-slutpunkten för förutsägelse för att generera maskininlärningsinsikter i realtid.

### Leverans

Marknadsförarna kan sedan definiera segment och regler som mappar Machine Learning-resultat i realtid till upplevelser med Adobe Target. På så sätt kan besökare på ert varumärkes webbplats visas på samma eller nästa sida med en hyper-personaliserad upplevelse i realtid (under 100 ms).

## Utvecklingsplan

Maskininlärning i realtid är för närvarande i alfafasen. Tabellen nedan visar några av de funktioner och uppdateringar som förväntas släppas i den framtida betatestningen.

<table>
    <th></th>
    <th>Alfa (maj)</th>
    <th>Beta</th>
    <tr>
        <td>
            <strong>Funktioner</strong>
        </td>
        <td>
            <li>Data Science Workspace ger dig en egen modell och författare via en startintegration för bärbara datorer.</li>
            <li>Startuppsättning med redigeringsoperatorer.</li>
            <li>Distribuera till hubben</li>
            <li>Scikit Learn-baserade modeller.</li>
        </td>
        <td>
            <li>Integrering av gränssnitt i tjänstgalleriet för datavetenskap.</li>
            <li>Förbättra automatiskt kundprofilen i realtid med resultat av häpnadsväckande resultat.</li>
            <li>Djupgående utbildningsmodeller.</li>
            <li>Utökad uppsättning med redigeringsoperatorer, inklusive anpassade operatorer.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Tillgänglighet</strong>
        </td>
        <td>
            Nordamerika
        </td>
        <td>
            <li>Nordamerika</li>
            <li>Europa och Mellanöstern (EMEA)</li>
            <li>Asien/Stillahavsområdet (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Redigering</strong>
        </td>
        <td>
            <li>Stöd för Python</li>
            <li>Machine Learning SDK i realtid</li>
            <li>Python-redigeringsnoder: Pandor, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Stöd för Tensorflow.</li>
            <li>Fler Python-redigeringsnoder: Kundprofilläsare i realtid, kundprofilskrivaren i realtid, nukleära matriser, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Körtider för poäng</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Nästa steg

Du kan börja med att följa guiden [Komma igång](./getting-started.md) . I den här guiden får du hjälp med att konfigurera alla nödvändiga förutsättningar för att skapa en maskininlärningsmodell i realtid.

