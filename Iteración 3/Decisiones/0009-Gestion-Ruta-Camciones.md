# **Decisión: Arquitectura del Algoritmo de Planificación de Rutas**

* **Status:** Aprobado  
* **Fecha:** 28/05/2025  
* **Decision-Makers:** Alejandro Rico, Elena Ceinos  
* **Consulted:** Gaizka Aranbarri, Alberto Acebes  
* **Informed:** Jon Mazcuñán, Daniel Rong, Pablo Villamayor  

---

## **1. Contexto**  
El microservicio de **Reparto** requiere un algoritmo para optimizar rutas de camiones, integrado con:  
- Datos de pedidos (ubicaciones, prioridades).  
- Flota disponible (capacidad, ubicación actual).  
- Eventos en tiempo real (incidencias, tráfico).  

**Requisitos clave:**  
-**Desacoplamiento**: No afectar a otros servicios (Pedidos, Clientes).  
-**Flexibilidad**: Cambiar algoritmos fácilmente (ej: de Dijkstra a OR-Tools).  
- **Escalabilidad**: Manejar picos de pedidos.  

---

## **2. Opciones Evaluadas**

### **Opción 1: Strategy Pattern + Event-Driven**  
**Descripción:**  
Se utiliza el patrón Strategy para encapsular diferentes algoritmos de optimización de rutas (por ejemplo, Dijkstra, OR-Tools), lo que permite cambiar el algoritmo sin modificar la lógica del servicio. Se complementa con un enfoque Event-Driven donde el microservicio de Reparto reacciona a eventos (ej: PedidoConfirmado) para disparar el cálculo de rutas. 
* **Good** Bajo acoplamiento: El microservicio depende de una interfaz, no del algoritmo concreto.  
* **Good** Extensible: Nuevos algoritmos se añaden sin modificar el código existente.  
* **Good** Integración limpia: Se activa por eventos (ej: PedidoConfirmado → CalcularRuta).   
* **bad** Complejidad inicial: Requiere diseñar la interfaz y adaptadores.  

---

### **Opción 2: Servicio Externo (API REST)**  
**Descripción:**  
Un microservicio especializado (ej: Python + OR-Tools) expuesto como API REST, donde se centraliza el cálculo de rutas. El servicio de Reparto realiza una llamada HTTP para obtener la ruta optimizada.
 
* **Good** Escalabilidad independiente: El servicio de rutas escala según demanda.  
* **Good** Lenguaje óptimo: Uso de librerías específicas (ej: OR-Tools para Python).  
* **bad**Latencia: Llamadas HTTP añaden overhead.  
* **bad**Dependencia externa: Si falla, afecta a Reparto.  

---

### **Opción 3: Saga + CQRS**  
**Descripción:**  
Se utiliza un patrón Saga para coordinar el flujo de eventos entre los microservicios de Pedidos y Reparto, y CQRS para separar consultas y comandos (optimización de rutas vs. obtener rutas).

* **Good**Consistencia eventual: Ideal para procesos asíncronos largos.  
* **Good**Escalabilidad de lecturas.   
* **bad**Complejidad alta: Requiere diseñar modelos separados.  

---

## **3. Decisión Final**  
**Elegido:** **Strategy Pattern + Event-Driven**  
Razones:  
- Alineación con la arquitectura actual: Ya se utiliza Event-Driven (Kafka) y microservicios independientes.  
- Flexibilidad: Permite empezar con un algoritmo simple (ej: Dijkstra) y migrar a uno complejo (OR-Tools) sin cambios en el código del servicio.  
- Bajo riesgo: No introduce dependencias externas críticas.  

---

## **4. Consecuencias**  
### **Positivas:**  
- **Desacoplamiento**: El servicio de Reparto no sabe qué algoritmo se utiliza.  
- **Escalabilidad**: Facilidad de cambiar y escalar los algoritmos de optimización sin impactar otros servicios.

### **Negativas:**  
- **Overhead inicial**: Se requiere una fase de diseño y adaptación para crear interfaces y adaptadores.

---

## **5. Relación con otras decisiones**  
- **Base de Datos**: PostgreSQL será utilizado como gestor SQL para todos los microservicios (Decisión 0007.1).  
---
