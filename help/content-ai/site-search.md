---
title: Introducción a la búsqueda por inteligencia artificial aplicada al contenido de AEM
description: 'Esta guía explica cómo habilitar la búsqueda en el sitio con la inteligencia artificial aplicada al contenido: conecte el contenido y, a continuación, elija un componente de búsqueda para presentarlo a los visitantes.'
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: Inteligencia artificial aplicada al contenido de AEM, Búsqueda por inteligencia artificial aplicada al contenido de AEM, GenSearch, Búsqueda rápida, Fuentes de inteligencia artificial aplicada al contenido, Adquisición, Cloud Manager
source-git-commit: 51fa66b5ac0ef77e438db76530788826da65f91e
workflow-type: ht
source-wordcount: '1487'
ht-degree: 100%

---


# Introducción a la búsqueda por inteligencia artificial aplicada al contenido de AEM

La búsqueda tradicional del sitio hace coincidir las palabras que escribe un visitante con las palabras del contenido. Funciona bien cuando los visitantes utilizan la misma terminología que el contenido, pero falla en el momento en que hacen una pregunta, expresan una intención o simplemente formulan las cosas de forma diferente. La búsqueda es una de las señales más claras de la intención del visitante en un sitio, por lo que una coincidencia infructuosa a menudo implica un recorrido fallido: el contenido no se descubre, la participación cae y las conversiones se pierden. Los visitantes esperan cada vez más que la búsqueda entienda lo que quieren decir, no solo lo que escriben, y esa misma base que toma en cuenta la intención es lo que hace posible, en primer lugar, las respuestas generativas.

La búsqueda por inteligencia artificial aplicada al contenido de AEM no reemplaza la experiencia de búsqueda del sitio, sino que la mejora: pasa de la simple coincidencia de palabras clave a comprender el significado y la intención, y a responder preguntas directamente. La búsqueda semántica incorpora una función de recuperación basada en la intención a la experiencia de búsqueda actual, mostrando contenido relevante incluso cuando la consulta no coincide exactamente con el texto del contenido. La búsqueda generativa aprovecha la misma base de recuperación para producir respuestas contextuales generadas basadas en el contenido propio del sitio; se trata de un paso distinto, no es lo mismo que la recuperación semántica.

Para los visitantes, esto implica mayor relevancia, compatibilidad con lenguajes naturales, menos búsquedas de resultados cero y respuestas más rápidas. Para su empresa, supone mejor coincidencia de intenciones, una detección de contenido más sólida y una base de búsqueda compatible con IA, sin tener que reconstruir su experiencia de búsqueda desde cero. Para su equipo, se trata de una actualización incremental: el componente de búsqueda existente puede pasar de lo léxico a lo semántico y a las capacidades generativas paso a paso, en lugar de requerir una implementación completamente nueva.

La llegada a dicho punto se reduce a dos decisiones: cómo se introduce el contenido en la inteligencia artificial aplicada al contenido y qué componente lo lleva a los visitantes. Conecte el contenido y, a continuación, agregue un componente de búsqueda a una página; el sitio estará listo para ofrecer a los visitantes los resultados y las respuestas por intención más relevantes.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que cumple las siguientes condiciones:

