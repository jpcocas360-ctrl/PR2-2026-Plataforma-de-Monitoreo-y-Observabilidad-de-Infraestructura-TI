# Plataforma de Monitoreo y Observabilidad de Infraestructura TI

**Equipo:** ByteCraft Solutions · **Asignatura:** Sistemas Operativos 2 · **Gestión:** 2026

## Propósito

Este proyecto busca ayudar al personal de TI universitario a detectar fallos y saturación de recursos antes de que interrumpan las actividades académicas. La propuesta es implementar y demostrar una plataforma de monitoreo en un entorno de prueba, con métricas, dashboards y una alerta preventiva.

## Qué se construirá

El objetivo es desplegar Prometheus y Grafana en una máquina virtual sobre Proxmox VE, utilizando Docker Compose. Node Exporter permitirá recolectar métricas de un servidor de prueba; Grafana presentará CPU, memoria, almacenamiento y red.

### MVP

La primera versión funcional incluirá:

- Prometheus y Grafana desplegados mediante Docker Compose.
- Un servidor de prueba monitoreado con Node Exporter.
- Un dashboard con las métricas prioritarias disponibles.
- Una alerta demostrada de principio a fin, enviada a un canal elegido por el equipo: Telegram o Discord.
- Instrucciones para desplegar, verificar y repetir la instalación.

**Criterio de éxito:** Prometheus recibe métricas del host; Grafana las muestra en el dashboard; una condición de prueba activa una alerta y la notificación llega al canal configurado; otro integrante puede repetir el procedimiento con la documentación.

SNMP Exporter y cAdvisor son ampliaciones condicionadas a que el MVP funcione y exista tiempo y acceso para validarlos. No forman parte del alcance mínimo.

## Arquitectura propuesta

```text
Proxmox VE
└── Máquina virtual de prueba
    ├── Docker Compose
    │   ├── Prometheus ── consulta métricas de Node Exporter
    │   └── Grafana ───── consulta Prometheus y muestra dashboards
    └── Alerta de prueba ── Telegram o Discord
```

Los componentes y configuraciones se incorporarán al repositorio conforme avance la implementación. Las credenciales y tokens no deben versionarse.

## Equipo

| Integrante | Responsabilidad principal |
|---|---|
| **Juan Gabriel Ortega Orellana** | Project Manager y Frontend Developer: coordinación, requisitos, UX y dashboards. |
| **Nathan Ezequiaz Torrico** | Systems & Infrastructure Engineer: Proxmox, Docker y agentes de recolección. |
| **Juan Pablo Coca Soliz** | DevOps & Backend Specialist: Prometheus, Grafana, integración y alertas. |

Los perfiles individuales están en [`equipo/`](equipo/).

## Documentación

- [Informe actualizado del proyecto (PDF)](docs/proyecto/informe-proyecto.pdf): problema, objetivos, equipo, arquitectura y planificación.
- [Presentación ejecutiva (PDF)](docs/proyecto/Monitoreo%20de%20Infraestructura%20TI.pdf): resumen visual para exposición.
- [Diagrama de Gantt (Excel)](docs/planificacion/gantt.xlsx): tareas, responsables, fechas, duración, progreso y estado.

## Plan de trabajo

El plan abarca del **12 de agosto al 11 de diciembre de 2026**. El informe y el cronograma detallado enumeran ocho fases; el equipo debe mantener este número y las fechas sincronizados en todos los documentos.

| Fase | Actividad | Periodo previsto |
|---|---|---|
| 1 | Inicio y planificación | 12 ago – 18 sep |
| 2 | Investigación y diseño | 1 sep – 25 sep |
| 3 | Documentación y validación del diseño | 21 sep – 7 oct |
| 4 | Preparación de infraestructura | 23 sep – 16 oct |
| 5 | Despliegue de la plataforma | 14 oct – 30 oct |
| 6 | Implementación de agentes y recolección | 28 oct – 13 nov |
| 7 | Diseño e integración de dashboards | 10 nov – 27 nov |
| 8 | Alertas, pruebas y entrega final | 23 nov – 11 dic |

Las fechas se solapan cuando hay trabajo paralelo. El Gantt debe indicar las dependencias y actualizarse con el progreso real; consultar ese archivo para el estado vigente de cada tarea.

## Estado del repositorio

El repositorio contiene actualmente el README, documentos del proyecto, cronograma y perfiles del equipo. La implementación técnica está planificada; verifica en el Gantt el estado actualizado de Docker y de las tareas de despliegue antes de asumir que los servicios ya están operativos.

## Estructura

```text
.
├── README.md
├── docs/
│   ├── planificacion/
│   │   └── gantt.xlsx
│   └── proyecto/
│       ├── informe-proyecto.pdf
│       └── Monitoreo de Infraestructura TI.pdf
└── equipo/
    ├── juan-gabriel-ortega-orellana.txt
    ├── nathan-ezequiaz-torrico.txt
    └── juan-pablo-coca-soliz.txt
```

## Entrega

**Fecha prevista:** 11 de diciembre de 2026. La demostración final debe incluir el flujo de métricas, dashboard, alerta de prueba, resultados de validación y documentación para repetir el despliegue.
