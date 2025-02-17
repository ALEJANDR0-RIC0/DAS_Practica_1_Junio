# Sistema para reportar incidencias

* Status: Accepted
* Date: 16/02/2025
* Decision-Makers: Alejandro Rico, Elena Ceinos
* Consulted: Gaizka Aranbarri, Alberto Acebes
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor
---

## Context and Problem Statement

Se necesita poder gestionar incidencias de manera eficiente y rápida, asegurando que los problemas sean reportados y atendidos en el menor tiempo posible para minimizar el impacto en las operaciones.

## Drivers de decisión

* RF-07: Reportar incidencias cuando sucedan

## Considered Options

* **0004-1-Integrar una API de mensajería existente**
* **0004-2.1-Desarrollar un sistema propio de notificaciones**
* **0004-2.2-Utilizar el patron observer para gestionar los pedidos y las incicencias**

## Pros and Cons of the Options

### 0004-1-Integrar una API de mensajería existente

* **Good** porque permite una implementación rápida utilizando APIs populares como Twilio, Slack o Telegram.  
* **Good** porque ofrece alta fiabilidad y escalabilidad, siendo soluciones probadas y ampliamente utilizadas.  
* **Bad** porque introduce un costo recurrente dependiendo del volumen de mensajes enviados.  
* **Bad** porque limita la personalización del sistema de notificaciones.  

### 0004-2.1-Desarrollar un sistema propio de notificaciones

* **Good** porque permite personalizar completamente las notificaciones y su integración con el resto del software.  
* **Good** porque no depende de servicios de terceros, eliminando costos recurrentes a largo plazo.  
* **Bad** porque requiere un mayor tiempo y esfuerzo de implementación, lo que podría retrasar otros desarrollos.  
* **Bad** porque aumenta la carga de mantenimiento y la necesidad de garantizar escalabilidad y fiabilidad.  

### 0004-2.2-Utilizar el patron observer para gestionar los pedidos y las incicencias

* **Good** porque los observadores son notificados automáticamente de los cambios en el sujeto, lo que asegura que siempre tengan la información más reciente.
* **Good** porque los observadores y el sujeto están desacoplados, lo que significa que pueden cambiar independientemente sin afectar al otro. Esto facilita la mantenibilidad y la escalabilidad del sistema.
* **Bad** porque no hay garantía sobre el orden en que los observadores serán notificados, lo que puede ser problemático en algunos casos.
* **Bad** porque puede ser difícil de depurar y rastrear el flujo de notificaciones, especialmente en sistemas complejos con muchos observadores.


## Decision Outcome

* **Chosen option: "0004-1-Integrar una API de mensajería existente"**
Se integrará una API de mensajería, como Twilio para notificaciones SMS o Slack/Telegram para mensajes en tiempo real, asegurando que las incidencias sean reportadas de manera rápida y fiable (queda pendiente decidir la API).

### Positive Consequences

* Se garantiza una implementación más rápida, alineada con los tiempos del proyecto.  
* La solución es altamente fiable y escalable, manejando picos de notificaciones sin problemas.  
* La integración con APIs populares proporciona acceso a funcionalidades avanzadas como logs de mensajes, reintentos automáticos y reportes de estado.

### Negative Consequences

* Se asume un costo recurrente por el uso de la API, que dependerá del volumen de incidencias reportadas.  
* La personalización estará limitada por las características de la API elegida.  