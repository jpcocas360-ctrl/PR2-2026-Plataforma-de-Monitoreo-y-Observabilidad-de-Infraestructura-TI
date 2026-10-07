# Plataforma de Monitoreo y Observabilidad de Infraestructura TI

**Equipo de Desarrollo:** ByteCraft Solutions | **Gestión:** 2026 | **Materia:** Sistemas Operativos 2

---

## 1. Descripción y Propósito del Proyecto

Las infraestructuras informáticas institucionales, tales como los laboratorios y centros de cómputo universitarios, frecuentemente operan bajo un esquema de administración reactiva. En este modelo, los administradores de red y sistemas identifican y resuelven incidentes únicamente después de que los servicios han experimentado caídas, lo que genera altos tiempos de inactividad (downtime) y afecta directamente el desarrollo de las actividades académicas y administrativas.

El propósito central de este proyecto es diseñar e implementar una transición técnica hacia una **gestión preventiva**. A través de la construcción de una plataforma centralizada de monitoreo basada en tecnologías de código abierto, el sistema permitirá recolectar, almacenar y visualizar en tiempo real el estado de los recursos críticos de la infraestructura (uso de CPU, consumo de memoria RAM, saturación de almacenamiento y tráfico de red). Asimismo, el sistema contará con la capacidad de emitir alertas automáticas tempranas ante anomalías o el sobrepaso de umbrales críticos, mitigando el riesgo de caídas masivas.

## 2. Arquitectura y Stack Tecnológico

La plataforma está diseñada sobre los estándares actuales de la industria para observabilidad nativa de la nube, garantizando eficiencia, bajo consumo de recursos y alta escalabilidad:

* **Prometheus:** Actuará como el motor central (Base de datos de series temporales - TSDB) encargado de recolectar (hacer *scraping*) y almacenar las métricas de la infraestructura mediante su lenguaje de consultas PromQL.
* **Grafana:** Herramienta de visualización avanzada que se conectará a Prometheus para generar paneles de control (dashboards) interactivos y dinámicos para el análisis de los datos.
* **Agentes de Recolección:** Se emplearán exportadores ligeros como Node Exporter, SNMP Exporter y cAdvisor instalados en los equipos objetivo para extraer las métricas del hardware y del sistema operativo.
* **Docker y Docker Compose:** La orquestación y el despliegue de los servicios centrales se realizará mediante contenedores, asegurando un entorno aislado, reproducible y libre de conflictos de dependencias, alojado sobre el hipervisor Proxmox VE.

## 3. Usuarios Principales y Beneficios

* **Administradores de Red y Sistemas TI:** Obtendrán visibilidad total e instantánea del rendimiento del hardware, eliminando la necesidad de resolver incidentes "a ciegas".
* **Personal de Soporte Técnico:** Contarán con herramientas automatizadas para la detección de cuellos de botella preventivos antes de que los usuarios finales reporten fallas.
* **Estudiantes y Docentes (Usuarios Finales):** Se beneficiarán de manera indirecta al contar con servicios estables y laboratorios informáticos con tiempos de inactividad reducidos al mínimo.

## 4. Integrantes y Roles

El equipo de trabajo opera bajo un marco ágil adaptado a equipos pequeños, garantizando la integración continua y la distribución equilibrada de las responsabilidades de ingeniería:

| Integrante | Rol y Responsabilidad Principal |
|---|---|
| **Juan Gabriel Ortega Orellana** | Project Manager & Frontend Developer (Coordinación general, diseño UX, integración visual de Dashboards y gestión del proyecto) |
| **Nathan Ezequiaz Torrico Torrez** | Systems & Infrastructure Engineer (Configuración del entorno de virtualización en Proxmox VE y despliegue de Agentes de recolección de red) |
| **Juan Pablo Coca Soliz** | DevOps & Backend Specialist (Despliegue automatizado de la infraestructura central mediante Docker, interconexión de servicios y reglas de Alertas) |

## 5. Organización del Repositorio y Documentación

Este repositorio funciona como el centro de control oficial del proyecto durante el semestre. La estructura inicial de los directorios para la documentación técnica y planificación es la siguiente:

```text
/
├── README.md
├── docs/
│   ├── proyecto/
│   │   ├── Monitoreo de Infraestructura TI.pdf
│   │   └── Plataforma de Monitoreo y Observabilidad de Infraestructura TI (1).pdf
│   └── planificacion/
│       └── diagrama de gantt.xlsx
└── equipo/
    ├── Juan Pablo.txt
    ├── NathanEzequiazTorrico.txt
    └── Nombre Juan Gabriel.txt
(Nota: En etapas posteriores, este repositorio alojará los directorios /src y /config correspondientes al código fuente, los archivos docker-compose y la configuración de infraestructura como código).

6. Estado Actual y Fases del Proyecto
El desarrollo se encuentra estructurado con base en el Diagrama de Gantt oficial. Actualmente, el proyecto ha superado con éxito la fase de planificación y se encuentra ingresando a la etapa de despliegue técnico:

Fase de Inicio y Planificación (Completada):

[x] Definición de la problemática, objetivos, alcance técnico y selección del stack de herramientas.

[x] Estructuración del repositorio oficial como centro de control del equipo.

[x] Consolidación de la documentación formal y el cronograma de actividades (Gantt).

[x] Preparación y configuración de la red y el entorno de virtualización base en Proxmox VE.

Fase de Desarrollo y Despliegue (En Progreso):

[ ] Creación e implementación de tareas de ingeniería mediante la plataforma de Issues de GitHub.

[ ] Instalación del motor Docker y estructuración del archivo docker-compose.yml.

[ ] Despliegue automatizado del servidor central (Prometheus y Grafana).

[ ] Despliegue de los primeros agentes de recolección en los entornos de prueba para validar la extracción de métricas.