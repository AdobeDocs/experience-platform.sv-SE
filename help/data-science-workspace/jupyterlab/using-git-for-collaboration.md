---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;Git;Github
solution: Experience Platform
title: Samarbeta i JupyterLab med Git
topic: tutorial
type: Tutorial
description: Git är ett distribuerat versionshanteringssystem för att spåra ändringar i källkoden under programvaruutvecklingen. Git är förinstallerat i JupyterLab-miljön för Data Science Workspace.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# Samarbeta i [!DNL JupyterLab] med [!DNL Git]

[!DNL Git] är ett distribuerat versionshanteringssystem för att spåra ändringar i källkod under programvaruutveckling. Git är förinstallerat i [!DNL Data Science Workspace JupyterLab]-miljön.

## Förutsättningar

>[!NOTE]
>
> Den Git-server du tänker använda måste vara tillgänglig via Internet.

Miljön [!DNL Data Science Workspace JupyterLab] är en hostingmiljö som inte används i företagets brandvägg, och därför måste den Git-server som du ansluter till vara tillgänglig från det offentliga Internet. Detta kan vara en offentlig eller privat databas på [GitHub](https://github.com/) eller en annan instans av en [!DNL Git]-server som du har valt att vara värd för själv.

## Anslut [!DNL Git] till [!DNL Data Science Workspace JupyterLab Notebooks]-miljön

Börja med att starta [!DNL Adobe Experience Platform] och navigera till [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)-miljön.

I [!DNL JupyterLab] väljer du **[!UICONTROL File]** och håller sedan markören över **[!UICONTROL New]**. Välj **[!UICONTROL Terminal]** i listrutan som visas.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Gå sedan till arbetsytan i *Terminal* med följande kommando: `cd my-workspace`.

![arbetsyta för cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Om du vill visa en lista med tillgängliga Git-kommandon skickar du kommandot: `git -help` i terminalen.

Sedan klonar du den databas du vill använda med kommandot `git clone`. Klona projektet med en `https://`-URL i stället för `ssh://`.

**Exempel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klona](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> För att utföra skrivåtgärder (`git push` till exempel) måste följande konfigurationskommandon köras för varje ny session. Observera också att eventuella push-kommandon kräver ett användarnamn och lösenord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nästa steg

När du är klar med kloningen av din databas kan du använda Git på samma sätt som du brukar göra på din lokala dator för att samarbeta med andra på bärbara datorer. Mer information om vad du kan göra i [!DNL JupyterLab] finns i [[!DNL JupyterLab user guide]](./overview.md).
