# Que API de mensajerría utilizar para reportar y gestionar incidencias

* Status: Accepted
* Date: 16/02/2025
* Decision-Makers: Alejandro Rico, Daniel Rong
* Consulted: Elena Ceinos, Gaizka Aranbarri
* Informed: Jon Mazcuñán, Alberto Acebes, Pablo Villamayor

## Context and Problem Statement

Se necesita seleccionar una API de mensajería adecuada para gestionar las incidencias y las notificaciones relacionadas con estas. Esta decisión es crucial para asegurar que las incidencias se reporten y notifiquen de manera eficiente y fiable, permitiendo una rápida respuesta y resolución.

## Drivers de decisión

* RF-07: Reportar incidencias cuando sucedan

## Considered Options

* **0005-1-Twilio**
* **0005-2-Slack**
* **0005-3-Telegram**

## Pros and Cons of the Options

### 0005-1-Twilio

* **Good** porque ofrece una integración sencilla y rápida para notificaciones SMS.  
* **Good** porque es altamente fiable y escalable, con soporte global.  
* **Bad** porque introduce un costo recurrente por cada mensaje enviado.  
* **Bad** porque puede ser costoso si el volumen de mensajes es alto.  

### 0005-2-Slack

* **Good** porque permite enviar mensajes en tiempo real a canales específicos.  
* **Good** porque es ampliamente utilizado y tiene una buena documentación y soporte.  
* **Bad** porque requiere que los usuarios estén en la plataforma Slack.  
* **Bad** porque puede no ser ideal para notificaciones SMS.  

### 0005-3-Telegram

* **Good** porque permite enviar mensajes en tiempo real y es gratuito.  
* **Good** porque tiene una API robusta y es fácil de integrar.  
* **Bad** porque requiere que los usuarios tengan la aplicación Telegram instalada.  
* **Bad** porque puede no ser tan fiable como Twilio para notificaciones críticas.  

## Decision Outcome

* **Chosen option: "0005-2-Twilio"**  
Se ha decidido utilizar Twilio para las notificaciones SMS debido a su fiabilidad, escalabilidad, facilidad de integración y la gran flexibilidad para añadir más funcionalidades. Aunque introduce un costo recurrente, se considera que los beneficios superan los inconvenientes.

### Positive Consequences

* Implementación rápida y sencilla, alineada con los tiempos del proyecto.  
* Alta fiabilidad y escalabilidad, manejando picos de notificaciones sin problemas.  
* Acceso a funcionalidades avanzadas como logs de mensajes, reintentos automáticos y reportes de estado.

### Negative Consequences

* Costo recurrente por el uso de la API, que dependerá del volumen de incidencias reportadas.  
* La personalización estará limitada por las características de la API elegida.  