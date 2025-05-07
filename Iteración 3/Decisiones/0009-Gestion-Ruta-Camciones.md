# Decisión de Arquitectura: RF-04 - Gestión de Rutas para Camiones

## **Requisito**
| ID     | Descripción                                                                 |
|--------|-----------------------------------------------------------------------------|
| RF-04  | La aplicación debe repartir y generar rutas para los camiones usando un algoritmo basado en técnicas de investigación operativa. |

## **Opciones de Algoritmos (Previamente Analizadas)**
1. **Vehicle Routing Problem (VRP)**
   - Variantes: CVRP (capacidad), VRPTW (ventanas de tiempo), DVRP (dinámico).
2. **Algoritmo de Clarke-Wright** (Ahorros)
3. **Algoritmos Genéticos**
4. **Búsqueda Tabú**
5. **Colonia de Hormigas (ACO)**
6. **Programación Lineal Entera (MILP)**
7. **Algoritmo del Vecino Más Cercano**
8. **Algoritmo de Barrido (Sweep)**

## **Decisión de Diseño UML (Nueva Propuesta)**
### **Objetivo**
Implementar un sistema **flexible y escalable** para gestionar rutas de camiones, permitiendo intercambiar algoritmos de ruteo sin modificar el núcleo de la aplicación.

### **Diagrama de Clases (Resumen)**
```mermaid
classDiagram
    class Camion {
        +String id
        +double capacidadMaxima
        +Ubicacion ubicacionActual
    }
    class Paquete {
        +Ubicacion destino
        +TimeWindow ventanaTiempo
    }
    class AlgoritmoRuteo {
        <<interface>>
        +generarRutas() List~Ruta~
    }
    class VRPAlgorithm {
        +generarRutas() 
    }
    class GestorRutas {
        -AlgoritmoRuteo algoritmo
        +setAlgoritmo()
    }
    AlgoritmoRuteo <|-- VRPAlgorithm
    GestorRutas --> AlgoritmoRuteo
