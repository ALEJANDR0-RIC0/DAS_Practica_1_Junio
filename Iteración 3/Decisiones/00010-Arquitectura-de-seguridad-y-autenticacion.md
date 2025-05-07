# Implementación del sistema de seguridad y autenticación
* Status: Accepted
* Date: 18/02/2025
* Decision-Makers: Alejandro Rico, Daniel Rong
* Consulted: Elena Ceinos, Gaizka Aranbarri
* Informed: Jon Mazcuñán, Alberto Acebes, Pablo Villamayor
---

## Context and Problem Statement

El sistema requiere una capa de seguridad paralela para el acceso de clientes y el sistema de pago. Es necesario definir el mecanismo de autenticación de usuario y clave con doble factor, así como la gestión centralizada de identidades y permisos.

## Drivers de decisión

* RF-09: Sistema de seguridad con doble factor de autenticación
* RD-02: Seguridad en acceso de clientes y sistema de pago

## Considered Options

* **OAuth 2.0 con OpenID Connect (OIDC)**
* **JWT con implementación propia de 2FA**
* **Servicio de autenticación externo (Auth0, Okta, etc.)**

## Pros and Cons of the Options

### OAuth 2.0 con OpenID Connect (OIDC)
* **Good** porque es un estándar ampliamente adoptado con amplio soporte y documentación.
* **Good** porque proporciona una clara separación entre autenticación y autorización.
* **Good** porque facilita la implementación de 2FA a través de proveedores de identidad.
* **Good** porque permite federación con múltiples proveedores de identidad (redes sociales, SAML, etc.).
* **Bad** porque requiere la implementación o configuración de un servidor de autorización.
* **Bad** porque añade complejidad inicial al desarrollo.

### JWT con implementación propia de 2FA
* **Good** porque ofrece control total sobre la implementación.
* **Good** porque es más ligero en términos de infraestructura (no requiere servidores adicionales).
* **Good** porque tiene menor latencia al eliminar redirects adicionales.
* **Bad** porque requiere desarrollar y mantener código de seguridad propio, con riesgo de vulnerabilidades.
* **Bad** porque aumenta la responsabilidad del equipo en cuanto a la seguridad.
* **Bad** porque es más propenso a errores de implementación en comparación con soluciones probadas.

### Servicio de autenticación externo (Auth0, Okta, etc.)
* **Good** porque proporciona una solución completa y probada sin necesidad de desarrollo.
* **Good** porque incluye funcionalidades avanzadas como MFA, social login, y análisis de seguridad.
* **Good** porque reduce la carga de mantenimiento del equipo.
* **Bad** porque introduce costos recurrentes que aumentan con el número de usuarios.
* **Bad** porque crea dependencia con proveedores externos.
* **Bad** porque puede limitar la personalización según las políticas específicas del negocio.

## Decision Outcome

* **Chosen option: "OAuth 2.0 con OpenID Connect (OIDC)"**

### Positive Consequences

* Estándar ampliamente adoptado y compatible con múltiples proveedores
* Separación clara entre autenticación y autorización
* Fácil implementación de 2FA
* Posibilidad de integración con redes sociales para login

### Negative Consequences

* Requiere implementación adicional de un servidor de autorización
* Mayor complejidad inicial en comparación con soluciones más sencillas
