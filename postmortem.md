# Postmortem

## Introducción

Fiufit es una plataforma diseñada para conectar a entrenadores y usuarios interesados en mejorar su condición física. El objetivo principal de la aplicación es proporcionar a los entrenadores un medio para compartir sus planes de entrenamiento personalizados, mientras que los usuarios pueden acceder a una amplia variedad de programas de ejercicios y obtener orientación profesional para alcanzar sus objetivos fitness.

La aplicación ofrece a los entrenadores la posibilidad de crear y subir planes de entrenamiento detallados. Estos planes pueden adaptarse a diferentes niveles de condición física y objetivos individuales, como perder peso, ganar masa muscular o mejorar la resistencia cardiovascular.

Por otro lado, los usuarios pueden explorar y seleccionar entre los planes de entrenamiento disponibles en la aplicación, según sus preferencias y necesidades. Una vez que hayan elegido un plan, podrán empezarlo a través de la aplicación. También tendrán la opción de interactuar directamente con los entrenadores, haciendo preguntas o solicitando modificaciones en los planes, como también con los otros usuarios.

La aplicación busca brindar comodidad y flexibilidad a los usuarios, permitiéndoles acceder a programas de entrenamiento de calidad en cualquier momento y lugar. Además, fomenta la interacción entre entrenadores y usuarios.

Habiendo llegado al final de la materia se procede a hacer un revision del proyecto después de su finalización, con el objetivo de analizar los éxitos y los desafíos enfrentados durante el desarrollo.

## Logros

A lo largo del desarrollo de Fiufit, logramos alcanzar varios objetivos y metas que nos propusimos. A continuación, presentaremos los principales logros que alcanzamos.

### Trabajo en equipo

Desde la perpectiva del trabajo en equipo se puede destacar:

- La buena comunicación entre los integrantes del grupo, la cual fue fundamental para el desarrollo del proyecto. Se mantuvo una comunicación fluida y constante, tanto en las reuniones semanales como en el grupo de WhatsApp. Esto permitió que todos los integrantes estuvieran al tanto de los avances y dificultades de cada uno, y que se pudieran tomar decisiones en conjunto.
- La organización del equipo para ir avanzando paulatinamente en cada checkpoint hizo que el proyecto se pudiera llevar a cabo de manera ordenada y eficiente. Se establecieron tareas y objetivos claros para cada checkpoint, y se cumplió con los plazos establecidos.

### Logros técnicos

En cuanto a los logros técnicos, se puede destacar:

- La implementación de la autenticación de usuarios, la cual fue una de las primeras funcionalidades desarrolladas. Esto permitió que los usuarios pudieran registrarse y acceder a la aplicación, y que los entrenadores pudieran crear sus planes de entrenamiento y subirlos a la aplicación.
- La integración con Google tanto para cuestiones de ubicación (mapa y coordenadas) como también para el login y para el registro de la actividad del usuario dentro de la sesión de entrenamiento. Esto permitió que los usuarios pudieran acceder a la aplicación de manera más rápida y sencilla, y que los entrenadores pudieran ubicar sus planes de entrenamiento en el mapa. También, se pudo registrar la actividad del usuario durante la sesión de entrenamiento, lo cual fue fundamental para el desarrollo de la aplicación.
- La incorporación de multimedia tanto para las fotos de pérfil de los usuarios como para los planes de entrenamiento mediante firebase storage.
- La implementación de un chat en tiempo real para que los usuarios puedan comunicarse entre ellos y con los entrenadores. También se implementó un sistema de notificaciones para que los usuarios puedan recibir alertas por distintos motivos.
- Posibilidad de compartir los planes de entrenamiento en las redes sociales, lo cual permite que los usuarios puedan compartir sus logros y avances con sus amigos y familiares.
- Recuperación de la contraseña como también, login con datos biométricos.
- Ambiente de Okteto corriendo en la nube, con el cluster de kubernetes.
- Una CI/CD functional del lado del Backend, donde cada commit pusheado se despliega en producción.
- La infraestructura del lado del servidor totalmente kubernetizada desde un primero momento, lo cual permitió tener una infraestructura declarativa, y facilitó la CI/CD. Hacerlo desde un principio nos facilitó en _no_ tener que hacer una migración completa a Kubernetes en ningún momento.
- Despliegue correcto de distintas bases de datos, principalmente dos esquemas de Bases SQL (PostgreSQL) como bases NoSQL, Redis como colas asincrónicas para métricas y MongoDB para almacenar las métricas agregadas
- Sistema de métricas completo, donde varias métricas se disparan desde los distintos microservicios hacia una cola de métricas, para que un CronJob que hace de consumer las agregue cada minuto y guarda la cantidad. Luego, otro microservicio, se encarga de seervir estas métricas para visualizarlas desde el frontend de administrador.
- Integración con la API de OpenAI para recomendaciones de entrenamientos

