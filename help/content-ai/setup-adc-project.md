---
title: Configuración de un proyecto de Adobe Developer Console para la IA de contenido de AEM
description: Obtenga información sobre cómo configurar un proyecto de Adobe Developer Console y autenticar llamadas de API a los servicios de inteligencia artificial aplicada al contenido de AEM mediante la autenticación de servidor a servidor o clave de API.
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: AEM Content AI, Adobe Developer Console, autenticación, servidor a servidor, clave de API, token de acceso
source-git-commit: 2ff1bbdd3ff224e2a6b389243c78af5fd228d5ee
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 2%

---


# Configuración de un proyecto de Adobe Developer Console {#configure-adc-project}

Para llamar a la API de servicios de inteligencia artificial aplicada al contenido de AEM, necesita las credenciales emitidas por un proyecto de Adobe Developer Console (ADC). Esta página le explica cómo crear el proyecto, seleccionar un método de autenticación y generar las credenciales que incluye con cada solicitud de API.

Vaya a [Adobe Developer Console](https://developer.adobe.com/console/) para que su organización comience.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de lo siguiente:

* Tiene acceso a [Adobe Developer Console](https://developer.adobe.com/console/) para su organización.
* Se le ha agregado como **Desarrollador** en el perfil de producto de los servicios de inteligencia artificial aplicada al contenido de AEM en **Adobe Admin Console**. Sin esta función, la tarjeta de API **[!UICONTROL AEM Content AI Services]** aparece deshabilitada y la opción de autenticación **[!UICONTROL Servidor a servidor]** está oculta.
* Conoce los números de programa y entorno del perfil de producto que desea seleccionar (por ejemplo, `AEM User - publish - Program 12345 - Environment 67890`).
* Usted tiene el rol de **[Administrador del sistema](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-admin-console/admin-roles)** en Admin Console para el programa. Esta función le permite administrar perfiles de producto y asignar usuarios al entorno.

## Elegir un método de autenticación {#choose-auth}

Los servicios de inteligencia artificial aplicada al contenido de AEM admiten dos métodos de autenticación. Elija el que coincida con su integración:

| Método | Ideal para |
| --- | --- |
| [Servidor a servidor](#s2s-auth) | Servicios back-end que llaman a la API sin interacción del usuario. Devuelve un token de acceso de corta duración. |
| [Clave API](#api-key-auth) | Integraciones del lado del cliente o basadas en explorador que llaman directamente a la API de. Devuelve una clave de larga duración con ámbitos de dominios permitidos. |

## Autenticación de servidor a servidor {#s2s-auth}

1. Seleccione **[!UICONTROL API y servicios]**, luego **[!UICONTROL API]**.

   ![Developer Console muestra API y servicios](../assets/e2e-env-setup-28.png)

1. Filtre por **Servicios de inteligencia artificial aplicada al contenido de AEM** y, a continuación, seleccione **[!UICONTROL Crear proyecto]** para iniciar un nuevo proyecto o **[!UICONTROL Agregar API]** si agrega el servicio a un proyecto existente.

   >[!NOTE]
   >
   >Si la tarjeta API está deshabilitada con el mensaje &quot;Se requiere licencia&quot;, es posible que el entorno de AEM as a Cloud Service no se actualice. Consulte [Modernización del entorno de AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#modernization-of-aem-as-a-cloud-service-environment).

1. En el cuadro de diálogo **[!UICONTROL Configurar API]**, seleccione la autenticación de **[!UICONTROL servidor a servidor]**.

   ![Cuadro de diálogo Configurar API con selección de servidor a servidor](../assets/e2e-env-setup-29.png)

   >[!TIP]
   >
   >Si la opción Servidor a servidor no está disponible, el usuario que configura la integración no se agrega como Desarrollador al Perfil del producto. Consulte [Habilitar la autenticación de servidor a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

1. Si es necesario, cambie el nombre de la credencial. Seleccione **[!UICONTROL Siguiente]**.

   ![Paso de Adobe Developer Console para cambiar el nombre de la nueva credencial de servidor a servidor antes de seleccionar Siguiente](../assets/e2e-env-setup-30.png)

1. Seleccione el perfil de producto **[!UICONTROL Usuario de AEM - publicar - Programa XXX - Entorno XXX]** y/o **[!UICONTROL Usuario de AEM - autor - Programa XXX - Entorno XXX]** y, a continuación, seleccione **[!UICONTROL Guardar]**.

   ![Selector de perfil de producto que muestra los perfiles de publicación y creación de usuarios de AEM para el programa y el entorno de destino](../assets/e2e-env-setup-31.png)

1. Revise la configuración de la API y la autenticación.

   ![Pantalla de revisión que resume la API, el tipo de autenticación y el nombre de credencial seleccionados](../assets/e2e-env-setup-33.png)

   ![Revise los detalles de pantalla que muestran los perfiles de producto asignados para la credencial](../assets/e2e-env-setup-34.png)

### Generar un token de acceso {#generate-token}

1. En su proyecto ADC, vaya a **[!UICONTROL Credenciales]** y seleccione **[!UICONTROL Generar token de acceso]**.

   ![Página de credenciales con el botón Generar token de acceso resaltado](../assets/e2e-env-setup-32.png)

1. Incluya el token en el encabezado `Authorization` de cada solicitud de API:

   ```http
   Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

   >[!WARNING]
   >
   >Guarde el token de forma segura. Caduca y debe regenerarse periódicamente.

## Autenticación de clave API {#api-key-auth}

1. Al agregar la API de AEM Content AI Services a su proyecto, seleccione **[!UICONTROL Clave de API]** en el cuadro de diálogo **[!UICONTROL Seleccionar tipo de autenticación]**.

   ![Seleccionar tipo de autenticación de clave API](../assets/onboarding-api-key-01.png)

1. Confirme la credencial de la clave API.

   ![Agregar credencial de clave API](../assets/onboarding-api-key-02.png)

1. Para restringir qué orígenes pueden utilizar la clave, configure los dominios permitidos.

   ![Configurar dominios permitidos](../assets/onboarding-api-key-03.png)

1. Su clave API (ID de cliente) aparece en **[!UICONTROL Credenciales conectadas]**. Seleccione **[!UICONTROL Copiar]**.

   ![Copiar clave API de las credenciales conectadas](../assets/onboarding-api-key-04.png)

1. Incluya la clave en cada solicitud de API:

   ```http
   x-api-key: YOUR_API_KEY
   ```

   El proyecto ya está listo. Utilice la clave con cada solicitud a los servicios de IA de contenido de AEM.

## Próximos pasos {#next-steps}

* [Controle sus fuentes de contenido](contentsources.md) - Configure una fuente de contenido en Cloud Manager y la adquisición de déclencheur.
* [Referencia de API de inteligencia artificial aplicada al contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/): use su token de acceso o clave de API para consultar el contenido indizado.
