# Decisión: Microservicio de Noticias

* Status: Accepted
* Date: 16/02/2025
* Decision-Makers: Alejandro Rico, Elena Ceinos
* Consulted: Gaizka Aranbarri, Alberto Acebes
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor
---

## Context and Problem Statement

El microservicio de noticias es responsable de gestionar las suscripciones de los clientes a las noticias sobre el estado de los pedidos y del reparto. Además, notifica cualquier incidencia asi como reportarla relacionada con estos procesos.

## Drivers de decisión

* RF-06: Suscripción a un sistema de noticias por parte de los clientes

## Considered Options

* **0003-1-Clase principal NewsService**
* **0003-2-Clase incidence**
* **0003-3-Se conecta tanto con client como con order**

## Decision Outcome

* **Chosen options: "0003-1-Clase principal NewsService", "Clase incidence", "0003-3-Se conecta tanto con client como con order"**

### Positive Consequences

* Facilita la gestión de incidencias al centralizar la información y notificaciones relacionadas.
* Optimiza la eficiencia operativa al integrar la información de incidencias y noticias en un solo servicio.
* Facilita la escalabilidad y el mantenimiento del sistema al tener componentes desacoplados.
