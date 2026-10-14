# Plataforma de Monitoreo y Observabilidad de Infraestructura TI

**Equipo:** ByteCraft Solutions · **Asignatura:** Sistemas Operativos 2 · **Gestión:** 2026

## Resumen

En los laboratorios universitarios, los fallos de servidores y la saturación de recursos pueden detectarse cuando ya interrumpen las actividades académicas. El personal de TI necesita conocer el estado de los equipos y recibir avisos oportunos para investigar antes de una interrupción. Este proyecto implementa y demuestra ese flujo preventivo en un entorno de prueba, sin afirmar una reducción cuantificada del downtime institucional.

**Entrega prevista:** 11 de diciembre de 2026. **Estado al 14 de octubre:** fases 1–3 completadas; preparación de infraestructura en curso. Docker y Docker Compose figuran al 30 % en el Gantt. Prometheus, Grafana, agentes, dashboards y alertas aún deben implementarse y validarse según el cronograma.

## Usuarios y valor esperado

- **Usuario principal: administrador o responsable de TI.** Necesita consultar el estado y las tendencias de CPU, memoria, almacenamiento y red, y recibir avisos accionables.
- **Personal de soporte.** Necesita datos para investigar incidentes sin diagnosticar a ciegas.
- **Docentes y estudiantes.** Son beneficiarios indirectos si la detección oportuna permite intervenir antes de afectar las actividades.

El problema parte del diagnóstico del equipo. El repositorio todavía no presenta registros institucionales ni mediciones de frecuencia o duración de incidentes. Para validar la necesidad, el equipo debe documentar una entrevista con un responsable de TI o una fuente verificable de incidentes. El prototipo medirá el funcionamiento técnico en el host de prueba; no permitirá afirmar por sí solo que bajó el downtime de la universidad.

## Objetivo y alcance

**Objetivo general:** antes del 11 de diciembre de 2026, desplegar y demostrar en un entorno virtual de prueba una plataforma que recolecte métricas de un host, las presente en un dashboard y envíe a Telegram una alerta ante una condición crítica definida.

**Incluye:** VM sobre Proxmox VE; Docker Compose; Prometheus y Grafana; Node Exporter en un servidor Ubuntu de prueba; paneles de CPU, RAM, disco y red; una regla de alerta con notificación a Telegram; pruebas funcionales, documentación y demostración.

**Fuera del alcance del MVP:** despliegue en producción institucional, monitoreo de todos los laboratorios, alta disponibilidad, recuperación ante desastres, varios canales de notificación y medición cuantitativa del impacto institucional. SNMP Exporter y cAdvisor son ampliaciones; se abordarán después de aceptar el MVP y solo si hay tiempo y acceso.

## MVP y criterios de aceptación

El MVP es un despliegue reproducible de Prometheus y Grafana con Docker Compose en la VM `Lab-SO2-Prueba`, que recibe métricas mediante Node Exporter, muestra CPU, memoria, disco y red, y envía una alerta de prueba a Telegram.

- **Servicios:** Prometheus y Grafana arrancan desde la configuración versionada, quedan accesibles y conservan sus datos configurados después de reiniciar.
- **Recolección:** el target de Node Exporter aparece `UP` en Prometheus y devuelve muestras recientes del host acordado.
- **Dashboard:** Grafana muestra datos identificados y unidades legibles para CPU, memoria, disco y red.
- **Alerta:** con CPU superior al 85 % durante más de cinco minutos continuos, la regla genera una alerta de severidad alta y se recibe el mensaje en el bot `ByteCraft_AlertBot`. Responsable de atenderla: Juan Pablo Coca Soliz.
- **Repetibilidad:** un integrante distinto de quien preparó el despliegue completa el procedimiento siguiendo el manual y registra cualquier paso confuso.

Las pruebas previstas cubren arranque, recolección, dashboard, activación controlada de alertas, persistencia y repetición por otro integrante. Las pruebas de carga se ejecutarán después de las pruebas funcionales, con límites seguros y registro del consumo de recursos. La configuración o prueba independiente del webhook de Telegram no sustituye la prueba end-to-end de la alerta desde Prometheus.

## Arquitectura y decisiones técnicas

```text
Proxmox VE
└── VM Ubuntu Server 24.04: Lab-SO2-Prueba
    ├── Docker Compose
    │   ├── Prometheus ← scrape cada 15 s ← Node Exporter
    │   └── Grafana ← dashboards y consultas a Prometheus
    └── Alerta de CPU → Telegram: ByteCraft_AlertBot
```

- **VM:** Ubuntu Server 24.04, 2 vCPU, 4 GB RAM, disco de 32 GB, IP estática y firewall interno configurado. Nathan Ezequiaz Torrico validó el acceso por SSH.
- **Métricas:** intervalo de scrape de 15 segundos y retención de Prometheus de 15 días, ajustada al disco de 32 GB.
- **Alerta crítica:** CPU >85 % durante más de 5 minutos; severidad alta; atención a cargo de Juan Pablo Coca Soliz.
- **Canal:** Telegram es el único canal del MVP. El equipo reporta el webhook de `ByteCraft_AlertBot` configurado y probado; falta conservar evidencia de la integración end-to-end prevista en el Gantt.
- **Ampliaciones:** SNMP Exporter para métricas de red y cAdvisor para métricas de contenedores. No son dependencias para aceptar el MVP.