* Dispone de un programa de Cloud Manager activo con al menos un entorno de AEM as a Cloud Service.
* El usuario está asignado al perfil de producto **[!UICONTROL Usuarios de AEM]** (para ver fuentes de contenido) o a **[!UICONTROL Administradores de AEM]** (para crearlos y editarlos), asignados al nivel **publicar**: la inteligencia artificial aplicada al contenido indexa contenido publicado, no contenido creado. Consulte [Asignar un usuario a un perfil de producto de AEM](contentsources.md#assign-product-profile) para ver todo el proceso.
* El perfil de producto del entorno se ha proporcionado en **Adobe Admin Console**.

>[!NOTE]
>
>El acceso a Cloud Manager por sí solo no es suficiente. Un usuario también necesita un perfil de producto de AEM asignado en el nivel de publicación para ver o administrar fuentes de contenido.

## Paso 1a: Conexión de un índice existente {#option-a}

Los índices de repositorio existentes aparecen de forma automática en la lista Fuentes de contenido como Source Type AEM, según lo que indizan, como Páginas, Recursos o Fragmentos de contenido. Empiezan en **Restringido** y bloqueado; aún no se pueden buscar a través de la inteligencia artificial aplicada al contenido.

1. Inicie sesión en [Cloud Manager](https://my.cloudmanager.adobe.com/), seleccione su programa y abra la pestaña **[!UICONTROL Configuración de inteligencia artificial aplicada al contenido]** para el entorno que desea configurar.
1. Busque la fuente con la que desea buscar (por ejemplo, **Páginas**) y seleccione su icono de candado. Solo los usuarios con el perfil de producto **[!UICONTROL Administradores de AEM]** pueden hacer esto: los **[!UICONTROL Usuarios de AEM]** pueden ver fuentes de contenido, no cambiar su capacidad de búsqueda.
1. ¿Desea leer **Hacer que la fuente se pueda buscar?** dialogar con cuidado. Advierte que las listas de control de acceso (ACL) de Apache Oak no se aplicarán a este índice una vez que se pueda buscar: cualquier usuario autenticado podrá recuperar todo su contenido. Marque **Entiendo que no se aplican los controles de acceso (ACL) y que se podrá buscar en todo el contenido de esta fuente**. A continuación, seleccione **Permitir la búsqueda**.
1. Confirme los cambios de estado en **Disponible**. Un icono de advertencia permanece junto a la fuente como recordatorio permanente de que las ACL se omiten en su caso.
1. Ejecute una búsqueda de prueba para comprobar que los resultados sean correctos.

>[!WARNING]
>
>Al hacer que un índice existente se pueda buscar de esta manera, se evitan por completo las ACL de Apache Oak para dicha fuente: cualquier usuario autenticado puede recuperar todo su contenido mediante la búsqueda, independientemente de sus permisos normales de repositorio. Haga esto únicamente en el caso de las fuentes que no le importe exponer en su totalidad.

>[!NOTE]
>
>Esta ruta es adecuada si ya tiene un índice con el contenido del sitio, como por ejemplo, el contenido de la página. Utilice dicho índice en lugar de configurar un mecanismo de rastreo independiente.

## Paso 1b: Rastrear un sitio web {#option-b}

Utilice esta ruta si aún no tiene un índice de búsqueda para el sitio. El propio rastreador de la inteligencia artificial aplicada al contenido crea y actualiza uno para usted. Este proceso de rastreo también se denomina **adquisición** en Cloud Manager y en esta guía.

1. Abra la pestaña **[!UICONTROL Configuración de la inteligencia artificial aplicada al contenido]**, al igual que en el Paso 1a.
1. Seleccione **[!UICONTROL Crear fuente]** y rellene los campos. Solo los usuarios con el perfil de producto **[!UICONTROL Administradores de AEM]** pueden agregar nuevas fuentes de contenido.

   | Campo | Descripción |
   | --- | --- |
   | **[!UICONTROL Nombre de configuración de la inteligencia artificial aplicada al contenido]** | Un identificador único para esta fuente. No se puede cambiar después de la creación. |
   | **[!UICONTROL Dirección del sitio web]** | URL raíz que se va a rastrear, por ejemplo `https://www.example.com/`. |
   | **[!UICONTROL Excluir URL]** | *(Opcional)* Patrones de URL que se deben omitir durante el rastreo. |
   | **[!UICONTROL Frecuencia de actualización]** | Semanal, Diario, Diario 4×, 60 min o 15 min. |

1. Seleccione **[!UICONTROL Crear fuente]**. La adquisición se inicia automáticamente y la fuente pasa a **Indexación**.
1. Monitorice el estado hasta que alcance **Disponible**:

   | Estado | Significado |
   | --- | --- |
   | **Nuevo** | La fuente se acaba de crear; la adquisición automática aún no ha comenzado. |
   | **Indexación** | Rastreo e indexación en curso. |
   | **Disponible** | Indexación completa: lista para servir consultas de búsqueda. |

1. Seleccione el icono de **búsqueda** situado junto a la fuente y ejecute una consulta de prueba para confirmar que el contenido se ha indexado de forma correcta.

>[!CAUTION]
>
>¿Hay una fuente atascada en la **[!UICONTROL Indexación]**? Vuelva a intentar la adquisición desde el menú (...). Si sigue sin avanzar, confirme que la dirección del sitio web sea accesible de forma pública y que los patrones de **[!UICONTROL Excluir URL]** no filtren todas las páginas.

## Paso 2: Selección de un componente de búsqueda {#choose-component}

Existen dos componentes que pueden colocar la búsqueda en una página, creados sobre diferentes bases:

| | Búsqueda rápida (v3) con búsqueda semántica | Búsqueda de inteligencia artificial aplicada al contenido de AEM |
| --- | --- | --- |
| Foundation | Componente principal de búsqueda rápida existente, actualizado a la versión 3 | Nuevo componente independiente: llama directamente a las API de inteligencia artificial aplicada al contenido |
| Origen del contenido | El contenido del sitio existente, que ya está en un índice, se ha enriquecido para la coincidencia semántica | Una fuente de inteligencia artificial aplicada al contenido (Paso 1a o 1b) |
| Respuesta generativa | No: mejora solo la calidad de coincidencia de la lista de resultados existente | Sí: resumen opcional generado por IA con fuentes y una exención de responsabilidad |
| Mejor ajuste | Sitios que ya utilizan la búsqueda rápida y que desean una actualización más ligera e incremental | El componente sugerido para toda la gama de capacidades de inteligencia artificial aplicada al contenido: búsqueda semántica, búsqueda generativa y búsqueda de lenguaje natural (NLS) |

## Búsqueda rápida (v3) con búsqueda semántica {#quicksearch}

Si el sitio ya usa el clásico componente de búsqueda rápida [!DNL AEM], la versión 3 agrega una opción de inclusión de **Búsqueda por IA** que los visitantes pueden activar; no se requiere ningún componente nuevo, proxy o fuente de contenido.

* La búsqueda sigue ejecutándose a través de la misma ruta JCR/QueryBuilder que hoy: nada cambia en el servlet de resultados ni en cómo se representan los resultados.
* Cuando un visitante habilita la opción, el componente prefija la consulta con un marcador especial que la enruta a la coincidencia semántica en lugar de a texto completo de palabra clave sin formato.
* No hay un resumen de respuestas generativas en esta ruta. Mejora la calidad de la coincidencia de la lista de resultados existente; no agrega una respuesta de IA generativa.
* **El paso 1 (Incorporación de inteligencia artificial aplicada al contenido) no se aplica a esta ruta.** No hay ninguna fuente de contenido para crear o conectar: este componente consulta directamente el índice de página existente.

>[!NOTE]
>
>Si la búsqueda semántica no funciona como se espera después de habilitar la opción, genere un ticket de asistencia.

Esta ruta es adecuada si desea una actualización de búsqueda semántica incremental sin adoptar un nuevo componente o fuentes de contenido. No es la ruta correcta si desea una experiencia de respuesta generativa; para ello, utilice la Búsqueda por inteligencia artificial aplicada al contenido de AEM.

## Búsqueda de inteligencia artificial aplicada al contenido de AEM {#gensearch}

La Búsqueda por inteligencia artificial aplicada al contenido de AEM es un componente principal [!DNL AEM] que permite a los visitantes buscar una fuente de contenido directamente desde una página, con capacidades de búsqueda semántica y generativa.

>[!VIDEO](https://video.tv.adobe.com/v/3497308)

>[!NOTE]
>
>Las funciones de búsqueda generativa se adquieren por separado mediante una SKU de IA. Póngase en contacto con su representante de ventas de Adobe para habilitarlo en su cuenta.

### Requisitos previos {#gensearch-prerequisites}

* [!DNL AEM] componentes principales instalados en el proyecto.
* Al menos una fuente de contenido ya se creó y se encuentra en estado **Disponible**.
* La configuración OSGi **Cliente de inteligencia artificial aplicada al contenido de AEM** (`ContentAIClientImpl`) se configuró en Autor y Publicación, con una credencial de API válida y una fuente de contenido predeterminada.

Para obtener la guía de configuración completa (poner el componente a disposición de los autores, conectar su biblioteca de cliente y configurar el cuadro de diálogo), consulte la [Documentación de componentes principales](https://www.adobe.com/go/aem_cmp_library_es).

## ¡Felicitaciones! {#congratulations}

Ha configurado correctamente sus capacidades de búsqueda semántica y generativa.

>[!VIDEO](https://video.tv.adobe.com/v/3497306)

## Siguientes pasos {#next-steps}

* [Configuración de un proyecto de Adobe Developer Console](setup-adc-project.md): cree el proyecto de ADC y las credenciales necesarias para llamar a la API de inteligencia artificial aplicada al contenido de forma directa.
* [Referencia de API de la inteligencia artificial aplicada al contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/): realice consultas del contenido indexado mediante puntos finales de búsqueda semántica, de texto completo o híbrida.
* [Documentación de componentes principales](https://www.adobe.com/go/aem_cmp_library_es): más información sobre componentes proxy y directivas de plantilla.
