# CLAUDE.md

Este archivo proporciona orientación a Claude Code (claude.ai/code) al trabajar con código en este repositorio.

## Resumen del Proyecto

SisCredi es un sistema de gestión de créditos basado en Django para prestamistas individuales e instituciones financieras en República Dominicana. El sistema gestiona clientes, préstamos, pagos y garantías con analítica predictiva y perfilado de riesgo potenciado por ML.

## Arquitectura

### Estructura Multi-Tenancy
- **Usuarios Primarios**: Administradores del sistema que contratan servicios, gestionan usuarios secundarios
- **Usuarios Secundarios**: Usuarios operacionales vinculados a usuarios primarios, realizan operaciones CRUD
- **Clientes**: Clientes finales que reciben notificaciones y pueden consultar estado de créditos vía WhatsApp

### Estructura de Apps Django
- `core`: App central para funcionalidad compartida
- `autenticacion`: Autenticación y gestión de usuarios
- `usuarios`: Perfiles y gestión de usuarios (Primarios/Secundarios)
- `clientes`: Datos y perfiles de clientes
- `prestamos`: Gestión y procesamiento de préstamos
- `pagos`: Seguimiento y procesamiento de pagos
- `cotizaciones`: Sistema de generación de cotizaciones
- `consultas`: Funcionalidad de consultas y búsquedas
- `analisis`: Analítica ML y perfilado de riesgo
- `informes`: Generación de reportes
- `main`: Punto de entrada principal de la aplicación

## Stack Tecnológico

- **Backend**: Python 3.13.7+, Django 5.2.5+, Django REST Framework
- **Base de Datos**: PostgreSQL con aislamiento multi-tenancy
- **ML/AI**: APIs open-source, scikit-learn para modelos predictivos
- **Frontend**: HTML, CSS, JavaScript con Bootstrap
- **Cache**: Redis
- **Cola de Tareas**: Celery con Redis broker
- **Deployment**: AWS Elastic Beanstalk

## Comandos de Desarrollo

### Operaciones de Base de Datos
```bash
# Crear migraciones para las apps
python manage.py makemigrations

# Aplicar migraciones
python manage.py migrate

# Verificar configuración de base de datos
python manage.py check --database default

# Mostrar estado de migraciones
python manage.py showmigrations
```

### Operaciones del Servidor
```bash
# Ejecutar servidor de desarrollo
python manage.py runserver

# Crear superusuario
python manage.py createsuperuser

# Django shell
python manage.py shell
```

### Configuración de Base de Datos
El proyecto usa PostgreSQL con conexión basada en servicio:
- Nombre del servicio: `my_service`
- Archivo de contraseña: `.my_pgpass` (crear si no existe)
- Arquitectura multi-tenant con aislamiento de datos por ID de usuario

## Directrices Clave de Desarrollo

### Diseño de Modelos
Todos los modelos deben soportar multi-tenancy a través de asociación de usuarios. Cada entrada de datos debe estar vinculada a un ID de usuario Primario o Secundario para el aislamiento adecuado de datos.

### Enfoque de Integración ML
El sistema está diseñado para alimentar modelos ML para:
- Perfilado de riesgo de clientes
- capacidad de pago con relacion a los ingresos
- Predicción de comportamiento de pagos
- Análisis de cartera de créditos
- Generación automatizada de reportes

### Sistema de Notificaciones
Implementar notificaciones en tiempo real para:
- Creación/actualización de créditos
- Recordatorios y confirmaciones de pagos
- Alertas del sistema a usuarios primarios
- Integración WhatsApp para comunicación con clientes

### Consideraciones de Seguridad
- El aislamiento de datos multi-tenant es crítico
- Rate limiting por usuario e IP
- Encriptación de datos sensibles
- Sistema de autenticación integrado de Django

## Estado del Proyecto
Este es un proyecto en etapa temprana con la estructura básica de Django implementada. Todas las apps están registradas en `INSTALLED_APPS` pero los modelos están vacíos y listos para desarrollo. El sistema sigue las especificaciones del PRD para una plataforma freemium de gestión de créditos.

## Idioma
Todo el desarrollo debe conducirse en español según los requerimientos del proyecto y mercado objetivo (República Dominicana).

## instrucciones para cada implementacion

- no realices o implementes modificaciones hasta que tengas total confianza  de lo que sabes que vas a crear o implementar
- siempre hazme preguntas de seguimientos hasta que logres la confianza necesaria
- siempre utiliza y apegate a los principios SOLID
- para la base de datos apegate a los principios ACID
- siempre utiliza las herramientas por defecto de Django para las tareas comunes y generales del desarrollo web
- siempre mantener la linea de desarrollo que esta implementados en los documentos oficiales de Django para las correctas practicas
- mantener las codificaciones, desarrollo e implementaciones simples, entendibles y escalables
- mantener las variables implementadas/creadas con nombres simples de identificar y en español
- comentar cada apartado explicado de manera simple y entendible cada apartado o funciones del codigo (en español)
- nunca asumir nada, siempre analiza e investiga antes de asumir
- antes de cada implementacion, primero explica el "por qué", "como", y "para que"

## Plan de Desarrollo Secuencial - SisCredi

### **FASE 1: Fundación del Sistema (2-3 semanas)**

#### **1.1 Modelos de Usuarios y Autenticación**
**Por qué empezar aquí:**
- Django se basa en usuarios para todo (permisos, sesiones, multi-tenancy)
- Sin usuarios definidos, no puedes implementar aislamiento multi-tenant
- Es la base para todas las demás funcionalidades

