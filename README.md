# Plataforma de Monitoreo y Observabilidad de Infraestructura TI

**Equipo:** ByteCraft Solutions · **Gestión:** 2026 · **Asignatura:** Sistemas Operativos 2

## Sobre el proyecto

El proyecto propone implementar una plataforma centralizada para monitorear la infraestructura TI de laboratorios universitarios. Busca pasar de una atención reactiva de incidentes a una gestión preventiva mediante métricas, paneles y alertas tempranas.

La solución se ejecutará sobre **Proxmox VE** y utilizará **Docker Compose**, **Prometheus** y **Grafana**. Para recolectar métricas se contemplan **Node Exporter**, **SNMP Exporter** y **cAdvisor**. El alcance incluye métricas de CPU, memoria, almacenamiento y red, además de alertas automatizadas.

## Documentos del proyecto

- [Informe actualizado del proyecto](docs/proyecto/informe-proyecto.pdf): descripción, alcance, organización y propuesta técnica.
- [Presentación ejecutiva](docs/proyecto/Monitoreo%20de%20Infraestructura%20TI.pdf): resumen visual para exposición y defensa.
- [Cronograma Gantt](docs/planificacion/gantt.xlsx): planificación de fases y tareas, del 12 de agosto al 11 de diciembre de 2026.

## Equipo y responsabilidades

| Integrante | Responsabilidad |
|---|---|
| **Juan Gabriel Ortega Orellana** | Project Manager y Frontend Developer: coordinación, UX y dashboards. |
| **Nathan Ezequiaz Torrico** | Systems & Infrastructure Engineer: virtualización en Proxmox, Docker y agentes de recolección. |
| **Juan Pablo Coca Soliz** | DevOps & Backend Specialist: servidor de observabilidad con Prometheus y Grafana, integración y alertas. |

Los perfiles individuales se encuentran en [equipo/](equipo/).

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

## Estado del repositorio

Actualmente se incluyen la documentación del proyecto, la presentación, el cronograma y los perfiles del equipo. La implementación técnica prevista contempla los archivos de despliegue y configuración de Prometheus, Grafana y sus exportadores; se incorporarán al repositorio conforme avance el desarrollo.

**Entrega prevista:** 11 de diciembre de 2026.
