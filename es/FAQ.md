# Preguntas Frecuentes

Documento de referencia que reúne las preguntas más habituales sobre el **Golem Community Builder Programme**. Está pensado como complemento al resto de la documentación del repositorio y como punto de partida antes de canalizar consultas específicas al equipo del programa o a la comunidad técnica de Golem.

Las respuestas aquí incluidas reflejan la política vigente del programa al momento de la última actualización del documento. Para situaciones particulares no contempladas en el FAQ, los canales de comunicación oficiales se detallan al final del documento.

---

## Sobre el programa

**¿Qué es exactamente el Golem Community Builder Programme?**

El programa es una iniciativa abierta y continua que financia proyectos técnicos construidos sobre Golem Network. Cada proyecto aprobado recibe un bounty de 500 USD pagados en $GLM, con una duración estimada de entre dos y cuatro semanas de desarrollo. A diferencia de un hackathon tradicional, el programa no opera bajo presión de fechas límite ni mediante competencias de pitch, sino que financia trabajo técnico genuino sobre el protocolo. La descripción completa del programa se encuentra en el [README](../README.md).

**¿En qué se diferencia este programa de un hackathon?**

La diferencia principal es estructural. Un hackathon tiene fecha de inicio y fin, exige a los participantes completar el trabajo dentro de un plazo comprimido, y suele entregar premios solo a los proyectos ganadores tras una competencia. Este programa no tiene deadline fijo, opera de manera continua, y paga el bounty completo a todo proyecto aprobado que cumpla con los entregables acordados. La filosofía es financiar trabajo técnico de calidad antes que producir competencia entre builders.

**¿Quién puede participar?**

El programa está abierto a desarrolladores Web3 con o sin experiencia previa en Golem, así como a desarrolladores Web2 que estén explorando compute descentralizado por primera vez. No se requieren credenciales formales ni afiliación a una organización específica. Sí se requiere capacidad técnica para construir el proyecto propuesto y disposición para publicar el resultado bajo licencia abierta.

**¿Se pueden formar equipos para participar?**

Sí. El programa acepta tanto builders individuales como equipos sin límite explícito de tamaño. Los equipos deben designar un punto de contacto único para la comunicación con el equipo de Golem y definir internamente cómo distribuirán el bounty entre sus miembros. El bounty se transfiere a una única dirección de wallet, y la distribución posterior queda fuera del alcance del programa.

**¿Puedo participar en múltiples proyectos a lo largo del tiempo?**

La participación en múltiples proyectos se evalúa caso por caso por el equipo del programa. Builders que hayan completado satisfactoriamente un proyecto previo pueden ser invitados o autorizados a presentar nuevas propuestas, dependiendo de la calidad del trabajo previo, del intervalo transcurrido y de la disponibilidad de cupos en el programa. La política busca equilibrar el reconocimiento al trabajo recurrente de builders comprometidos con la apertura del programa a nuevos participantes.

---

## Sobre los aspectos técnicos

**¿Necesito tener experiencia previa con Golem para participar?**

No. El programa está explícitamente diseñado para acoger tanto a builders con experiencia previa como a desarrolladores que están encontrándose con Golem por primera vez. Para builders nuevos, el [Getting Started](./docs/getting-started.md) cubre la configuración técnica desde cero, y el [Builders Guide](./docs/builders-guide.md) ofrece direcciones de proyecto con complejidad estimada para facilitar la elección inicial.

**¿Qué SDK debo usar para construir mi proyecto?**

El camino principal recomendado es `@golem-sdk/task-executor`, una librería en JavaScript y TypeScript orientada a patrones map-reduce y paralelización de tareas. Para builders con necesidades más específicas o experiencia previa en sistemas distribuidos, `@golem-sdk/golem-js` 3.x ofrece acceso directo a los modelos de bajo nivel del protocolo. La discusión completa sobre cuándo elegir cada opción se encuentra en la sección de Notas Técnicas Comunes del [Builders Guide](./docs/builders-guide.md).

**¿Puedo trabajar en testnet o tengo que usar mainnet?**

Ambas redes son válidas para entrega del programa. La testnet, que actualmente opera sobre la red hoodi, es el entorno recomendado para la mayoría de los proyectos, dado que permite ejecutar trabajo real sobre la red sin costo real. La mainnet es apropiada cuando el proyecto requiera demostrar comportamiento económico real o integraciones con sistemas de producción. La elección debe explicitarse en el formulario de aplicación.

**¿Hay soporte para lenguajes distintos a JavaScript y TypeScript?**

El stack de Golem cuenta con SDKs en otros lenguajes, pero la documentación más actualizada y los ejemplos oficiales se concentran en el ecosistema JavaScript. Los builders que prefieran trabajar en otro lenguaje pueden hacerlo, pero deben tener en cuenta que la curva de aprendizaje y el soporte disponible son menores. Se recomienda discutir esta decisión durante la fase de aplicación.

**¿Puedo usar GPU en mi proyecto?**

Golem ofrece acceso a providers con GPU, aunque la disponibilidad puede ser variable según el momento y el tipo de hardware requerido. Los proyectos que dependan críticamente de GPU deben mencionar esta dependencia en el formulario de aplicación para que el equipo pueda confirmar la viabilidad antes de la aprobación.

---

## Sobre el proceso del programa

**¿Cuánto tiempo tarda el equipo en revisar una aplicación?**