**Implementar:**
- Extender `User` de Django para Usuarios Primarios/Secundarios
- Modelo `PerfilUsuario` con campos específicos del negocio
- Sistema de permisos personalizado
- Middleware para multi-tenancy

#### **1.2 Modelo Core y Base**
**Por qué después de usuarios:**
- Necesitas saber quién crea/modifica cada registro
- Establece patrones reutilizables para todas las apps
- Define campos comunes (timestamps, usuario_creador, etc.)

**Implementar:**
- Clase abstracta `ModeloBase` con campos comunes
- Configuración de zona horaria para RD
- Validadores personalizados comunes

### **FASE 2: Entidades de Negocio Core (3-4 semanas)**

#### **2.1 App Clientes**
**Por qué primero clientes:**
- Sin clientes no hay préstamos ni pagos
- Valida el sistema multi-tenant desde el inicio
- Permite probar CRUD básico antes de lógica compleja

**Implementar:**
- Modelo `Clientes` (persona física/jurídica)
- Campos para ML (ingresos, historial, referencias)
- Sistema de documentos adjuntos
- Validaciones de cédula/RNC dominicanos

#### **2.2 App Prestamos**
**Por qué después de clientes:**
- Depende directamente de clientes existentes
- Contiene la lógica de negocio central
- Base para cálculos financieros y ML

**Implementar:**
- Modelo `Prestamos` con cálculos automáticos
- Estados del préstamo (solicitado, aprobado, activo, cerrado)
- Cálculo de intereses y cuotas
- Integración con app `cotizaciones`

#### **2.3 App Pagos**
**Por qué después de préstamos:**
- Los pagos dependen de préstamos existentes
- Genera data histórica para ML
- Crítico para flujo de caja del usuario

**Implementar:**
- Modelo `Pagos` vinculado a préstamos
- Cálculo automático de saldos
- Estados de pago y mora
- Triggers para notificaciones

### **FASE 3: Lógica de Negocio Avanzada (2-3 semanas)**

#### **3.1 App Cotizaciones**
**Por qué en esta fase:**
- Requiere datos de clientes y préstamos existentes
- Necesita lógica de cálculo ya probada
- Mejora UX antes de implementar ML

**Implementar:**
- Sistema de cotización automática
- Múltiples escenarios de pago
- Exportación a PDF
- Integración con ML básico

#### **3.2 App Consultas**
**Por qué ahora:**
- Ya tienes datos para consultar
- Optimiza performance antes de ML pesado
- Identifica patrones para alimentar ML

**Implementar:**
- Queries optimizadas con índices
- Filtros avanzados
- Exportación de datos
- APIs para análisis

### **FASE 4: Interfaz y Experiencia (2-3 semanas)**

#### **4.1 Templates y Frontend**
**Por qué después de lógica:**
- La lógica backend debe estar sólida
- Evita rehacer interfaces por cambios de lógica
- Permite focus en UX sin preocuparse por bugs

**Implementar:**
- Templates base con Bootstrap
- Dashboard principal
- Formularios optimizados
- JavaScript para interactividad

#### **4.2 App Main (Punto de Entrada)**
**Por qué al final de esta fase:**
- Necesita todas las otras apps funcionando
- Dashboard requiere data real
- Punto de integración de todas las funcionalidades

**Implementar:**
- Dashboard con métricas
- Navegación principal
- Widgets de estado
- Shortcuts a funciones principales

### **FASE 5: Inteligencia y Automatización (3-4 semanas)**

#### **5.1 App Analisis (ML Básico)**
**Por qué después de tener datos:**
- ML necesita datos históricos reales
- Requiere patrones identificables
- Base para predicciones

**Implementar:**
- Modelos ML básicos con scikit-learn
- Análisis de riesgo crediticio
- Predicción de pagos
- Scoring de clientes

#### **5.2 App Informes**
**Por qué después de análisis:**
- Los informes incluyen insights ML
- Requiere data procesada y analizada
- Valor agregado del sistema

**Implementar:**
- Generación automática de reportes
- Exportación múltiples formatos
- Reportes programados
- Visualizaciones con charts

### **FASE 6: Comunicación y Notificaciones (2-3 semanas)**

#### **6.1 Sistema de Notificaciones**
**Por qué casi al final:**
- Requiere todas las funcionalidades implementadas
- Integra con servicios externos (WhatsApp, Email)
- Feature de diferenciación

**Implementar:**
- Cola de tareas con Celery
- Integración WhatsApp Business API
- Templates de notificaciones
- Programación automática

### **FASE 7: Optimización y Producción (2-3 semanas)**

#### **7.1 Performance y Seguridad**
**Por qué al final:**
- Optimizas lo que ya funciona
- Identificas bottlenecks reales
- Preparas para escalar

**Implementar:**
- Caching con Redis
- Optimización de queries
- Rate limiting
- Security headers

#### **7.2 Testing y Deploy**
**Por qué último:**
- Testa funcionalidades completas
- Deploy de sistema funcional
- Preparado para usuarios reales

**Implementar:**
- Tests unitarios y de integración
- CI/CD pipeline
- Deploy AWS Elastic Beanstalk
- Monitoreo y logs

## **Principio Rector:**
Cada fase construye sobre la anterior y **valida la arquitectura multi-tenant** desde el inicio. Esto asegura que no tengas que refactorizar grandes porciones cuando implementes funcionalidades avanzadas.