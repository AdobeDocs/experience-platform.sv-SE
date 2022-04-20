---
title: Fliken Sammanfattning
description: Lär dig hur du använder fliken Sammanfattning i Adobe Experience Platform Debugger.
keywords: felsökning;Experience Platform Debugger extension;chrome;extension;summary;clear;requests;summary screen;solution;information;analytics;target;dtm;målgruppshanterare;starta;id service
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: f94bba7eb4763230dae6794eb70a75f53a853c53
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 1%

---

# Fliken Sammanfattning

Om du vill köra Adobe Experience Platform Debugger öppnar du den sida du vill granska i webbläsaren och väljer sedan ikonen (![](images/start-icon.jpg)) i webbläsarfältet. Tillägget öppnas på **Sammanfattning** -fliken.

![](images/summary.jpg)

På den här skärmen visas information om varje Adobe Experience Cloud-lösning. Den information som visas varierar beroende på lösning, men innehåller vanligtvis information som lösningsbiblioteket och version (till exempel&quot;AppMeasurement v2.9&quot;) och kontoidentifierare (till exempel Analytics-rapportens programpaket-ID, målklientkoden, Audience Manager partner-ID osv.)

## Information som visas i felsökningsprogrammet för Experience Platform

Felsökaren i Experience Platform visar följande information för varje lösning:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Rapportsvit(er) </p> </td> 
   <td colname="col2"> <p>A <a href="https://experiencecloud.adobe.com/resources/help/en_US/reference/report_suites_admin.html" format="html" scope="external"> rapportsvit</a> definierar den fullständiga, oberoende rapporteringen på en vald webbplats, en uppsättning webbplatser eller en delmängd av webbsidor </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>The <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html" format="html" scope="external"> AppMeasurement</a> version definierad för sidan </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Besökarversion </p> </td> 
   <td colname="col2"> <p>Versionen av <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external"> besökar-ID</a> bibliotek. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Sidnamn </p> </td> 
   <td colname="col2"> <p>The <a href="https://experiencecloud.adobe.com/resources/help/en_US/sc/implement/pageName.html" format="html" scope="external"> pageName</a> variabel som skickas till Analytics som innehåller ett användarvänligt namn för webbplatsen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Moduler </p> </td> 
   <td colname="col2"> <p>Modulerna som läses in av Adobe Analytics </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Partner </p> </td> 
   <td colname="col2"> <p>The <a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_get_partner.html" format="html" scope="external"> partnernamn</a> för instansen DIL </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>The<a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/r_api_return_versions_dil.html" format="html" scope="external"> versionsnummer</a> för instansen DIL </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>The <a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/ids-in-aam.html" format="html" scope="external"> Unikt användar-ID</a> associerad med instansen DIL </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform-taggar**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Namn </p> </td> 
   <td colname="col2"> <p>Namnet på taggen <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> property</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Turbinversionen</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Skapad den </p> </td> 
   <td colname="col2"> <p>Taggen <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> bibliotek</a> byggdatum </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Miljö </p> </td> 
   <td colname="col2"> <p>The <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" format="https" scope="external"> miljö</a> som används av taggbiblioteket </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Tillägg </p> </td> 
   <td colname="col2"> <p>De tillägg som används på sidan </p> </td> 
  </tr> 
 </tbody> 
</table>

**Webb-SDK för Adobe Experience Platform**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Biblioteksversion </p> </td> 
   <td colname="col2"> <p>Antalet Adobe Experience Platform Web SDK <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-ext-release-notes.html" format="html" scope="external">biblioteksversion</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namnutrymme</p> </td> 
   <td colname="col2"> <p>Namnet som identifieras i tillägget</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Egenskaps-ID </p> </td> 
   <td colname="col2"> <p>Namnet på taggegenskapen som anges i tillägget </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Edge Domain </p> </td> 
   <td colname="col2"> <p>Domänen som Adobe Experience Platform-tillägget skickar och tar emot data från </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS-organisations-ID </p> </td> 
   <td colname="col2"> <p>Organisationen som du vill att data skickas till på Adobe, enligt vad som anges i tillägget </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Loggning aktiverad </p> </td> 
   <td colname="col2"> <p>Anger om loggning har aktiverats för den här egenskapen</p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Cloud ID-tjänst**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud organisation-ID </p> </td> 
   <td colname="col2"> <p>Dina <a href="https://experiencecloud.adobe.com/resources/help/en_US/mcvid/" format="https" scope="external"> Organisations-ID</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Versionen av<a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external"> besökar-ID</a> bibliotek </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Klientkod </p> </td> 
   <td colname="col2"> <p>Ditt mål <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> Klientkod </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Din nuvarande <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> eller mbox.js version </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namn på global begäran </p> </td> 
   <td colname="col2"> <p>The<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> global mbox</a> refererar till det enskilda serveranropet som görs högst upp på varje webbsida i Target-implementeringen </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Sidinläsningshändelse </p> </td> 
   <td colname="col2"> <p>Typ av <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html" format="html" scope="external">event</a> som utlöses när sidan läses in </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namn på begäran </p> </td> 
   <td colname="col2"> <p>Namnet på en begäran runt en <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> plats</a> på sidan. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Aktivitetsnamn </p> </td> 
   <td colname="col2"> <p>Namnet på målet <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> kampanj eller aktivitet</a>. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Aktivitets-ID </p> </td> 
   <td colname="col2"> <p>ID för målaktiviteten. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Experience Name </p> </td> 
   <td colname="col2"> <p>Namnet på målet <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> upplevelse</a>. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Experience ID </p> </td> 
   <td colname="col2"> <p>ID för Target-upplevelsen. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namn på erbjudande</p> </td> 
   <td colname="col2"> <p>Namnet på målet <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> erbjudande</a>. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Erbjudande-ID </p> </td> 
   <td colname="col2"> <p>ID:t för Target-erbjudandet. Endast tillgängligt utan autentisering om du implementerar händelseavlyssnaren för felsökning i koden eller tagghanteraren och aktiverar den nödvändiga <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> svarstoken</a> i målgränssnittet. </p> </td> 
  </tr> 
 </tbody> 
</table>
