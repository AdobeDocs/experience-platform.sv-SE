---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;Git;Github
solution: Experience Platform
title: Samarbeta i JupyterLab med Git
type: Tutorial
description: Git är ett distribuerat versionshanteringssystem för att spåra ändringar i källkoden under programvaruutvecklingen. Git är förinstallerat i Data Science Workspace JupyterLab-miljön.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# Samarbeta i [!DNL JupyterLab] med [!DNL Git]

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

[!DNL Git] är ett distribuerat versionskontrollsystem för att spåra ändringar i källkoden under programvaruutveckling. Git är förinstallerat i miljön [!DNL Data Science Workspace JupyterLab].

## Förhandskrav

>[!NOTE]
>
> Den Git-server du tänker använda måste vara tillgänglig via Internet.

Miljön [!DNL Data Science Workspace JupyterLab] är en värdmiljö som inte har distribuerats inom företagets brandvägg, och därför måste den Git-server som du ansluter till vara tillgänglig från det offentliga Internet. Detta kan vara en offentlig eller privat databas på [GitHub](https://github.com/) eller en annan instans av en [!DNL Git]-server som du har bestämt att vara värd för själv.

## Anslut [!DNL Git] till miljön [!DNL Data Science Workspace JupyterLab Notebooks]

Starta [!DNL Adobe Experience Platform] och navigera till [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)-miljön.

I [!DNL JupyterLab] väljer du **[!UICONTROL File]** och håller pekaren över **[!UICONTROL New]**. Välj **[!UICONTROL Terminal]** i listrutan som visas.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Navigera sedan till arbetsytan i *Terminal* med följande kommando: `cd my-workspace`.

![arbetsytan för cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Om du vill visa en lista över tillgängliga Git-kommandon skickar du kommandot `git -help` i terminalen.

Sedan klonar du den databas du vill använda med kommandot `git clone`. Klona projektet med en `https://`-URL i stället för `ssh://`.

**Exempel**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![klon](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> För att kunna utföra skrivåtgärder (`git push` till exempel) måste följande konfigurationskommandon köras för varje ny session. Observera också att eventuella push-kommandon kräver ett användarnamn och lösenord.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Nästa steg

När du är klar med kloningen av din databas kan du använda Git på samma sätt som du brukar göra på din lokala dator för att samarbeta med andra på bärbara datorer. Mer information om vad du kan göra inom [!DNL JupyterLab] finns i [[!DNL JupyterLab user guide]](./overview.md).
