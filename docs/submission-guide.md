# Submission Guide

Documento de referencia para la entrega formal de proyectos dentro del **Builder Programme**. Define los criterios mínimos que un entregable debe cumplir, el procedimiento de notificación al equipo de Golem, el proceso de revisión y los pasos para recibir el pago del bounty.

La lectura de este documento se recomienda al inicio del desarrollo, no únicamente al momento de entregar. Conocer los requisitos de la submission desde el comienzo permite al builder estructurar el repositorio y la documentación de manera incremental, evitando trabajo de último momento y asegurando que el entregable cumpla con los estándares del programa.

---

## Procedimiento de entrega

La entrega formal de un proyecto finalizado se realiza mediante correo electrónico dirigido al equipo del programa. Este es el canal oficial mediante el cual se inicia el proceso de revisión y se dispara el ciclo de validación que conduce al pago del bounty.

El correo de entrega debe enviarse a la dirección oficial del programa [pendiente] e incluir como mínimo los siguientes elementos: identificación del builder y referencia al pitch aprobado previamente, enlace público al repositorio del proyecto en GitHub, dirección de wallet del builder para la transferencia del bounty con indicación explícita de la red sobre la que se realizará el pago, y cualquier nota relevante sobre el estado del proyecto que el equipo deba conocer antes de iniciar la revisión (por ejemplo, limitaciones identificadas durante el desarrollo, decisiones de alcance tomadas en consulta con el equipo, o resultados particularmente notables que conviene destacar).

De manera complementaria, una vez confirmada la recepción del correo y luego de que el proceso interno haya avanzado, se anunciará el proyecto en el Discord oficial de Golem con un resumen breve y los enlaces correspondientes. [pendiente_canal_dedicado] El builder no necesita iniciar este anuncio por su cuenta: el equipo coordina la publicación en los canales correspondientes una vez que la entrega ha sido validada.

---

## Requisitos del repositorio

El proyecto debe vivir en un repositorio público de GitHub bajo el usuario u organización personal del builder. 

El repositorio debe estar publicado bajo una licencia open source claramente indicada. La licencia recomendada es **MIT**, dado que es la más permisiva, la más utilizada en el ecosistema de Golem y la que mejor facilita la reutilización del trabajo por parte de la comunidad. El archivo `LICENSE` debe estar presente en la raíz del repositorio con el texto completo de la licencia y el nombre del titular.

La estructura del repositorio debe permitir que un desarrollador externo pueda clonar el proyecto, instalar las dependencias y ejecutarlo siguiendo exclusivamente las instrucciones del README, sin necesidad de consultas adicionales. Esto implica que el código debe estar acompañado de un archivo de configuración de dependencias estándar para el lenguaje utilizado (`package.json` para Node.js, `requirements.txt` o `pyproject.toml` para Python, según corresponda), de los scripts necesarios para reproducir las corridas documentadas en el entregable, y de cualquier archivo de configuración o variable de entorno requerida para la ejecución, debidamente documentado.

Se recomienda evitar incluir credenciales, claves privadas, archivos de configuración local o cualquier dato sensible en el repositorio. Las variables que el builder deba configurar para correr el proyecto deben estar documentadas en el README mediante un archivo `.env.example` o equivalente.

---

## Requisitos del README

El README del repositorio constituye el principal documento de cara al público y debe escribirse con el cuidado correspondiente. Cumple simultáneamente la función de presentación del proyecto, instrucciones de uso para desarrolladores que quieran reproducirlo, y write-up técnico que documenta el trabajo realizado.

El README debe abrir con una descripción concisa del proyecto que explique en pocas líneas qué hace, sobre qué track del programa fue construido, y por qué resulta interesante desde la perspectiva del compute descentralizado. Esta sección inicial debe ser comprensible para un lector que no haya leído el pitch original.

A continuación, debe incluirse una sección de instrucciones de instalación y ejecución, suficientemente detallada para que un desarrollador externo pueda reproducir el proyecto. Esta sección debe cubrir los requisitos previos (versión de yagna, versión de Node.js u otro runtime, dependencias del sistema operativo si aplica), el procedimiento paso a paso de instalación y configuración, y los comandos exactos para ejecutar el proyecto y reproducir los resultados documentados.

El cuerpo principal del README debe contener el write-up técnico del proyecto. Esta sección documenta qué se construyó, cómo se diseñó la paralelización, qué decisiones técnicas se tomaron y por qué, qué desafíos se encontraron durante el desarrollo y cómo se resolvieron, y qué resultados se obtuvieron. La extensión esperada es de varias secciones bien estructuradas, suficientes para que un lector técnico pueda comprender el trabajo en profundidad sin necesidad de leer el código fuente.