# Deuda técnica

Durante el desarrollo de Fiufit, nos encontramos con diversos desafíos y deudas técnicas que influyeron en el proceso y en el resultado final. Estos desafíos representaron obstáculos significativos que requerían soluciones creativas y esfuerzos adicionales para superarlos. A continuación, presentaremos los principales desafíos que enfrentamos, así como las deudas técnicas que quedaron pendientes.

Por una parte, del lado del backend, nos concentramos en hacer más system tests que en unit tests, lo cual nos permitió tener una cobertura de las historias de usuario pero no tanta seguridad a nivel código. Consideramos que, como la aplicación no tiene usuarios reales, los bugs en producción no causan incidentes, entonces decidimos priorizar otras cosas.

Luego, otra deuda técnica tiene que ver con la prolijidad y agrupación del código, en algunos casos quedaron clases con muchas líneas que, por cuestión de tiempo, no logramos refactorizar. Esto no tiene tanto impacto dado que es un proyecto con una duración fija, pero en caso de tener que mantenerlo por más tiempo, sería importante distribuir mejor las responsabilidades entre clases.
Por el lado del frontend, no hicimos tests para centrarnos en la funcionalidad de la aplicación, también la poca reutilización de componentes.

Por último, si bien estamos conformes con la UI/UX, de contar con más tiempos podríamos mejorarla.

### Desafíos

- Okteto: técnología con poco uso que se torno dificil de usar, principalmente integrarlo con la CI/CD. También tiene bastantes bugs.
- Mantener los esquemas de las bases de datos consistentes y actualizados.
- Google Maps: dificultad para integrar la API de Google Maps con React Native por cuestiones de la api key.
- Errores de kubernetes dificiles de resolver y mal documentados.
- Google Fit y el sistema de notificaciones: Ni la integración con Google Fit ni el sistema de notificaciones funciona en el emulador por lo que tuvimos que probarlo en un dispositivo físico.

## Conclusión

En conclusión, el desarrollo de Fiufit, nuestra aplicación móvil fitness, fue un proceso enriquecedor que nos permitió alcanzar importantes logros y superar desafíos significativos. Desde el punto de vista del trabajo en equipo, destacamos la excelente comunicación y la organización eficiente que nos permitió avanzar de manera consistente hacia nuestros objetivos. Mantuvimos una colaboración constante y fluida, lo que nos permitió tomar decisiones informadas y resolver problemas de manera efectiva.

Técnicamente, logramos implementar varias funcionalidades clave que enriquecen la experiencia de los usuarios y brindan un valor real a entrenadores y usuarios. La autenticación de usuarios, la integración con Google Maps, el chat en tiempo real y el sistema de notificaciones son solo algunas de las características destacadas que pudimos desarrollar con éxito.

Sin embargo, también reconocemos que hubo desafíos y deudas técnicas que quedaron pendientes. Enfrentamos obstáculos al trabajar con tecnologías poco documentadas o que se actualizan con gran frecuencia y también identificamos áreas de mejora.

Aprendimos valiosas lecciones a lo largo del proyecto. La importancia de la planificación, la resolución de problemas y la adaptabilidad ante obstáculos inesperados son aspectos que logramos aprender a lo largo del desarrollo de la materia.
