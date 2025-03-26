# Estrategia de gestión de la base de datos para entidades principales

* Status: Accepted  
* Date: 26/03/2025  
* Decision-Makers: Elena Ceinos, Alejandro Rico  
* Consulted: Gaizka Aranbarri, Alberto Acebes  
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor  

---

## Context and Problem Statement

En la arquitectura distribuida planteada, se necesita decidir cómo modelar la persistencia de datos para las entidades principales `Cliente` y `Pedido`. Estas entidades están en el centro del dominio y se relacionan directamente con otros servicios como pagos, estadísticas e incidencias. La decisión afectará al diseño general de las clases, su almacenamiento y su reutilización.

---

## Considered Options

**Opción 1:** Compartir una base de datos común entre microservicios para simplificar la integración.  
**Opción 2:** Separar por completo las bases de datos y modelar `Cliente` y `Pedido` como entidades independientes en cada una.  
**Opción 3:** Utilizar una base de datos federada con vistas compartidas entre servicios para facilitar reporting.

---

## Decision Outcome

Se decide que `Cliente` y `Pedido` se definan como entidades independientes en su propio microservicio y se persistan en instancias separadas de base de datos SQL. Estas instancias contendrán clases `ClienteEntity` y `PedidoEntity`, modeladas según JPA/Hibernate para facilitar la interacción con la base de datos. Esto asegura el aislamiento, la escalabilidad, y la integridad de los datos en cada servicio.

---

## Clases que se añaden

- `ClienteEntity`  
- `PedidoEntity`  
- `ClienteRepository`  
- `PedidoRepository`  

---
