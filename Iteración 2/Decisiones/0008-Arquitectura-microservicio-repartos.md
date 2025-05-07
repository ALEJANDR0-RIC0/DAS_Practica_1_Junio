# Modelado arquitectónico del microservicio de Repartos
* Status: Accepted
* Date: 26/03/2025
* Decision-Makers: Alejandro Rico, Elena Ceinos  
* Consulted: Gaizka Aranbarri, Alberto Acebes  
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor  
---

## Context and Problem Statement

El servicio de Repartos es responsable de organizar la entrega de los pedidos realizados por los clientes. Esto implica coordinar camiones, rutas, asignaciones, y resolver incidencias logísticas. Dado su impacto en la experiencia del usuario y su integración con otros microservicios (Pedidos, Incidencias, Notificaciones), se necesita decidir cómo modelarlo arquitectónicamente y qué componentes formarán parte de su diseño.

---

## Drivers de Decisión

* RF-04: Gestionar el reparto y las rutas de los camiones
* RF-05: Mostrar estadísticas del estado de los pedidos, la situación de los camiones y el estado del pedido

---

## Considered Options

### 0008-1: Modelado monolítico dentro del servicio de pedidos
* **Good**: Evita duplicación de datos.
* **Bad**: Aumenta el acoplamiento, dificulta la escalabilidad y separación de responsabilidades.

### 0008-2: Microservicio de Repartos con responsabilidad propia
* **Good**: Desacopla la lógica logística del pedido.
* **Good**: Permite especialización, escalabilidad y evolución independiente.
* **Bad**: Requiere sincronización con otros servicios vía eventos.

### 0008-3: Integración con sistema externo de logística
* **Good**: Outsourcing completo de la lógica de reparto.
* **Bad**: Pérdida de control, dependencia externa y costes asociados.

---

## Decision Outcome

**Chosen option: "0008-2 - Microservicio de Repartos con responsabilidad propia"**

Se implementará un microservicio independiente para Repartos que gestionará internamente las rutas (gestorRutas), la asignación de camiones, y la trazabilidad de entregas. Se comunicará con los servicios de Pedidos, Incidencias y Notificaciones mediante eventos de dominio.

---

## Positive Consequences

* Se mejora la separación de responsabilidades (SoC).
* Escalabilidad independiente según la carga logística.
* Facilita el registro, trazabilidad y análisis de entregas.
* Permite una integración posterior con mapas, geolocalización o IA de optimización de rutas.

---

## Negative Consequences

* Requiere sincronización de datos y estados entre Pedidos y Repartos.
* Aumenta la complejidad de coordinación entre servicios.

---

## Clases que se añaden

- `Camion`: representa un vehículo con matrícula, capacidad, estado y localización.
  - **Necesaria para** gestionar los recursos físicos de reparto.

- `Ruta`: contiene el trayecto, las paradas y el estado del recorrido asignado.
  - **Necesaria para** planificar y monitorizar las entregas.

- `AsignacionEntrega`: representa la relación entre pedido, camión y ruta.
  - **Necesaria para** coordinar pedidos concretos con su logística.

- `GestorRutas`: clase responsable de asignar camiones y rutas a los pedidos pendientes, integrando el algoritmo de rutas.
  - **Necesaria porque** encapsula la lógica de planificación logística.

- `EstadisticasPedido`: clase que permite consultar las diferentes estadísticas sobre los pedidos.
---
