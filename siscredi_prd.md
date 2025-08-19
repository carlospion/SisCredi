PRD: SisCredi

  # Product Requirements Document (PRD)
  ## SisCredi - Sistema de Gestión de Creditos

  ### 1. RESUMEN EJECUTIVO
  **Versión:** 1.0
  **Fecha:** Agosto 2025
  **Propietario del Producto:** SisCredi

  #### 1.1 Descripción del Producto
  SisCredi es una aplicacion web de gestion de datos de clientes, prestamos, pagos y garantias, que genera reportes, informes y analisis sobre el perfil de riesgo, capacidad de pago y cualquier perfil financiero en general del cliente, de manera inteligentes y predictivos (atraves del machine learning) de clientes en base a los cruces de datos de los usuarios suscriptos.
  El sistema esta dirigido para para prestamistas particulares (persona fisica/individual) y empresas como financieras, cooperativas, casas de empeños, joyerias y entidades financieras, y cualquier otra de las figuras establecidas y constituida como persona juridica.
  Construida con Python y el fremawork de Django.

  #### 1.2 Objetivos del Negocio
  - [ ] gestionar perfiles y datos de clientes fisicos y juridicos, sus prestamos, pagos y garantias mediante operaciones CRUD para usuarios fisicos o juridicos
  - [ ] realizar analisis predictivos e inteligentes de los clientes en base a sus comportamiento de pagos con relacion al credito otorgado y la gestion de cartera de credito en general del usuario, para alimentar los entrenamientos de machine learning
  - [ ] crear reportes, estados, metricas e informes detallados para los usuarios sobre su cartera de creditos  
  - [ ] realizar notificaciones en tiempo real de los comportamiento de los pagos 
  - [ ] implementar diferentes APIs al sistema como correlaciones bancarias entre otro
  - [ ] automatizar al 100% los analisis manuales y creacion de reportes detallados
  - [ ] alojar los datos de la manera mas optima y entendible posible para reportes, diarios, semanales, mensuales, trimestrales, semestrales y anuales, como tambien para posible migraciones
  - [ ] Incrementar productividad del usuario en 70% (medido por tareas
  completadas/hora)
  - [ ] Alcanzar 1,000 usuarios activos en 6 meses
  - [ ] Lograr 85% de retención de usuarios a los 30 días

  ### 2. CONTEXTO Y PROBLEMA

  #### 2.1 Problema a Resolver
  - Evitar que los prestamistas individuales registre manualmente de los datos de los clientes, el calculo de los prestamos y el registro de pagos, notificar y cobrar uno por uno los clientes, acordarse de fechas de pagos, redactar contratos y como tambien el crear reportes y estadisticas
  - Evitar que las empresas realicen analisis, predicciones y cotizaciones profundas e inteligentes de manera manuales o que tenga la necesidad de contratar un analista para esta area, comodidad y simplicidad para el usuario que manejara el sistema, ya que sera una herramienta totalmente intuitiva y eficaz para los registros de grandes cantidades de datos. 
  - Evitar cualquier tarea manual que conlleva este nicho 
  - Estimación imprecisa de tiempos
  - Sobrecarga de información sin contexto
  - Falta de insights sobre patrones de productividad

  #### 2.2 Usuarios Objetivo
  el sistema Siscredi trabajara con una base de datos SQL con aislamiento multi-tenancy, el cual estara dividido en dos usuarios: 
  - **Usuario Primario:** son los usuarios que contratan los servicios del sistema, son como una especie de admin de sus datos registrados que esten enlazados a su ID, los cuales tendran algunos privilegios dentro de sus datos enlazados, tambien manejaran a sus "Usuario Secundario" como agregar mas usuarios o eliminarlos que esten enlazados a su "Usuario Primario" Product Managers, equipos ágiles
  - **Usuario Secundario:** son los usuarios enlazados a su "Usuario Primario", y esto se encargaran de realizar las operaciones CRUD del sistema (basicamente son los que operaran el sistema bajo el enlace de su propio ID enlazado al ID de su "Usuario Primario")

  #### 2.3 Propuesta de Valor
  Una de las pocas plataformas Freemium del pais (Republica Dominicana) que combina gestión de tareas tradicional como lo es la gestion de clientes y sus creditos con las herramientas de machine learning (IA) para el estudio de los datos para arrojar analisis e informes predictivos e inteligentes y que optimiza automáticamente los flujos de trabajo y las tareas repetitivas.

  ### 3. ESPECIFICACIONES TÉCNICAS (DJANGO)

  #### 3.1 Stack Tecnológico
  - **Backend:** Python 3.13.7+, Django 5.2.5+, Django REST Framework
  - **Base de Datos:** PostgreSQL
  - **LLM/AI/ML:** IA open-source API, scikit-learn
  - **Frontend:** HTML, CSS y JavaScript (bootstrap)
  - **Deployment:** AWS (Elastic Beanstalk)
  - **Cache:** Redis
  - **Task Queue:** Celery con Redis broker

  #### 3.2 Modelos de Django Principales
  Utiliza de manera proactiva las herramientas por defecto que se encuentran en la libreria/biblioteca de Django para las implementaciones de las funciones principales de la aplicacion web la gestion de las tareas comunes de desarrollo web (para ello te puedes apoyar/ayudar de las documentaciones oficiales de la pagina de Django)

  #### 3.3 APIs y Endpoints
  - APIs REST
  - metodos HTTPs
  - Seguridad
  - Documentación
  - Escalabilidad
  - Manejo de errores
  - Versiones

  4. REQUERIMIENTOS FUNCIONALES

  4.1 Epic 1: Registro de datos generales

  User Story: Como project manager, quiero que el sistema priorice
  el correcto manejo y registro de los datos de los clientes, prestamos, pagos y garantias para garantizar una alimentacion optima de los datos almacenados para implementarlo al campo de entrenamiento de los modelos de machine learning que estaremos desarrollado.
  productividad para optimizar mi flujo de trabajo diario.

  Criterios de Aceptación:
  - Sistema valida que los datos ingresados sean correctos y coherentes antes de registrarlos en la BD
  - clasificar correctamente los datos en la BD
  - ML reconoce los datos y se empiezan a entrenar sus modelos

  4.2 Epic 2: Central de Notificaciones

  User Story: Como project manager, quiero que el sistema vele por una correcta central de notifiaciones, optima y eficiente, que se maneje de manera autonoma y en tiempo real tanto para el usuario como su cliente.

  Criterios de Aceptación:
  - mantener actualizada la central de notificaciones del sistema
  - manejo eficiente de las notificaciones hacia los clientes
  - utiliza la IA para la optimizacion y autonomia de la central de notificaciones

  4.3 Epic 3: Modelos de Machine learning

  User Story: Como project manager, quiero que el sistema vele por un correcto entrenamiento de los modelos de machine learning entrenados a base de los datos alojados en la BD.

  Criterios de Aceptación:
  - elaborar perfil de riesgo de los clientes 
  - elaborar analisis predicitvo del cliente
  - elaborar informes y estados 

