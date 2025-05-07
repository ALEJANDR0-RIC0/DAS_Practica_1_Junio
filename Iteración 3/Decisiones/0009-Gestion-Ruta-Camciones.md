# Gestión de Rutas para Camiones

* Status: Acepted  
* Date: 28/05/2025  
* Decision-Makers: Alejandro Rico, Elena Ceinos  
* Consulted: Gaizka Aranbarri, Alberto Acebes  
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor  

---

## Context and Problem Statement

En una empresa de logística con una flota de más de 100 camiones, los problemas operativos (averías mecánicas, retrasos, rutas bloqueadas, etc.) generan pérdidas significativas cuando no se resuelven rápidamente.

El microservicio de **Reparto** debe optimizar la asignación de rutas a camiones, considerando:

- 📍 Ubicaciones de pedidos (destinos)  
- 🚚 Flota disponible (capacidad, ubicación actual)  
- ⏱️ Restricciones logísticas (tiempos de entrega, tráfico)

---

## Drivers de decisión

* RF-04: Gestionar el reparto y las rutas de los camiones  
* Escalabilidad y flexibilidad en la planificación de rutas dinámicas  
* Compatibilidad con arquitectura basada en eventos y microservicios

---

## Considered Options

* **0009-1-Vehicle Routing Problem (VRP) + Strategy Pattern + Event-Driven**
* **0009-2-Algoritmo de Clarke-Wright (Ahorros)**
* **0009-3-Algoritmos Genéticos**
* **0009-4-Colonia de Hormigas (ACO)**

---

## Pros and Cons of the Options

### 0009-1-Vehicle Routing Problem (VRP) + Strategy Pattern + Event-Driven

* **Good**  
  - Estándar en la industria  
  - Integra bien con eventos (Kafka)  
  - Permite cambiar algoritmos (Dijkstra → OR-Tools) sin modificar la lógica de negocio  
  - Aislado del resto del sistema mediante interfaz `IRutaStrategy`  
* **Bad**  
  - Diseño inicial más complejo  
  - Configuración técnica de OR-Tools

### 0009-2-Algoritmo de Clarke-Wright (Ahorros)

* **Good**  
  - Simple y rápido para problemas medianos  
* **Bad**  
  - No óptimo para restricciones complejas (tiempos, ventanas)

### 0009-3-Algoritmos Genéticos

* **Good**  
  - Adaptables a entornos no lineales  
* **Bad**  
  - Requiere tuning fino  
  - Difícil de mantener a largo plazo

### 0009-4-Colonia de Hormigas (ACO)

* **Good**  
  - Fuerte en entornos cambiantes  
* **Bad**  
  - Costo computacional alto  
  - Requiere mucha calibración

---

## Decision Outcome

* **Chosen Option: 0009-1 - Vehicle Routing Problem (VRP) + Strategy Pattern + Event-Driven**

Se implementará el VRP como núcleo del sistema de planificación de rutas, usando una arquitectura basada en el patrón **Strategy** y comunicación **Event-Driven** con Kafka. El algoritmo podrá ser sustituido o evolucionado (ej: Dijkstra → OR-Tools → heurísticas) sin impactar el sistema principal.

---

### Positive Consequences

* 🧠 **Desacoplamiento**: Cambios en el algoritmo no afectan al resto del sistema  
* ⚙️ **Testabilidad**: `IRutaStrategy` se puede mockear en pruebas unitarias  
* 🚀 **Flexibilidad**: Integración progresiva de OR-Tools, posibilidad de probar múltiples estrategias  
* 🧩 **Compatibilidad técnica**: Usa infraestructura existente (Kafka, microservicios)

---

### Negative Consequences

* 🔧 **Sobrecoste inicial**: Diseño de interfaz y estructura de eventos  
* 💻 **Dependencia técnica**: Necesidad de dominar OR-Tools o herramientas similares  
* 🧪 **Iteración de parámetros**: Requiere pruebas para ajuste óptimo

