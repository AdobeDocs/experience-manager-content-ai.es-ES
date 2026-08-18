---
title: Introducción a la Búsqueda por IA de contenido de AEM
description: 'Esta guía explica cómo habilitar la búsqueda en el sitio con la inteligencia artificial aplicada al contenido: conecte el contenido y, a continuación, elija un componente de búsqueda para presentarlo a los visitantes.'
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: AEM Content AI, Búsqueda por IA de contenido de AEM, GenSearch, Búsqueda rápida, Fuentes de inteligencia artificial aplicada al contenido, Adquisición, Cloud Manager
source-git-commit: 51fa66b5ac0ef77e438db76530788826da65f91e
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 6%

---


# Introducción a la Búsqueda por IA de contenido de AEM

La búsqueda tradicional del sitio hace coincidir las palabras que escribe un visitante con las palabras del contenido. Funciona bien cuando los visitantes utilizan la misma terminología que el contenido, pero se desglosa en el momento en que hacen una pregunta, expresan una intención o simplemente formulan las cosas de forma diferente. La búsqueda es una de las señales más claras de la intención del visitante en un sitio, por lo que una coincidencia fallida a menudo significa un recorrido fallido: el contenido no se descubre, la participación cae y las conversiones se pierden. Los visitantes esperan cada vez más que la búsqueda entienda lo que significan, no solo lo que escriben, y esa misma base consciente de la intención es lo que hace posibles las respuestas generativas en primer lugar.

La Búsqueda por IA de contenido de AEM no reemplaza la experiencia de búsqueda del sitio, sino que la desarrolla, desde palabras clave coincidentes, hasta la comprensión del significado y la intención, pasando por la respuesta directa a preguntas. La búsqueda semántica agrega recuperación según la intención sobre la experiencia de búsqueda existente, y muestra contenido relevante incluso cuando una consulta no comparte la redacción exacta del contenido. La búsqueda generativa se basa en la misma base de recuperación para producir respuestas contextuales generadas basadas en el contenido propio del sitio, un paso distinto, no lo mismo que la recuperación semántica.

Para los visitantes, esto significa una mejor relevancia, compatibilidad con lenguajes naturales, menos búsquedas de resultados cero y respuestas más rápidas. Para su empresa, significa una mejor coincidencia de intenciones, una detección de contenido más sólida y una base de búsqueda compatible con IA, sin tener que reconstruir su experiencia de búsqueda desde cero. Para su equipo, se trata de una actualización incremental: el componente de búsqueda existente puede pasar de lo léxico, a lo semántico, a las capacidades generativas paso a paso, en lugar de requerir una implementación completamente nueva.

Llegar allí se reduce a dos decisiones: cómo se introduce el contenido en la inteligencia artificial aplicada al contenido y qué componente lo lleva a los visitantes. Conecte el contenido y, a continuación, añada un componente de búsqueda a una página; el sitio estará listo para ofrecer a los visitantes los resultados y las respuestas por intención más relevantes.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que cumple las siguientes condiciones:

