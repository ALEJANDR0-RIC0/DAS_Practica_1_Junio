# Decisión sobre las clases principales a añadir
* Status: Accepted
* Date: 26/03/2025
* Decision-Makers: Elena Ceinos, Alejandro Rico
* Consulted: Gaizka Aranbarri, Alberto Acebes
* Informed: Jon Mazcuñán, Daniel Rong, Pablo Villamayor

---

## Drivers de Decisión

- El modelo de alto nivel define se divide en tres paquetes de Cliente, Negocio y Datos.
- Es necesario concretar las clases principales que estructurarán el sistema de acuerdo al diseño modular presentado.

---

## Context and Problem Statement

El diseño de la arquitectura presenta una organización en tres capas (Cliente, Negocio, Datos) con conexiones definidas mediante relaciones. Este modelo modular debe traducirse en clases que sirvan como eje de desarrollo de los microservicios correspondientes.

---

## Considered Options

Clases que se valoran para formar parte del sistema (algunas ya aparecen en el UML, otras pueden añadirse en fases posteriores):

- Cliente: `Cliente`, `clienteApp`
- Pedidos: `Pedido`, `Producto`
- Pagos: `Pago`, `Transaccion`
- Reparto: `Ruta`, `Camion`, `Incidencia`
- Seguridad: `Usuario`, `Credencial`, `SecurityManager`
- Estadísticas: `RegistroEstadistico`
- Notificaciones: `Notificacion`
- Datos: `RepositorioX`, `Configuracion`
- API Gateway: `apiGateway`
- Otros futuros: `DTOs`, `Mapper`, `ServicioCorreo`, `Logs`

---

## Decision Outcome

**Opción elegida**: Definir en esta iteración las siguientes clases extraídas directamente del modelo UML, incluyendo su justificación:

###  Cliente
- `clienteApp`: representa la aplicación del cliente (PC/móvil), encargada de gestionar la interacción del usuario final con el sistema.

###  Negocio
- `Seguridad`: controla el acceso, autenticación y autorización, incluyendo doble factor.
- `Cliente`: maneja la lógica relacionada con los datos personales y el perfil del usuario.
- `Pedidos`: gestiona la creación, modificación y estado de los pedidos.
- `Reparto`: se encarga de la asignación de rutas y camiones para realizar entregas.
- `Pagos`: centraliza la interacción con Stripe, estados del pago y validaciones.
- `Estadísticas`: proporciona datos en tiempo real o diferido sobre pedidos, entregas y uso.
- `Notificaciones`: gestiona el sistema de avisos y noticias suscribibles por los clientes.

###  Datos
- `Configuracion`: clase que gestiona la configuración general del sistema (parámetros globales, variables de entorno).
- `Repos`: clase contenedora para los distintos repositorios de acceso a datos de cada microservicio.

###  API Gateway
- `apiGateway`: punto de entrada único al sistema, encargado de redirigir peticiones a los servicios correspondientes según la ruta y autenticación.

###  Capa de seguridad
- `SecurityManager`: aplica políticas de seguridad transversales entre el gateway y los microservicios críticos.

---

## Consecuencias

### Positivas

- Claridad en la organización del sistema basada en la vista modular.
- Fomenta una estructura escalable y alineada con microservicios.
- Facilita la asignación de responsabilidades por equipo según subsistemas.

### Negativas

- Algunas clases aún son abstractas y requerirán refinamiento en la implementación.
- El modelo aún no detalla relaciones internas entre clases (atributos y métodos), lo cual se desarrollará en siguientes iteraciones.

---

