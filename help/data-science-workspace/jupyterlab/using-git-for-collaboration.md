---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;Git;Github
solution: Experience Platform
title: Samarbeta i JupyterLab med Git
type: Tutorial
description: Git är ett distribuerat versionshanteringssystem för att spåra ändringar i källkoden under programvaruutvecklingen. Git är förinstallerat i JupyterLab-miljön för Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Samarbeta i [!DNL JupyterLab] använda [!DNL Git]

[!DNL Git] är ett distribuerat versionshanteringssystem för att spåra ändringar i källkod under programvaruutveckling. Git är förinstallerat i [!DNL Data Science Workspace JupyterLab] miljö.

## Förutsättningar

>[!NOTE]
>
> Den Git-server du tänker använda måste vara tillgänglig via Internet.

The [!DNL Data Science Workspace JupyterLab] -miljön är en värdmiljö som inte används i företagets brandvägg, och därför måste den Git-server som du ansluter till vara tillgänglig från det offentliga Internet. Detta kan vara en offentlig eller privat databas på [GitHub](https://github.com/) eller en annan instans av en [!DNL Git] server som du har bestämt dig för att vara värd för dig själv.

## Anslut [!DNL Git] till [!DNL Data Science Workspace JupyterLab Notebooks] miljö

Starta genom att starta [!DNL Adobe Experience Platform] och navigera till [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) miljö.

Inom [!DNL JupyterLab], markera **[!UICONTROL File]** hovra sedan över **[!UICONTROL New]**. I listrutan som visas väljer du **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Nästa, inom *Terminal* navigera till arbetsytan med följande kommando: `cd my-workspace`.

![arbetsyta för cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Om du vill visa en lista med tillgängliga Git-kommandon skickar du kommandot: `git -help` i terminalen.

Klona sedan den databas du vill använda med `git clone` -kommando. Klona ditt projekt med en `https://` URL i stället för `ssh://`.

**Exempel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klona](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> För att kunna utföra skrivåtgärder (`git push` till exempel) följande konfigurationskommandon måste köras för varje ny session. Observera också att eventuella push-kommandon kräver ett användarnamn och lösenord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nästa steg

När du är klar med kloningen av din databas kan du använda Git på samma sätt som du brukar göra på din lokala dator för att samarbeta med andra på bärbara datorer. Mer information om vad du kan göra inom [!DNL JupyterLab], se [[!DNL JupyterLab user guide]](./overview.md).
