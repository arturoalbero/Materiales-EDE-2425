
# Pruebas de Seguridad

En la ingeniería de software contemporánea, la **seguridad** no es un componente adicional, sino un aspecto intrínseco del ciclo de vida del desarrollo de software (SDLC). Las pruebas de seguridad son un conjunto de actividades diseñadas para evaluar la resiliencia de una aplicación frente a ataques maliciosos, identificar vulnerabilidades y asegurar que los controles de seguridad implementados funcionan como se espera.


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Pruebas de Seguridad](#pruebas-de-seguridad)
    - [Importancia de las pruebas de seguridad](#importancia-de-las-pruebas-de-seguridad)
    - [Tipos de Pruebas de Seguridad](#tipos-de-pruebas-de-seguridad)
      - [Pruebas de Seguridad de Aplicaciones Estáticas (SAST)](#pruebas-de-seguridad-de-aplicaciones-estáticas-sast)
      - [Pruebas de Seguridad de Aplicaciones Dinámicas (DAST)](#pruebas-de-seguridad-de-aplicaciones-dinámicas-dast)
      - [Análisis de Composición de Software (SCA)](#análisis-de-composición-de-software-sca)
      - [Pruebas de Penetración (Pentesting)](#pruebas-de-penetración-pentesting)
    - [Estrategias y Consideraciones Clave](#estrategias-y-consideraciones-clave)
    - [Recursos para la realización de pruebas de seguridad](#recursos-para-la-realización-de-pruebas-de-seguridad)

<!-- /code_chunk_output -->



> **Actividad**
> Realiza un mapa conceptual sobre las pruebas de seguridad y experimenta con alguna de las aplicaciones presentadas al final de este apartado

### Importancia de las pruebas de seguridad

La integración de pruebas de seguridad es indispensable por múltiples razones. Permiten la **prevención de brechas de datos**, salvaguardando la información sensible y la privacidad de los usuarios. Aseguran el **cumplimiento normativo** con regulaciones cada vez más estrictas, como GDPR o PCI DSS. Además, protegen la **reputación** de una organización, ya que un incidente de seguridad puede tener consecuencias devastadoras para la confianza del cliente. Finalmente, **reducen costos** significativamente, puesto que corregir vulnerabilidades en las primeras etapas del desarrollo es considerablemente más económico que hacerlo tras un incidente en producción.

### Tipos de Pruebas de Seguridad

Las pruebas de seguridad se clasifican principalmente por la metodología y el punto del SDLC en el que se aplican:

#### Pruebas de Seguridad de Aplicaciones Estáticas (SAST)

El **SAST** analiza el código fuente, el bytecode o los binarios de una aplicación sin ejecutarla. Se realiza en fases tempranas del SDLC, a menudo durante el desarrollo o la integración continua. Su objetivo es identificar vulnerabilidades comunes como inyección SQL, Cross-Site Scripting (XSS) y configuraciones inseguras. La principal ventaja del SAST radica en su capacidad para detectar fallos tempranamente y proporcionar la ubicación precisa de la vulnerabilidad en el código. Sin embargo, puede generar un número considerable de falsos positivos y no detecta vulnerabilidades que solo se manifiestan en tiempo de ejecución.

#### Pruebas de Seguridad de Aplicaciones Dinámicas (DAST)

El **DAST** evalúa la aplicación mientras está en ejecución, interactuando con ella desde una perspectiva externa, similar a como lo haría un atacante. Este enfoque revela vulnerabilidades que se manifiestan durante la ejecución, como problemas de autenticación, autorización, manejo de sesiones y validación de entradas. Una ventaja clave del DAST es su capacidad para simular ataques reales y detectar problemas relacionados con el entorno de ejecución, como configuraciones incorrectas. No obstante, no proporciona la ubicación exacta del código fuente vulnerable y su cobertura depende de las rutas de la aplicación que se ejerciten.

#### Análisis de Composición de Software (SCA)

El **SCA** se enfoca en identificar y evaluar las vulnerabilidades de seguridad inherentes en las **bibliotecas y componentes de código abierto** que una aplicación utiliza. Dada la prevalencia del uso de componentes de terceros, este análisis es crucial para detectar dependencias con vulnerabilidades conocidas (CVEs), las cuales podrían introducir puntos débiles significativos en la aplicación final.

#### Pruebas de Penetración (Pentesting)

El **pentesting** es una simulación controlada de un ataque real al sistema, llevada a cabo por pentesters éticos. Combina herramientas automatizadas con habilidades manuales y un conocimiento profundo de las tácticas de ataque para identificar y explotar vulnerabilidades críticas que las herramientas automáticas podrían pasar por alto. Los resultados se materializan en informes detallados sobre la explotabilidad de las vulnerabilidades y recomendaciones específicas para su mitigación.

### Estrategias y Consideraciones Clave

Para una implementación efectiva de las pruebas de seguridad, es fundamental adoptar un enfoque integral. Esto incluye la **seguridad por diseño**, integrando consideraciones de seguridad desde las fases iniciales del diseño arquitectónico. La **revisión manual de código** por parte de expertos en seguridad puede complementar las herramientas automatizadas, especialmente en la lógica de negocio crítica. El uso de guías como el **OWASP Top 10** proporciona una hoja de ruta invaluable para priorizar las pruebas. Además, la **integración de herramientas de seguridad en los pipelines de CI/CD** automatiza la detección de vulnerabilidades, proporcionando una retroalimentación continua y rápida a los equipos de desarrollo.

### Recursos para la realización de pruebas de seguridad

Para experimentar de primera mano con las pruebas de seguridad en entornos Java, existen diversas aplicaciones deliberadamente vulnerables. Estas aplicaciones están diseñadas para simular escenarios de vulnerabilidades comunes y permiten practicar la detección y explotación de fallos de seguridad de manera ética y controlada.

* [OWASP WebGoat](https://owasp.org/www-project-webgoat/): Probablemente el proyecto más conocido para aprender sobre seguridad de aplicaciones web. WebGoat es una aplicación web de Java diseñada por OWASP que contiene una serie de lecciones interactivas. Cada lección presenta una vulnerabilidad específica (como inyección SQL, XSS, control de acceso roto, etc.) y guía al usuario para explotarla y luego comprender cómo mitigarla. Es una excelente plataforma para practicar DAST y revisión manual de código.

* [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/): Aunque no está construida en Java, es una aplicación Node.js/Angular.js, su naturaleza de aplicación web moderna con una amplia gama de vulnerabilidades la convierte en una plataforma de prueba fantástica para DAST y pruebas de penetración, sin importar la tecnología de backend específica. Las técnicas para encontrar vulnerabilidades son agnósticas al lenguaje del servidor en muchos casos.

* [Damn Vulnerable Java Application (DVJA)](https://github.com/appsecco/dvja): Similar a WebGoat, DVJA es una aplicación web Java creada para ser vulnerable. Ofrece un entorno controlado para que los estudiantes y profesionales de la seguridad puedan probar y experimentar con diferentes tipos de vulnerabilidades de aplicaciones web y Java, incluyendo deserialización insegura y problemas de manejo de archivos.

* [bWAPP (Buggy Web Application)](http://www.itsecgames.com/): Es una aplicación web gratuita y de código abierto que contiene más de 100 vulnerabilidades web. Si bien está escrita principalmente en PHP, muchas de las vulnerabilidades son agnósticas al lenguaje y pueden ser un excelente banco de pruebas para herramientas DAST y principios de pruebas de penetración que son aplicables a cualquier aplicación web, incluidas las Java.

La utilización de estas plataformas en un entorno de laboratorio permite a los alumnos desarrollar habilidades prácticas en la identificación, explotación y mitigación de vulnerabilidades, un conocimiento crítico para cualquier desarrollador que aspire a construir software seguro.