4.4 Epic 4: Manejo del sistema

  User Story: Como usuario Principal, quiero mantenerme al tanto de las acciones realizadas por mis usuarios Secudarios, como tambien el poder ejecutar sus tareas (si no tengo usuarios secundarios registrados), poder eliminar y agregar usuarios secundarios y tener privilegios e informaciones que solo el yo como usuario principal puedo ejecutar, tales como editar, eliminar o crear datos especificos.

  Criterios de Aceptación:
  - Privilegios de poder realizar personalizaciones a su perfil
  - crear u eliminar usuarios secudarios
  - notificar directamente al usuario principal de acciones relevante
  - privilegios a informaciones restringidas al usuario secudario

  4.5 Epic 5: Manejo del sistema

  User Story: Como Usuario Secundario, quiero realizar las operaciones CRUD del sistema enlazado al ID del Usuario Principal y dentro del alcance de mis acciones sin sobre pasar las areas restringidas.

  Criterios de Aceptación:
  - ejecutar todas las operaciones CRUD del sistema
  - siempre estar enlazado al Usuario Principal

  4.5 Epic 5: Manejo del sistema

  User Story: Como Cliente de mi Usuario Principal, quiero que se me notifique de la creacion de cada credito otorgado y de ser notificado de cada pago realizado, como tambien tener la opcion de revisar el estatus de mis creditos y de los pagos realizados atraves de Whatsapp.

  Criterios de Aceptación:
  - Ser notificado por sus creditos y pagos atraves de correos electronicos, mensajes de texto telefonicos y/o Whatsapp
  - Poder consultar el estatus de su Credito atraves de Whatsapp

  5. REQUERIMIENTOS NO FUNCIONALES

  5.1 Performance

  - Respuesta de API para queries simples
  - AI processing para análisis de tareas
  - Soporte 100 usuarios concurrentes (escalable)

  5.2 Seguridad

  - autenticación de usuarios de Django
  - Aislamiento Multi-tenancy
  - Rate limiting por usuario y IP
  - Encriptación de datos sensibles


  5.3 AI/ML Requirements

  - Model accuracy para estimaciones de tiempo
  - Reentrenamiento automático semanal
  - A/B testing framework para algoritmos
  - Fallback a reglas heurísticas si AI falla

  6. DISEÑO Y UX

  6.1 Flujos de Usuario Principales

  1. Smart Task Creation
    - Usuario crea tarea con descripción
    - AI analiza y sugiere prioridad, tiempo estimado, tags
    - Usuario confirma o ajusta sugerencias
    - Sistema aprende de ajustes
  2. Intelligent Daily Planning
    - Usuario inicia día
    - AI presenta plan optimizado basado en calendar, energy levels
    - Usuario puede reorganizar con drag & drop
    - Sistema recalcula prioridades dinámicamente

  7. PLAN DE DESARROLLO

  7.1 Fases del Proyecto

  - Fase 1 (MVP): [6 semanas]
    - CRUD básico de tareas y proyectos
    - Integración OpenAI para análisis básico
    - Dashboard simple con métricas
  - Fase 2: [4 semanas]
    - ML model personalizado para estimaciones
    - Sistema de notificaciones inteligentes
    - Analytics avanzados
  - Fase 3: [4 semanas]
    - Colaboración en equipo
    - Integraciones (Slack, Calendar)
    - Mobile responsiveness

  8. MÉTRICAS Y KPIs

  8.1 Métricas de AI Performance

  - Accuracy de estimaciones de tiempo (objetivo: >80%)
  - User satisfaction con recomendaciones (objetivo: >4.5/5)
  - Reduction en task switching (objetivo: 30% decrease)

  8.2 Métricas de Producto

  - Monthly Active Users (objetivo: 10K en 6 meses)
  - Average session duration (objetivo: >15 min)
  - Tasks completed per user per day (objetivo: >8)

  9. INTEGRACIONES AI/MCP

  9.1 MCP Connectors Planeados

  - Calendar integration (Google, Outlook)
  - Communication tools (Slack, Teams)
  - Development tools (GitHub, Jira)
  - Time tracking (Toggl, RescueTime)

  9.2 AI Models Pipeline

  # Ejemplo de pipeline de ML
  class TaskAnalyzer:
      def analyze_task(self, task_description):
          # NLP analysis
          complexity_score = self.complexity_model.predict(description)

          # Time estimation
          time_estimate = self.time_model.predict(
              features=[complexity_score, user_history, task_type]
          )

          return {
              'complexity': complexity_score,
              'estimated_time': time_estimate,
              'suggested_priority': self.calculate_priority()
          }

  10. CRITERIOS DE LANZAMIENTO

  10.1 Go/No-Go Criteria

  - AI model accuracy >75% en dataset de prueba
  - Load testing exitoso (1K concurrent users)
  - Security audit completado
  - GDPR compliance verificado
  - Beta testing con 100 usuarios completado