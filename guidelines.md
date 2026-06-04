---
source-git-commit: 70812e4c8dc3865402c97b2b47a988957ddf09fa
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 3%

---
# Directrices para contribuir a la documentación de Adobe Experience Manager

## Filosofía de documentación

Los usuarios de Adobe Experience Manager trabajan en entornos altamente competitivos y se esfuerzan por crear experiencias digitales que los diferencien de su competencia. Por lo tanto, es vital que cuando Adobe ofrece nuevas herramientas avanzadas en AEM, estas herramientas se complementen con una documentación precisa y clara que permita al cliente utilizar inmediatamente su inversión en AEM y maximizar el retorno de la inversión.

El objetivo de la documentación de AEM es poner la documentación en manos de los usuarios de AEM lo antes posible. Por lo tanto, el equipo de documentación de AEM da prioridad a la documentación precisa y utilizable, y se esfuerza por actualizarla y mejorarla continuamente.

## Contribuciones de documentación

Para mejorar continuamente la documentación de AEM, contamos con la ayuda de toda la comunidad de usuarios de AEM. Ya sea a través de solicitudes de extracción o incidencias, las mejoras en la documentación pueden ser correcciones, aclaraciones, expansiones y ejemplos adicionales.

## Normas de documentación

Aunque el equipo de documentación de Experience Manager agradece las contribuciones a la documentación de Adobe, cualquier contribución a la documentación de AEM, ya sea en forma de solicitud de extracción o de incidencia, debe ajustarse a las normas de contribución y documentación del equipo.

Las contribuciones que no cumplan estas normas podrán ser rechazadas.

### El equipo de documentación de Experience Manager documenta casos de uso estándar.

La documentación de AEM abarca estos casos de uso estándar. Los casos de uso que exceden el ámbito de la instalación y el uso estándar del producto no forman parte de la documentación de AEM.

### El equipo de documentación de Experience Manager no suele documentar los errores ni sus soluciones alternativas.

La documentación de AEM abarca estos casos de uso estándar. Por este motivo, los errores, los efectos causados por errores y las soluciones alternativas para los errores no están documentados,

Las excepciones a esta regla se aplican a las notas de la versión, donde los problemas conocidos pueden enumerarse con posibles soluciones aprobadas por el equipo de administración del producto de AEM.

### Las contribuciones a la documentación no sirven para responder preguntas técnicas.

Cualquier idea que tenga para mejorar la documentación de AEM es bienvenida como contribución. Sin embargo, los comentarios, problemas y solicitudes de extracción están destinados únicamente a *contribuciones*. No están pensados para utilizarse para responder a sus preguntas sobre cómo utilizar AEM, implementar su proyecto de AEM o solucionar problemas técnicos.

Cualquier pregunta sobre el uso de AEM o errores técnicos que pueda tener debe notificarse a través del proceso de asistencia normal mediante el [Portal de asistencia de Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=es#home) o analizarse en la [comunidad de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community).

***Las contribuciones a la documentación de AEM no sustituyen a la asistencia al cliente de Adobe*** y se rechaza cualquier contribución de este tipo que busque respuestas a preguntas relacionadas con la asistencia.

### Las contribuciones deben hacer referencia claramente a las páginas de documentación afectadas.

Si crea un problema para sugerir mejoras en la documentación, debe incluir vínculos a las páginas afectadas. Si crea un problema usando el vínculo **Editar esta página** en una página de documentación, el problema se creará automáticamente con un vínculo a la página.

Esto no se aplica a las solicitudes de extracción, ya que las solicitudes de extracción, por su naturaleza, hacen referencia a las páginas afectadas.

## Directrices de documentación

Cualquier contribución a la documentación de AEM debe seguir determinadas directrices de estilo.

Seguir estas directrices facilita la revisión de su contribución y, por lo tanto, la integración en la documentación de AEM es más rápida.

### Idioma y estilo

#### Idioma

* La documentación de AEM se redacta y se actualiza en inglés estadounidense (originalmente).
* Utilice frases lo más simples posibles.
* Utilice un lenguaje claro y conciso.

Recuerde, los lectores de la documentación de AEM son de todo el mundo y no se puede esperar que hablen inglés de forma nativa o fluida. Evite los coloquialismos y utilice un lenguaje tan claro y simple como sea posible.

#### Siga el Manual de estilo de Microsoft®

[El Manual de estilo de Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) es una guía de estilo de documentación disponible libremente que se centra en documentación de software y la documentación de AEM sigue esta guía siempre que es posible.

### Formato

| Elemento | Estilo |
|---|---|
| Elemento u opción de la IU | **negrita** |
| Nombre de archivo, ruta, entrada de usuario, valores de parámetro | `monospaced` |
| Código, línea de comandos | ```Code Block``` |

### Capturas de pantalla

Las capturas de pantalla deben utilizarse con prudencia y solo cuando la descripción textual no sea suficiente.

No utilice marcadores u otras anotaciones en las capturas de pantalla (como marcos rojos, flechas o texto). De este modo, las capturas de pantalla son más fáciles de reutilizar o replicar en versiones localizadas de la documentación.

### Referencias específicas de la versión

Intente evitar cualquier referencia directa a una versión específica en todo el contenido de la documentación, siempre que sea posible. Esto hace que la documentación sea más flexible y extensible para futuras versiones.

### Uso de Day, AEM, CQ, CRX

El producto siempre se debe llamar por su nombre completo **Adobe Experience Manager** por primera vez en un artículo y, después, se puede hacer referencia a él como **AEM**.

No utilice Day, Day Software, CQ y CRX excepto cuando sea inevitable, como en nombres de clase o referencias al historial de AEM.
