---
product: experience-platform
audience: user
user-guide-title: Experience Data Model (XDM) - systemhjälp
breadcrumb-title: XDM-guide (Experience Data Model)
user-guide-description: Använd XDM-klasser (Experience Data Model) och mixins för att standardisera upplevelsedata.
translation-type: tm+mt
source-git-commit: 099e88373d945660e7529bbd508e616869fd01da
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 6%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM - systemöversikt](home.md)
* Scheman {#schema}
   * [Grunderna för schemakomposition](schema/composition.md)
   * [Bästa tillvägagångssätt för datamodellering](schema/best-practices.md)
   * [Begränsningar för XDM-fälttyp](schema/field-constraints.md)
   * [XDM-fältordlista](schema/field-dictionary.md)
   * Användningsexempel för schema {#use-cases}
      * [Datatypen Innehåll och inställningar](schema/privacy-consent.md)
* Klasser {#classes}
   * [Individuell XDM-profil](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Blandningar {#mixins}
   * Profilblandningar {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Demografiska detaljer](./mixins/profile/person-details.md)
      * [Kontaktinformation, privat](./mixins/profile/personal-details.md)
      * [Information om segmentmedlemskap](./mixins/profile/segmentation.md)
      * [Kontaktinformation, arbete](./mixins/profile/work-details.md)
   * Händelseblandningar {#event}
      * [Information om slutanvändar-ID](./mixins/event/enduserids.md)
      * [Miljöinformation](./mixins/event/environment-details.md)
   * [Uppdateringar av blandade namn](./mixins/name-updates.md)
* Datatyper {#data-types}
   * [Beacon](./data-types/beacon.md)
   * [Webbläsarinformation](./data-types/browser-details.md)
   * [Innehåll och inställningar](./data-types/consents.md)
   * [Enhet](./data-types/device.md)
   * [E-postadress](./data-types/email-address.md)
   * [Miljö](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Geo Circle](./data-types/geo-circle.md)
   * [Geokoordinater](./data-types/geo-coordinates.md)
   * [Info om geo-interaktion](./data-types/geo-interaction-details.md)
   * [Geo Shape](./data-types/geo-shape.md)
   * [Identitet](./data-types/identity.md)
   * [Personnamn](./data-types/person-name.md)
   * [Telefonnummer](./data-types/phone-number.md)
   * [Montera kontext](./data-types/place-context.md)
   * [POI-information](./data-types/poi-details.md)
   * [POI-interaktion](./data-types/poi-interaction.md)
   * [Postadress](./data-types/postal-address.md)
* [!UICONTROL Schemas] UI  {#ui}
   * [Översikt](./ui/overview.md)
   * [Utforska XDM-resurser](./ui/explore.md)
   * Skapa och redigera resurser {#resources}
      * [Scheman](./ui/resources/schemas.md)
      * [Klasser](./ui/resources/classes.md)
      * [Blandningar](./ui/resources/mixins.md)
      * [Datatyper](./ui/resources/data-types.md)
   * Definiera fält {#fields}
      * [Översikt](./ui/fields/overview.md)
      * [Obligatoriska fält](./ui/fields/required.md)
      * [Objektfält](./ui/fields/object.md)
      * [Matrisfält](./ui/fields/array.md)
      * [Uppräkningsfält](./ui/fields/enum.md)
      * [Identitetsfält](./ui/fields/identity.md)
      * [Relationsfält](./ui/fields/relationship.md)
* API för schemaregister {#api}
   * [Översikt](api/overview.md)
   * [Komma igång](api/getting-started.md)
   * [Scheman](api/schemas.md)
   * [Beteenden](api/behaviors.md)
   * [Klasser](api/classes.md)
   * [Blandningar](api/mixins.md)
   * [Datatyper](api/data-types.md)
   * [Beskrivningar](api/descriptors.md)
   * [Unions](api/unions.md)
   * [Ad hoc-scheman](api/ad-hoc.md)
   * [Bilaga](api/appendix.md)
* Självstudiekurser {#tutorials}
   * [Skapa ett schema (API)](tutorials/create-schema-api.md)
   * [Skapa ett schema (UI)](tutorials/create-schema-ui.md)
   * [Definiera en relation mellan två scheman (API)](tutorials/relationship-api.md)
   * [Definiera en relation mellan två scheman (UI)](tutorials/relationship-ui.md)
   * [Skapa ett ad hoc-schema (API)](tutorials/ad-hoc.md)
* [Felsökningsguide](troubleshooting-guide.md)
* [API-referens](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)