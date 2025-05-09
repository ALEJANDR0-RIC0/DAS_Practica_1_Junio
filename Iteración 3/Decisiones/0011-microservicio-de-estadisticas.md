# Microservicio de Estadísticas  
* Status: Accepted  
* Date: 07/05/2025  
* Decision-Makers: Alejandro Rico, Daniel Rong  
* Consulted: Gaizka Aranbarri, Elena Ceinos
* Informed: Jon Mazcuñán, Pablo Villamayor, Alberto Acebes  

---

## Context and Problem Statement  

El sistema necesita mostrar estadísticas en tiempo real sobre:  
- Estado de pedidos (completados, en proceso, retrasados).  
- Situación de camiones (ubicación, rutas activas, incidencias).  
- Históricos para análisis (tendencias, eficiencia logística).  

**Problema:** ¿Cómo implementar esta funcionalidad manteniendo escalabilidad, bajo acoplamiento y sin impactar servicios críticos?  

---

## Drivers de Decisión  

* **RF-05:** Mostrar estadísticas a clientes y empleados.  
* **NF-01:** Baja latencia (<500ms) en consultas.  
* **NF-02:** Escalabilidad independiente de servicios base.  
* **NF-03:** Consistencia eventual aceptable (máx. 1 min de desfase).  

---

## Considered Options  

### **EST-1: Estadísticas embebidas en microservicio de Pedidos/Repartos**  
* **Good:** Minimiza duplicación de datos.  
* **Bad:** Degrada rendimiento de servicios críticos.  

### **EST-2: Microservicio independiente con base de datos analítica**  
* **Good:** Escalabilidad dedicada y tecnologías optimizadas (PostgreSQL + Redis).  
* **Bad:** Requiere sincronización vía eventos.  

### **EST-3: Solución externa (Power BI, Google Analytics)**  
* **Good:** Visualización avanzada sin desarrollo.  
* **Bad:** Coste elevado y dependencia externa.  

---

## Decision Outcome  

**Chosen option:** `EST-2 - Microservicio independiente`  
 
Alinea con la arquitectura de microservicios existente, Permite usar PostgreSQL (decisión 0007) con extensiones como `TimescaleDB` para series temporales, Integración limpia mediante eventos (Kafka/RabbitMQ). 

## Positive Outcomes  

1. **Alta escalabilidad**  
   - El servicio puede escalar independientemente de los microservicios críticos (Pedidos/Repartos).  
   - Soporta picos de consultas mediante Redis y vistas materializadas.  

2. **Experiencia de usuario mejorada**  
   - Datos en tiempo real (<1s para métricas cacheadas).  
   - Interfaz unificada para clientes y empleados.  

3. **Flexibilidad analítica**  
   - Permite añadir fácilmente nuevas KPIs (ej: "tiempo promedio de entrega por región").  
   - Soporta futuras integraciones con herramientas BI (Power BI, Tableau).  

4. **Resiliencia**  
   - Fallos en el servicio de Estadísticas no afectan a los procesos core.  
   - Recuperación rápida gracias a eventos almacenados en Kafka.  

---

## Negative Outcomes  

1. **Consistencia eventual**  
   - Los datos pueden tener un desfase de hasta 1 minuto (dependiendo de la configuración de Kafka).  

2. **Coste operacional**  
   - Requiere recursos adicionales (PostgreSQL analítico, Redis, Kafka).  
   - Complejidad en el mantenimiento de vistas materializadas.  

3. **Curva de aprendizaje**  
   - El equipo necesita formación en patrones CQRS y optimización de consultas analíticas.  

4. **Sobrecarga de eventos**  
   - Alto volumen de eventos puede saturar el sistema si no se filtra adecuadamente.  

---

# Clases Propuestas

## Capa de Consumo de Eventos
1. `EventConsumer` - Escucha y procesa eventos de Kafka

## Capa de Procesamiento
2. `StatsProcessor` - Lógica principal de cálculo de estadísticas

## Capa de Consulta
3. `StatsController` - Expone endpoints REST para consultas

## Capa de Almacenamiento
4. `StatsRepository` - Acceso a datos en PostgreSQL

## Capa de Caché
5. `CacheService` - Gestiona datos en Redis

## Modelos de Datos
6. `PedidoStats` - Modelo para estadísticas de pedidos
7. `CamionStats` - Modelo para estadísticas de camiones
8. `RepartoStats` - Modelo para estadísticas de repartos

## DTOs (Data Transfer Objects)
9. `StatsResponseDTO` - Estructura de respuesta para API
10. `TimeRangeDTO` - Para consultas por intervalos de tiempo