Las dependencias externas son acceso al hipervisor Proxmox y a la VM, conectividad entre host y contenedores, reglas de firewall, disponibilidad de Docker y acceso de salida a Telegram. La solución es un prototipo académico, no un servicio de producción.

## Datos, seguridad y calidad

Se recolectarán métricas técnicas del host y disponibilidad de los targets; no se prevé recopilar datos personales. Los tokens, contraseñas y secretos de Telegram no se guardarán en Git. Se restringirán puertos y acceso administrativo, se cambiarán las credenciales predeterminadas de Grafana y se documentarán versiones, configuración y recuperación. Si se habilita SNMP como ampliación, se utilizarán credenciales de solo lectura.

## Equipo y forma de trabajo

| Integrante | Responsabilidad y entregables principales |
|---|---|
| **Juan Gabriel Ortega Orellana** | Coordinación, requisitos, UX, dashboards y consolidación de documentación. |
| **Nathan Ezequiaz Torrico** | Proxmox, VM, Docker, conectividad y agentes de recolección. |
| **Juan Pablo Coca Soliz** | Docker Compose, Prometheus, Grafana, reglas y alertas. |

El Gantt asigna responsables y apoyo cruzado en varias tareas técnicas. Para integrar el trabajo, el equipo gestionará las tareas mediante GitHub Issues, cambios en ramas y revisión de otro integrante; revisará bloqueos y progreso semanalmente. Cada cambio debe dejar evidencia del criterio de aceptación correspondiente.

## Plan de trabajo

El cronograma contiene **nueve fases y 36 tareas**, del 12 de agosto al 11 de diciembre de 2026. Las tareas incluyen responsables, fechas, dependencias, entregables o criterios, clasificación MVP/ampliación, progreso y estado. Las fechas se solapan cuando hay trabajo paralelo; el Gantt es la fuente de detalle y estado vigente.

| Fase | Periodo | Resultado principal |
|---|---|---|
| 1. Inicio y planificación | 12–31 ago | Problema, alcance, requisitos y objetivos definidos. |
| 2. Investigación y diseño | 1–25 sep | Investigación técnica, arquitectura y entorno Proxmox. |
| 3. Documentación y validación del diseño | 21 sep–7 oct | Informe inicial revisado y corregido. |
| 4. Preparación de infraestructura | 23 sep–20 oct | VM, Docker y Docker Compose listos. Docker y Compose: 30 % al corte del 14 oct. |
| 5. Despliegue de la plataforma | 19–30 oct | Prometheus, Grafana y comunicación validados. |
| 6. Agentes y recolección | 28 oct–13 nov | Node Exporter integrado; SNMP y cAdvisor como ampliaciones. |
| 7. Dashboards y visualización | 10–27 nov | Paneles de infraestructura integrados y revisados. |
| 8. Alertas y pruebas | 23 nov–5 dic | Regla, Telegram, pruebas funcionales y evaluación de carga. |
| 9. Documentación y entrega | 30 nov–11 dic | Manual, correcciones, informe y presentación final. |

**Siguiente trabajo:** terminar Docker y Compose; desplegar Prometheus y Grafana; integrar Node Exporter y confirmar métricas; crear dashboard; validar alerta Telegram end-to-end; realizar pruebas; documentar y preparar la entrega. SNMP Exporter y cAdvisor no deben retrasar ese recorrido mínimo.

## Riesgos y respuesta

| Riesgo | Mitigación y señal de control |
|---|---|
| Caída de red de Proxmox que aísle los contenedores. | Comprobar conectividad y firewall en cada integración; registrar rutas y pasos de recuperación. |
| Saturación del disco por retención o carga. | Mantener retención en 15 días, monitorear el disco del servidor central y ejecutar una prueba de estrés semanal. |
| Fallo de integración entre exporter, Prometheus, Grafana y Telegram. | Probar temprano el flujo vertical, validar cada target y repetir la prueba end-to-end antes de la entrega. |
| Indisponibilidad de una persona clave. | Mantener instrucciones versionadas, apoyo cruzado y una prueba de despliegue realizada por otro integrante. |

## Documentos del proyecto

- [Informe actualizado del proyecto (DOCX)](docs/proyecto/Informe_Proyecto_Monitoreo_Observabilidad.docx): alcance, objetivos, requisitos, arquitectura, seguridad, riesgos, preparación y pruebas.
- [Presentación del proyecto (PDF)](docs/proyecto/Monitoreo%20de%20Infraestructura%20TI.pdf): resumen visual para exposición.
- [Diagrama de Gantt corregido (Excel)](docs/planificacion/gantt.xlsx): tareas, responsables, dependencias, criterios, clasificación y avance.
- [Perfiles del equipo](equipo/): roles y responsabilidades individuales.

## Estructura del repositorio

```text
.
├── README.md
├── docs/
│   ├── planificacion/
│   │   └── gantt.xlsx
│   └── proyecto/
│       ├── Informe_Proyecto_Monitoreo_Observabilidad.docx
│       └── Monitoreo de Infraestructura TI.pdf
└── equipo/
    ├── juan-gabriel-ortega-orellana.txt
    ├── nathan-ezequiaz-torrico.txt
    └── juan-pablo-coca-soliz.txt
```

El repositorio contiene actualmente documentación y planificación. La implementación técnica se irá incorporando conforme se complete; no se debe asumir que los servicios ya están desplegados hasta que el Gantt y la evidencia de pruebas lo confirmen.

**Fecha prevista de entrega:** 11 de diciembre de 2026.