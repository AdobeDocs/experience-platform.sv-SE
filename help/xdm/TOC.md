---
product: experience-platform
audience: user
user-guide-title: Experience Data Model (XDM) - systemhjälp
breadcrumb-title: Datamodellguide (XDM)
user-guide-description: Använd XDM-klasser (Experience Data Model) och mixins för att standardisera upplevelsedata.
translation-type: tm+mt
source-git-commit: 0a5b6bab6a0a11a572a4cd5de95b33f8d61d34bc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 3%

---


# Experience Data Model (XDM) System {#xdm}

* [XDM - systemöversikt](home.md)
* Scheman {#schema}
   * [Grunderna för schemakomposition](schema/composition.md)
   * [Bästa tillvägagångssätt för datamodellering](schema/best-practices.md)
   * [Begränsningar för XDM-fälttyp](schema/field-constraints.md)
   * [XDM-fältordlista](schema/field-dictionary.md)
   * Användningsexempel för schema {#use-cases}
      * [Integritet och samtycke](schema/privacy-consent.md)
* Klasser {#classes}
   * [Individuell XDM-profil](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Blandningar {#mixins}
   * Profilinmixningar {#profile}
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
* API för schemaregister {#api}
   * [Komma igång](api/getting-started.md)
   * [Visa resurser](api/list-resources.md)
   * [Söka efter en resurs](api/look-up-resource.md)
   * [Uppdatera en resurs](api/update-resource.md)
   * [Ersätta en resurs](api/replace-resource.md)
   * [Ta bort en resurs](api/delete-resource.md)
   * [Skapa en klass](api/create-class.md)
   * [Skapa en blandning](api/create-mixin.md)
   * [Skapa en datatyp](api/create-data-type.md)
   * [Skapa ett schema](api/create-schema.md)
   * [Unions](api/unions.md)
   * [Beskrivningar](api/descriptors.md)
   * [Ad hoc-scheman](api/ad-hoc.md)
   * [Bilaga](api/appendix.md)
* Tutorials {#tutorials}
   * [Skapa ett schema (API)](tutorials/create-schema-api.md)
   * [Skapa ett schema (UI)](tutorials/create-schema-ui.md)
   * [Definiera en relation mellan två scheman (API)](tutorials/relationship-api.md)
   * [Definiera en relation mellan två scheman (UI)](tutorials/relationship-ui.md)
   * [Skapa ett ad hoc-schema (API)](tutorials/ad-hoc.md)
* [Felsökningsguide](troubleshooting-guide.md)
* [API-referens](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)