# Preguntas Frecuentes

## Sobre el programa

**¿Qué es exactamente el Golem Community Builder Programme?**

El programa es una iniciativa abierta y continua que financia proyectos técnicos construidos sobre Golem Network. Cada proyecto aprobado recibe un bounty de 500 USD pagados en $GLM, con una duración estimada de entre dos y cuatro semanas de desarrollo. La descripción completa del programa se encuentra en el [README](./README.md).

**¿En qué se diferencia este programa de un hackathon?**

El programa es abierto: sin plazos, sin competencia de pitch, sin finalistas. Los builders proponen sus propias ideas a través del formulario. El equipo de Golem revisa las propuestas de forma continua y selecciona las más sólidas. Para los proyectos seleccionados, el builder y el equipo acuerdan el alcance antes de que comience el desarrollo — y solo entonces arranca el trabajo.

**¿Quién puede participar?**

Cualquier desarrollador con capacidad técnica para entregar un proyecto real: perfil Web2 o Web3, con o sin experiencia previa en Golem.

**¿Se pueden formar equipos para participar?**

Sí. El programa acepta tanto builders individuales como equipos sin límite de tamaño. Los equipos deben designar un punto de contacto único para la comunicación con el equipo de Golem y definir internamente cómo distribuirán el bounty entre sus miembros. El bounty se transfiere a una única dirección de wallet, y la distribución posterior queda fuera del alcance del programa.

**¿Puedo participar en múltiples proyectos a lo largo del tiempo?**

Un proyecto por equipo a la vez. Una vez validada la entrega y pagado el bounty, el mismo equipo puede volver a aplicar con una nueva idea.

---

## Sobre los aspectos técnicos

**¿Necesito tener experiencia previa con Golem para participar?**

No se requiere experiencia previa con Golem. El equipo está disponible en Discord para incorporarte al protocolo durante el desarrollo.

**¿Qué SDK debo usar para construir mi proyecto?**

El camino principal recomendado es `@golem-sdk/task-executor`, una librería en JavaScript y TypeScript orientada a patrones map-reduce y paralelización de tareas. Para builders con necesidades más específicas o experiencia previa en sistemas distribuidos, `@golem-sdk/golem-js` 3.x ofrece acceso directo a los modelos de bajo nivel del protocolo. La discusión completa sobre cuándo elegir cada opción se encuentra en la sección de Notas Técnicas Comunes del [Builders Guide](./docs/guia_builders.md).

**¿Puedo trabajar en testnet o tengo que usar mainnet?**

Se espera que los builders trabajen en testnet (actualmente `hoodi`). No hay expectativa de mainnet por defecto. Si un proyecto genuinamente la requiere, eso se acuerda entre el equipo seleccionado y el equipo de Golem durante la fase de scoping.

**¿Hay soporte para lenguajes distintos a JavaScript y TypeScript?**

El stack de Golem cuenta con SDKs en otros lenguajes, pero la documentación más actualizada y los ejemplos oficiales se concentran en el ecosistema JavaScript. Los builders que prefieran trabajar en otro lenguaje pueden hacerlo, pero deben tener en cuenta que la curva de aprendizaje y el soporte disponible son menores. Se recomienda discutir esta decisión durante la fase de aplicación.

**¿Puedo usar GPU en mi proyecto?**

Golem ofrece acceso a providers con GPU, aunque la disponibilidad puede ser variable según el momento y el tipo de hardware requerido. Los proyectos que dependan críticamente de GPU deben mencionar esta dependencia en el formulario de aplicación para que el equipo pueda confirmar la viabilidad antes de la aprobación.

---

## Sobre el proceso del programa

**¿Cuánto tiempo tarda el equipo en revisar una aplicación?**

El equipo de Golem revisa las aplicaciones de forma continua, sin ventana de respuesta fija. Recibirás notificación en cuanto se tome una decisión. Si la idea encaja con el programa, el equipo se pone en contacto para acordar alcance e hitos antes de que comience el desarrollo.

**¿Qué ocurre si mi aplicación es rechazada?**

Las decisiones quedan a discreción del equipo del programa. Intentamos compartir feedback cuando podemos, pero dado el volumen de aplicaciones no podemos garantizarlo.

**¿Puedo modificar el alcance del proyecto durante el desarrollo?**

