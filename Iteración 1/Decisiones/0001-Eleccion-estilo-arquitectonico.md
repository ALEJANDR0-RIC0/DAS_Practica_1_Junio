# Elección de arquiterctura de cliente-servidor
* Status: Accepted
* Date: 2024-11-12
* Decision-Makers: Alejandro Rico, Elena Ceinos
* Consulted: Gaizka Aranbarri, Alberto Acebes
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor
---

## Context and Problem Statement
La empresa pretende migrar de una 

## Considered Options

* **0001-1-utilizar-arquitectura-cliente-servidor**

## Decision Outcome

Chosen option: "0001-1-utilizar-arquitectura-cliente-servidor"

### Consequences

### Positive Consequences

* Reducción de duplicación: Al centralizar la lógica en el servidor, se evita duplicar funciones críticas como la gestión de rutas o el procesamiento de pagos en los clientes.
* Escalabilidad del cliente: Permite soportar una mayor variedad de plataformas de cliente (PC, móvil, tabletas) con una interacción mínima, ya que la lógica principal está en el servidor.
* Soporte a múltiples clientes simultáneos: Es ideal para manejar un gran número de usuarios simultáneos con peticiones diversas, como pedidos o consultas de rutas.


### Negative Consequences

* Requerimientos de conectividad: Los clientes necesitan una conexión constante y confiable para interactuar con el servidor, lo que podría ser problemático en áreas con baja conectividad.
* Complejidad en la sincronización: Si los clientes necesitan operar parcialmente offline, mantener la consistencia de datos entre cliente y servidor añade complejidad.