El equipo de Golem revisa las aplicaciones de forma continua a medida que llegan. No hay un plazo fijo de respuesta, pero se notifica al builder en cuanto se toma una decisión. Si la idea encaja con el programa, el equipo se pone en contacto para definir los detalles y los hitos antes de que comience el desarrollo.

**¿Qué ocurre si mi aplicación es rechazada?**

Las decisiones sobre aplicaciones rechazadas quedan a discreción del equipo del programa. En algunos casos, el rechazo puede acompañarse de comentarios específicos que permiten al builder ajustar la propuesta y reenviarla. En otros casos, puede recomendarse al builder explorar una dirección alternativa o esperar antes de presentar una nueva propuesta. La decisión específica se comunica directamente al builder al momento del rechazo.

**¿Puedo modificar el alcance del proyecto durante el desarrollo?**

Cambios menores en el alcance, motivados por hallazgos técnicos durante el desarrollo, son habituales y aceptables siempre que se comuniquen al equipo del programa. Cambios sustanciales que alteren la naturaleza del proyecto requieren acuerdo explícito con el equipo antes de proceder. La comunicación proactiva durante el desarrollo es una expectativa formal del programa y se documenta en el [README](../README.md).

**¿Qué ocurre si no logro completar el proyecto?**

Las situaciones de proyectos no completados se evalúan caso por caso por el equipo del programa. Cuando el builder ha mantenido comunicación durante el desarrollo y existen circunstancias técnicas genuinas que impidieron la finalización, el equipo puede considerar pagos parciales proporcionales al avance demostrable o reorientar el proyecto hacia un alcance reducido. En situaciones de abandono sin comunicación, no procede el pago del bounty. La política del programa busca proteger tanto al builder ante dificultades genuinas como al equipo ante entregas no completadas.

---

## Sobre la propiedad intelectual y la difusión

**¿Quién es dueño del repositorio y del código?**

El builder mantiene plena propiedad del repositorio y del código, publicado bajo la licencia open source elegida. El programa no reclama derechos exclusivos sobre el trabajo financiado y no requiere transferencia del repositorio a una organización de Golem.

**¿Puedo usar el proyecto para mi portfolio o continuar desarrollándolo?**

Sí. El builder es libre de usar el proyecto para portfolio profesional, presentaciones públicas, candidaturas laborales, continuación del desarrollo, e incluso evolución del proyecto hacia productos comerciales. El programa fomenta explícitamente que los proyectos financiados continúen creciendo más allá del bounty inicial.

**¿Qué difusión hace Golem del proyecto?**

Una vez validado el entregable, el equipo coordina la difusión del proyecto a través de los canales oficiales de Golem. Esto incluye publicación en el Discord oficial, mención en redes sociales del proyecto cuando aplique, e inclusión del repositorio como referencia dentro del ecosistema. La difusión específica varía según el tipo de proyecto y el momento del programa.

**¿Puedo presentar el proyecto en eventos o conferencias?**

Sí. El builder es libre de presentar su trabajo en cualquier evento, hackathon o conferencia, mencionando que fue construido en el marco del Golem Community Builder Programme. Cuando aplique, el equipo del programa puede facilitar contactos o información adicional para apoyar este tipo de presentaciones.

---

## Canales de soporte y consultas

Para preguntas no cubiertas en este documento, los canales recomendados se diferencian según la naturaleza de la consulta.

Para consultas específicas sobre el programa, la primera opción es el canal de builders en el Discord oficial de Golem (discord.gg/golem), donde el equipo del programa atiende dudas sobre tracks, aplicaciones, alcance, entrega, pagos y cualquier aspecto operativo de la iniciativa.

Para consultas técnicas sobre el protocolo Golem en sí, independientemente del programa, la opción adecuada es el canal `❓question-answers` o equivalente del servidor oficial de Golem, donde la comunidad técnica más amplia y el equipo de protocolo responden dudas sobre el SDK, yagna, providers, infraestructura y otros aspectos técnicos generales.

Para profundizar en aspectos técnicos antes de plantear una consulta, la documentación oficial de Golem en [docs.golem.network](https://docs.golem.network) constituye el recurso de referencia principal y suele responder la mayoría de las dudas técnicas habituales sin necesidad de canalizarlas por chat.

El acceso al servidor oficial de Discord se realiza desde [discord.gg/golem](https://discord.gg/golem).

---

## Preguntas adicionales

**¿Necesito preparar un documento de pitch o una plantilla para aplicar?**

No. Las aplicaciones se realizan a través del formulario oficial en https://forms.golem.network/golem-builders-programme. El formulario recoge el track, la idea, el enfoque técnico y la experiencia relevante. No hay ningún documento de pitch separado que escribir o subir.

**¿Cuánto tiempo se tarda en recibir respuesta tras aplicar?**

El equipo de Golem revisa las aplicaciones de forma continua. No hay un plazo de respuesta fijo, pero se te notificará en cuanto se tome una decisión. Si la idea encaja con el programa, el equipo se pone en contacto para discutir los detalles y los hitos antes de que comience el desarrollo.

**¿Qué debe mostrar el vídeo demo de 2–3 minutos?**

Una grabación breve del proyecto funcionando en la práctica, suficiente para que alguien sin conocimiento previo del trabajo entienda qué hace y cómo utiliza Golem. El vídeo es un entregable obligatorio y se emplea para la difusión en los canales oficiales de Golem.