Cambios menores en el alcance, motivados por hallazgos técnicos durante el desarrollo, son habituales y aceptables siempre que se comuniquen al equipo del programa. Cambios sustanciales que alteren la naturaleza del proyecto requieren acuerdo explícito con el equipo antes de proceder.

**¿Qué ocurre si no logro completar el proyecto?**

Las situaciones de proyectos no completados se evalúan caso por caso por el equipo del programa.

---

## Sobre la propiedad intelectual y la difusión

**¿Quién es dueño del repositorio y del código?**

El builder mantiene plena propiedad del repositorio y del código, publicado bajo la licencia open source elegida. El programa no reclama derechos exclusivos sobre el trabajo financiado y no requiere transferencia del repositorio a una organización de Golem.

Al enviar un proyecto al programa, el builder autoriza a Golem a mencionar, compartir y destacar el proyecto en sus canales con fines de comunicación y promoción del ecosistema.

**¿Puedo usar el proyecto para mi portfolio o continuar desarrollándolo?**

Sí. El builder es libre de usar el proyecto para portfolio profesional, presentaciones públicas, candidaturas laborales, continuación del desarrollo, e incluso evolución del proyecto hacia productos comerciales. El programa fomenta explícitamente que los proyectos financiados continúen creciendo más allá del bounty inicial.

**¿Cómo difunde Golem el proyecto?**

Una vez validado el entregable: una publicación en Discord, una mención en redes sociales cuando encaje, y el repositorio añadido a la lista de referencias del ecosistema. Lo que hacemos exactamente depende del proyecto.

**¿Puedo presentar el proyecto en eventos o conferencias?**

Sí. El builder es libre de presentar su trabajo en cualquier evento, hackathon o conferencia. Cuando aplique, el equipo del programa puede facilitar contactos o información adicional para apoyar este tipo de presentaciones.

---

## Soporte y canales

- **Preguntas sobre el programa** (tracks, aplicaciones, alcance, entrega, pagos): canal `builders` en el Discord oficial de Golem.
- **Preguntas técnicas sobre Golem** (SDK, yagna, providers, infraestructura): canal `❓question-answers` en el mismo Discord.
- **Antes de preguntar, consulta la documentación**: [docs.golem.network](https://docs.golem.network) cubre la mayoría de las dudas técnicas habituales.

Únete al Discord en [discord.gg/golem](https://discord.gg/golem).

---

## Preguntas adicionales

**¿Necesito preparar un documento de pitch o una plantilla para aplicar?**

No. Las aplicaciones se realizan a través del formulario oficial en https://forms.golem.network/golem-builders-programme. El formulario recoge el track, la idea, el enfoque técnico y la experiencia relevante. No hay ningún documento de pitch separado que escribir o subir.

**¿Qué debe mostrar el vídeo demo de 2–3 minutos?**

Una grabación breve del proyecto funcionando en la práctica, suficiente para que alguien sin conocimiento previo del trabajo entienda qué hace y cómo utiliza Golem. El vídeo es un entregable obligatorio y se emplea para la difusión en los canales oficiales de Golem.

**Cuando el bounty se paga en $GLM, ¿cómo se convierte el monto en USD?**

El bounty está denominado en 500 USD y se paga en $GLM. El monto de $GLM se fija al tipo de cambio del día del pago, de modo que el valor equivalente en USD en ese momento coincide con el bounty acordado. Los builders proporcionan una dirección de wallet y la red en la que desean recibirlo (Polygon o Ethereum mainnet); el $GLM se transfiere directamente.

**¿Puedo usar herramientas de IA o asistentes de código mientras construyo?**

Sí. El entregable es el proyecto funcionando, la documentación y el vídeo demo. La forma en que lo construyes es decisión tuya: asistentes de código con IA, herramientas de pair programming o cualquier otro recurso. Lo importante es que el código sea tuyo para publicar bajo licencia open source, que el informe técnico refleje tu comprensión del trabajo y que el proyecto realmente ejecute en Golem.

**¿Puedo hacer un fork de un proyecto Golem existente para mi propuesta?**

Los forks se aceptan únicamente como punto de partida y solo cuando hay trabajo nuevo sustancial sobre ellos. Un fork puro con cambios menores no califica. Si tienes dudas sobre si tu propuesta cuenta como trabajo sustancial, menciónalo en el formulario de aplicación — el equipo te lo confirmará de antemano.