Una sección dedicada debe presentar las métricas y resultados de la ejecución del proyecto sobre Golem. <!-- PLACEHOLDER: definir conjunto mínimo común de métricas requeridas para todos los tracks --> Los criterios específicos sobre qué métricas reportar y en qué formato se establecerán en una versión posterior de este documento. Hasta entonces, los builders deben reportar las métricas indicadas en el track correspondiente del [Builders Guide](./guia_builders.md) y cualquier dato adicional que considere relevante para demostrar el funcionamiento del proyecto.

Finalmente, el README debe cerrar con una breve sección que documente las limitaciones conocidas del proyecto, las posibles direcciones de extensión que otros builders podrían explorar a partir de este trabajo, y los créditos correspondientes al builder y al programa.

---

## Resumen para Discord

De manera complementaria al write-up extenso del README, el proyecto debe acompañarse de un resumen breve diseñado para publicación en el Discord oficial de Golem. Este resumen no reemplaza al README sino que funciona como anuncio de la entrega y puerta de entrada hacia el repositorio.

El resumen debe ser significativamente más corto que el README, escrito en un registro accesible para una audiencia amplia que puede no tener contexto técnico profundo, y orientado a generar interés por consultar el repositorio completo. La extensión recomendada es de uno o dos párrafos que cubran qué se construyó, qué demuestra del protocolo, y dónde encontrar el repositorio para mayor detalle.

El builder debe enviar este resumen junto con el correo de entrega o como respuesta posterior cuando el equipo lo solicite. La publicación efectiva en Discord la coordina el equipo del programa siguiendo el procedimiento interno correspondiente.

---

## Proceso de revisión y pago

Una vez recibido el correo de entrega con la información completa, el equipo de Golem inicia la revisión del proyecto. Esta revisión verifica que el entregable cumpla con los requisitos formales descritos en este documento, que se ajuste al alcance acordado en el pitch aprobado, y que las métricas reportadas sean coherentes y reproducibles a partir del código publicado.

Si la revisión identifica puntos abiertos que requieran ajustes (documentación incompleta, métricas insuficientes, problemas de reproducibilidad, alcance no cubierto), el equipo abrirá un ciclo de iteración con el builder por correo electrónico, indicando los puntos específicos a resolver. Este ciclo busca asegurar la calidad del entregable y, en general, los ajustes solicitados son menores y se resuelven en pocos días.

Una vez validado el entregable, el equipo procede al pago del bounty mediante transferencia de $GLM a la dirección de wallet proporcionada por el builder, en la red indicada en el correo de entrega. El builder debe asegurarse de proporcionar una dirección de wallet correcta y compatible con la red elegida, dado que los pagos enviados a direcciones erróneas no son recuperables.

Tras la confirmación del pago, el equipo procede a la coordinación de la difusión del proyecto a través de los canales oficiales y de las comunidades partner correspondientes, completando así el ciclo del programa.

---

## Recomendaciones finales

Más allá de los requisitos formales, existen algunas buenas prácticas que elevan significativamente la calidad percibida de un entregable y favorecen su difusión posterior.

Las capturas de pantalla, diagramas o grabaciones cortas que muestren el proyecto en operación tienen un valor demostrativo desproporcionado y se recomienda incluirlos en el README cuando el tipo de proyecto lo permita. Un GIF animado mostrando una ejecución real, un diagrama de arquitectura claro o una visualización de los resultados obtenidos transforman un README correcto en uno memorable.

La disponibilidad del builder para responder issues razonables abiertos en el repositorio durante las semanas posteriores a la entrega contribuye al valor del recurso publicado y se considera buena práctica del programa, sin constituir una condición formal para el pago del bounty.

Finalmente, los builders cuyo entregable resulte particularmente bien recibido por la comunidad pueden ser invitados a participar en futuras iniciativas del ecosistema, presentar su trabajo en eventos relacionados con Golem o colaborar en proyectos de mayor alcance. La calidad del entregable inicial es, en este sentido, también una inversión en oportunidades posteriores.

---

## Próximos pasos

Tras completar la entrega siguiendo este documento, el builder no requiere realizar acciones adicionales hasta recibir respuesta del equipo. Para consultas durante el proceso de revisión o sobre cualquier aspecto del programa, el canal recomendado continúa siendo el Discord oficial de Golem en [discord.gg/golem](https://discord.gg/golem).

Para referencia sobre los demás documentos del programa, consultar el [README](../README.md) general del repositorio.