* Dispone de un programa de Cloud Manager activo con al menos un entorno de AEM as a Cloud Service.
* El usuario está asignado al perfil de producto **[!UICONTROL Usuarios de AEM]** (para ver fuentes de contenido) o a **[!UICONTROL Administradores de AEM]** (para crearlos y editarlos), asignados al nivel **publicar**: la inteligencia artificial aplicada al contenido indexa contenido publicado, no contenido creado. Consulte [Asignar un usuario a un perfil de producto de AEM](contentsources.md#assign-product-profile) para ver el procedimiento completo.
* El perfil de producto del entorno se ha aprovisionado en **Adobe Admin Console**.

>[!NOTE]
>
>El acceso a Cloud Manager por sí solo no es suficiente. Un usuario también necesita un perfil de producto de AEM asignado en el nivel de publicación para ver o administrar fuentes de contenido.

## Paso 1a: Conexión de un índice existente {#option-a}

Los índices de repositorio existentes aparecen automáticamente en la lista Fuentes de contenido como Source Type AEM, según lo que indizan, como Páginas, Assets o Fragmentos de contenido. Empiezan **Restringido** y bloqueado; aún no se puede buscar a través de la inteligencia artificial aplicada al contenido.

1. Inicie sesión en [Cloud Manager](https://my.cloudmanager.adobe.com/), seleccione su programa y abra la pestaña **[!UICONTROL Configuración de inteligencia artificial aplicada al contenido]** para el entorno que desea configurar.
1. Busque el origen con el que desea buscar (por ejemplo, **Páginas**) y seleccione su icono de candado. Solo los usuarios con el perfil de producto **[!UICONTROL Administradores de AEM]** pueden hacer esto: **[!UICONTROL Usuarios de AEM]** pueden ver orígenes de contenido, no cambiar su capacidad de búsqueda.
1. ¿Desea leer **Hacer que el origen se pueda buscar?** dialogar cuidadosamente. Advierte que las listas de control de acceso (ACL) de Apache Oak no se forzarán para este índice una vez que se pueda buscar: cualquier usuario autenticado podrá recuperar todo su contenido. Compruebe **Entiendo que no se aplican los controles de acceso (ACL) y que se podrá buscar en todo el contenido de este origen**. A continuación, seleccione **Permitir la búsqueda**.
1. Confirme los cambios de estado en **Disponible**. Un icono de advertencia permanece junto al origen como recordatorio permanente de que las ACL se omiten para él.
1. Ejecute una búsqueda de prueba para comprobar que los resultados regresan correctamente.

>[!WARNING]
>
>Al hacer que un índice existente se pueda buscar de esta manera, se evitan por completo las ACL de Apache Oak para ese origen: cualquier usuario autenticado puede recuperar todo su contenido mediante la búsqueda, independientemente de sus permisos normales de repositorio. Solo haz esto para las fuentes que te sientas cómodo exponiendo en su totalidad.

>[!NOTE]
>
>Esta ruta es adecuada si ya tiene un índice con el contenido del sitio, por ejemplo, el contenido de la página. Utilice ese índice en lugar de configurar un mecanismo de rastrea independiente.

## Paso 1b: Rastrear un sitio web {#option-b}

Utilice esta ruta si aún no tiene un índice de búsqueda para el sitio. El propio rastreador de la inteligencia artificial aplicada al contenido crea y actualiza uno para usted. Este proceso de rastrea también se denomina **adquisición** en Cloud Manager y en esta guía.

1. Abra la ficha **[!UICONTROL Configuración de inteligencia artificial aplicada al contenido]**, igual que en el paso 1a.
1. Seleccione **[!UICONTROL Crear Source]** y rellene los campos. Solo los usuarios con el perfil de producto **[!UICONTROL Administradores de AEM]** pueden agregar nuevas fuentes de contenido.

   | Campo | Descripción |
   | --- | --- |
   | **[!UICONTROL Nombre de configuración de la inteligencia artificial aplicada al contenido]** | Un identificador único para este origen. No se puede cambiar después de la creación. |
   | **[!UICONTROL Dirección del sitio web]** | Dirección URL raíz que se rastreará, por ejemplo `https://www.example.com/`. |
   | **[!UICONTROL Excluir URL]** | *(Opcional)* Patrones de URL que se deben omitir durante el rastreo. |
   | **[!UICONTROL Frecuencia de actualización]** | Semanal, Diario, Diario 4×, 60 Min o 15 Min. |

1. Seleccione **[!UICONTROL Crear fuente]**. La adquisición se inicia automáticamente y la fuente pasa a **Indexación**.
1. Supervise el estado hasta que alcance **Disponible**:

   | Estado | Significado |
   | --- | --- |
   | **Nuevo** | Source acaba de crearse; la adquisición automática aún no ha comenzado. |
   | **Indexación** | Rastrea e indexación en curso. |
   | **Disponible** | Indexación completa: lista para servir consultas de búsqueda. |

1. Seleccione el icono **search** junto al origen y ejecute una consulta de prueba para confirmar que el contenido se ha indexado correctamente.

>[!CAUTION]
>
>¿Hay una fuente atascada en **[!UICONTROL Indexando]**? Reintente primero la adquisición desde el menú (...). Si sigue sin avanzar, confirma que la dirección del sitio web se puede acceder públicamente y que los patrones de **[!UICONTROL Excluir URL]** no filtran todas las páginas.

## Paso 2: Selección de un componente de búsqueda {#choose-component}

Existen dos componentes que pueden colocar la búsqueda en una página, creados sobre diferentes bases:

| | Búsqueda rápida (v3) con búsqueda semántica | Búsqueda por IA de contenido de AEM |
| --- | --- | --- |
| Foundation | Componente principal Búsqueda rápida existente, actualizado a la versión 3 | Nuevo componente independiente: llama directamente a las API de inteligencia artificial aplicada al contenido |
| Origen de contenido | El contenido del sitio existente, que ya está en un índice, se ha enriquecido para la coincidencia semántica | Una Source de inteligencia artificial aplicada al contenido (paso 1a o 1b) |
| Respuesta generativa | No: mejora solo la calidad de coincidencia de la lista de resultados existente | Sí: resumen opcional generado por IA con fuentes y una exención de responsabilidad |
| Mejor ajuste | Sitios que ya utilizan la búsqueda rápida y que desean una actualización más ligera e incremental | El componente sugerido para toda la gama de capacidades de IA de contenido: búsqueda semántica, búsqueda generativa y búsqueda de lenguaje natural (NLS) |

## Búsqueda rápida (v3) con búsqueda semántica {#quicksearch}

Si el sitio ya usa el componente de búsqueda rápida [!DNL AEM], la versión 3 agrega una opción de inclusión **Búsqueda por IA** que los visitantes pueden activar; no se requiere ningún componente nuevo, proxy o Source de contenido.

* La búsqueda sigue ejecutándose a través de la misma ruta JCR/QueryBuilder que hoy: nada cambia en el servlet de resultados ni en cómo se representan los resultados.
* Cuando un visitante habilita la opción, el componente prefija la consulta con un marcador especial que la enruta a la coincidencia semántica en lugar de a texto completo de palabra clave sin formato.
* No hay un resumen de respuestas generativas en esta ruta. Mejora la calidad de la coincidencia de la lista de resultados existente; no agrega una respuesta de IA generativa.
* **El paso 1 (incorporación de inteligencia artificial aplicada al contenido) no se aplica a esta ruta.** No hay ningún Source de contenido para crear o conectar: este componente consulta directamente el índice de página existente.

>[!NOTE]
>
>Si la búsqueda semántica no funciona como se espera después de habilitar la opción, genere un ticket de asistencia.

Esta ruta es adecuada si desea una actualización de búsqueda semántica incremental sin adoptar un nuevo componente o fuentes de contenido. No es la ruta correcta si desea una experiencia de respuesta generativa; para ello, utilice la Búsqueda por IA de contenido de AEM.

## Búsqueda por IA de contenido de AEM {#gensearch}

La Búsqueda por IA de contenido de AEM es un componente principal [!DNL AEM] que permite a los visitantes buscar un Source de contenido directamente desde una página, con capacidades de búsqueda semántica y generativa.

>[!VIDEO](https://video.tv.adobe.com/v/3497308)

>[!NOTE]
>
>Las funciones de búsqueda generativa se adquieren por separado mediante un SKU de IA. Póngase en contacto con su representante de ventas de Adobe para habilitarlo en su cuenta.

### Requisitos previos {#gensearch-prerequisites}

* [!DNL AEM] componentes principales instalados en el proyecto.
* Al menos un Source de contenido ya se creó y está en estado **Disponible**.
* La configuración OSGi **Cliente de inteligencia artificial aplicada al contenido de AEM** (`ContentAIClientImpl`) se configuró en Autor y Publicación, con una credencial de API válida y un Source de contenido predeterminado.

Para obtener la guía de configuración completa (poner el componente a disposición de los autores, conectar su biblioteca de cliente y configurar el cuadro de diálogo), consulte la [documentación de componentes principales](https://www.adobe.com/go/aem_cmp_library_es).

## ¡Felicitaciones! {#congratulations}

Ha configurado correctamente sus capacidades de búsqueda semántica y generativa.

>[!VIDEO](https://video.tv.adobe.com/v/3497306)

## Siguientes pasos {#next-steps}

* [Configurar un proyecto de Adobe Developer Console](setup-adc-project.md): cree el proyecto de ADC y las credenciales que necesita para llamar directamente a la API de inteligencia artificial aplicada al contenido.
* [Referencia de la API de inteligencia artificial aplicada al contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/): consulte el contenido indizado mediante puntos finales de búsqueda semánticos, generativos o híbridos.
* [Documentación de componentes principales](https://www.adobe.com/go/aem_cmp_library_es): más información sobre componentes proxy y directivas de plantilla.
