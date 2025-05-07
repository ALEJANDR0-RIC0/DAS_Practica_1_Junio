# Gestión de Rutas para Camiones

*Status: Acepted
*Date: 28/05/2025
* Decision-Makers: Alejandro Rico, Elena Ceinos
* Consulted: Gaizka Aranbarri, Alberto Acebes
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor
---

## Context and Problem Statement

En una empresa de logística con una flota de más de 100 camiones, los problemas operativos  (averías mecánicas, retrasos, rutas bloqueadas, etc.) generan pérdidas significativas cuando no se resuelven rápidamente.

## Drivers de decisión

*RF-04: Gestionar el reparto y las rutas de los camiones

##Considerer Options

* **0009-1-Vehicle Routing Problem (VRP)**
   - Variantes: CVRP (capacidad), VRPTW (ventanas de tiempo), DVRP (dinámico).
* **00009-2-Algoritmo de Clarke-Wright (Ahorros)**
* **00009-3-Algoritmos Genéticos**
* **00009-3-Colonia de Hormigas (ACO)**

## Pros and Cons of the Options

### 0009-1-Vehicle Routing Problem (VRP)
* **Good** Estándar en la industria, múltiples variantes (capacidad, tiempo).
* **Bad** Complejidad en implementaciones exactas.

### 0009-2-Algoritmo de Clarke-Wright (Ahorros)
* **Good** Simple y eficiente para problemas medianos.
* **Bad** No óptimo para restricciones complejas.

### 0009-3-Algoritmos Genéticos
* **Good** Bueno para problemas grandes/no lineales.
* **Bad** Requiere ajuste de hiperparámetros.

### 0009-4-Colonia de Hormigas (ACO)
* **Good** Efectivo en grafos dinámicos.
* **Bad** Costo computacional alto.

## Decision Outcome
* **Choosen Option: "0009-1-Vehicle Routing Problem (VRP)**
* Se implementará el Vehicle Routing Problem (VRP) como solución principal para la gestión de rutas de camiones, utilizando un solver especializado como Google OR-Tools para garantizar optimalidad en las rutas generadas. El VRP soportará restricciones clave como capacidad de carga (CVRP) y ventanas de tiempo (VRPTW), alineándose con los requisitos de investigación operativa especificados en RF-04.

### Positive Consequences

* Optimilidad garantizada:  El VRP proporciona rutas matemáticamente óptimas para restricciones complejas , reduciendo costos operativos.
* Escalabilidad industrial: Soporta flotas desde 10 hasta 500+ camiones usando metaheurísticas configurables
* Reducción de tiempos de desarrollo: Uso de librerías maduras  acelera la implementación en un 40-60% vs. algoritmos custom.

### Positive Consequences

*Costo computacional: En problemas muy grandes (1000+ paradas), el VRP exacto puede ser lento
* Dependencia de solvers externos: OR-Tools/Optaplanner requieren aprendizaje técnico y licencias en entornos empresariales.
* Complejidad de configuración:Ajustar parámetros demanda pruebas iterativas.
