# 🍽️ Sistema Integral de Gestión de Restaurantes

**Versión:** 1.0.0  
**Última actualización:** Junio 2026  
**Plataforma:** Windows Forms (.NET Framework 4.7.2)  
**Lenguaje:** C#

---

## 📋 Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Objetivos del Proyecto](#objetivos-del-proyecto)
- [Características Principales](#características-principales)
- [Arquitectura del Sistema](#arquitectura-del-sistema)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Entidades del Dominio](#entidades-del-dominio)
- [Formularios de la Aplicación](#formularios-de-la-aplicación)
- [Operaciones CRUD](#operaciones-crud)
- [Flujo de Funcionamiento](#flujo-de-funcionamiento)
- [Tecnologías Utilizadas](#tecnologías-utilizadas)
- [Principios de Programación Orientada a Objetos](#principios-de-programación-orientada-a-objetos)
- [Capturas de Pantalla](#capturas-de-pantalla)
- [Requisitos del Sistema](#requisitos-del-sistema)
- [Instrucciones de Instalación y Ejecución](#instrucciones-de-instalación-y-ejecución)
- [Conclusiones Técnicas](#conclusiones-técnicas)
- [Autores y Contribuciones](#autores-y-contribuciones)

---

## 📖 Descripción General

**SistemaRestaurante** es una aplicación de escritorio desarrollada en **C# con Windows Forms** que implementa un sistema integral de gestión para operaciones de restaurantes. La aplicación se diseñó para optimizar y centralizar los procesos críticos de un establecimiento gastronómico, desde la gestión de clientes, personal, menú, reservas de mesas, generación de pedidos y procesamiento de pagos.

El sistema está basado en una **arquitectura en capas** que separa claramente la lógica de datos (Entidades), la lógica de negocio (Controlador) y la presentación (Formularios), proporcionando una estructura modular, mantenible y escalable.

### Contexto de Uso

Este sistema es idóneo para:
- Restaurantes de pequeño a mediano tamaño
- Establecimientos que requieren gestión de mesas y pedidos
- Negocios que necesitan control de inventario de platos
- Operaciones que requieren procesamiento de pagos y generación de recibos
- Organizaciones que necesitan administración de personal diversificado

---

## 🎯 Objetivos del Proyecto

1. **Centralizar la Información:** Proporcionar un único punto de acceso para todos los datos operacionales del restaurante
2. **Automatizar Procesos:** Reducir tiempos manuales mediante operaciones automáticas de cálculo y gestión
3. **Mejorar Eficiencia:** Optimizar el flujo de trabajo del personal (meseros, cocineros, administradores)
4. **Facilitar la Toma de Decisiones:** Proporcionar información estructurada sobre clientes, pedidos y transacciones
5. **Garantizar Consistencia de Datos:** Mantener la integridad informativa mediante validaciones y controles
6. **Escabilidad Futura:** Diseñar una base sólida para extensiones posteriores (integración con bases de datos, reportes avanzados, etc.)

---

## ✨ Características Principales

| # | Característica | Descripción |
|---|---|---|
| 1 | **Gestión de Clientes** | Registro, actualización, búsqueda y eliminación de clientes. Sistema de puntos de fidelidad para incentivar lealtad |
| 2 | **Administración de Empleados** | Gestión dual de dos tipos de empleados: meseros y cocineros, con cálculo de salarios dinámicos |
| 3 | **Catálogo de Platos** | Administración completa del menú: creación, edición, control de disponibilidad y gestión de stock |
| 4 | **Gestión de Mesas** | Control de disponibilidad de mesas, reservas y liberación de mesas |
| 5 | **Sistema de Pedidos** | Creación de pedidos complejos que integran cliente, mesero, mesa, plato y cantidad. Cálculo automático de subtotales e IVA |
| 6 | **Procesamiento de Pagos** | Registro de transacciones, múltiples métodos de pago, generación de recibos y auditoría de pagos |
| 7 | **Cálculos Automáticos** | Cálculo automático de IVA (15%), bonificaciones por antigüedad y experiencia, salarios netos |
| 8 | **Validación de Datos** | Validación exhaustiva de todas las entradas para garantizar integridad operacional |
| 9 | **Interfaz Intuitiva** | Diseño amigable con grillas de datos, combos, campos de entrada y botones de acción claramente identificados |
| 10 | **Búsqueda y Filtrado** | Funcionalidades de búsqueda por ID y visualización mediante DataGridView |

---

## 🏗️ Arquitectura del Sistema

### Modelo de Capas

El sistema implementa una **arquitectura en capas de tres niveles**:

```
┌─────────────────────────────────────────────┐
│          CAPA DE PRESENTACIÓN                   │
│  (Formularios Windows Forms - Interfaz Gráfica) │
├─────────────────────────────────────────────┐
│          CAPA DE LÓGICA DE NEGOCIO              │
│         (Controlador - Gestión de Datos)        │
├─────────────────────────────────────────────┐
│          CAPA DE DATOS/ENTIDADES                │
│    (Modelos de Dominio - Estructuras Base)      │
└─────────────────────────────────────────────┘
```

### Descripción de Capas

#### 1. **Capa de Presentación (Formularios)**
- Responsable de la interacción con el usuario
- Implementa formularios Windows Forms con DataGridView, TextBox, ComboBox, DateTimePicker
- Directiva: No contiene lógica de negocio, solo delegación a la capa de controlador
- Carpeta: `Formularios/`

#### 2. **Capa de Lógica de Negocio (Controlador)**
- Implementa operaciones CRUD sobre las colecciones de datos
- Gestiona reglas de negocio y validaciones
- Utiliza listas estáticas para almacenamiento en memoria
- Carpeta: `Controlador/`

#### 3. **Capa de Datos/Entidades**
- Define las estructuras de datos (clases entidad) del dominio
- Encapsula propiedades y métodos específicos de cada concepto
- Implementa relaciones entre objetos
- Carpeta: `Entidades/`

### Patrón de Diseño: Jerarquía de Herencia

```
                    ┌─────────┐
                    │ Persona │ (Abstracta)
                    └────┬────┘
                         │
            ┌────────────┬┴────────────┐
            │            │            │
        ┌───────┐    ┌─────────┐  ┌────────┐
        │Cliente│    │Empleado │  │(Otros) │
        └───────┘    └────┬────┘  └────────┘
                          │
                ┌─────────┴────────┐
                │                  │
            ┌───────┐         ┌─────────┐
            │Mesero │         │Cocinero │
            └───────┘         └─────────┘
```

---

## 📁 Estructura del Proyecto

### Árbol de Directorios

```
SistemaRestaurante/
│
├── Entidades/                      # Capa de Datos - Modelos de Dominio
│   ├── Persona.cs                  # Clase abstracta base para personas
│   ├── Cliente.cs                  # Hereda de Persona - Representa clientes
│   ├── Empleado.cs                 # Clase abstracta - Base para empleados
│   ├── Mesero.cs                   # Hereda de Empleado - Personal de servicio
│   ├── Cocinero.cs                 # Hereda de Empleado - Personal de cocina
│   ├── Mesa.cs                     # Representa mesas del restaurante
│   ├── Plato.cs                    # Representa platos del menú
│   ├── Pedido.cs                   # Representa pedidos de clientes
│   └── Pago.cs                     # Representa transacciones de pago
│
├── Controlador/                    # Capa de Lógica de Negocio - Gestión CRUD
│   ├── TLista.cs                   # Contenedor centralizado de listas
│   ├── TListaCliente.cs            # CRUD para clientes
│   ├── TListaPedido.cs             # CRUD para pedidos
│   └── TListaPlato.cs              # CRUD para platos
│
├── Formularios/                    # Capa de Presentación - Interfaz de Usuario
│   ├── frmMenu.cs                  # Formulario principal - Menú de navegación
│   ├── frmClientes.cs              # Gestión de clientes (ABM)
│   ├── frmPlatos.cs                # Gestión de platos (ABM)
│   ├── frmPedidos.cs               # Gestión de pedidos (ABM)
│   ├── frmPagos.cs                 # Procesamiento de pagos
│   ├── frmEmpleados.cs             # Visualización de empleados
│   ├── frmMesas.cs                 # Gestión de mesas (reserva/liberación)
│   └── [Designer.cs / .resx]       # Archivos de diseño generados automáticamente
│
├── Properties/                     # Propiedades del proyecto y recursos
│   ├── AssemblyInfo.cs
│   ├── Resources.resx
│   └── Settings.settings
│
├── Program.cs                      # Punto de entrada - Main()
├── App.config                      # Configuración de la aplicación
├── SistemaRestaurante.csproj       # Archivo de proyecto C#
├── SistemaRestaurante.sln          # Solución Visual Studio
└── README.md                       # Este archivo
```

### Tabla Descriptiva de Estructura de Carpetas

| Carpeta | Propósito | Contenido |
|---------|-----------|----------|
| **Entidades** | Define los modelos de negocio y estructuras de datos | Clases que representan conceptos del dominio (Persona, Cliente, Empleado, Mesero, Cocinero, Mesa, Plato, Pedido, Pago) |
| **Controlador** | Implementa la lógica CRUD y gestión de datos | Clases TLista* que manejan operaciones de creación, lectura, actualización y eliminación sobre listas en memoria |
| **Formularios** | Interfaz gráfica de usuario | Formularios Windows Forms que permiten la interacción del usuario con los datos del sistema |
| **Properties** | Configuración e información de ensamblado | Metadatos del proyecto, recursos y configuraciones |

---

## 📊 Entidades del Dominio

### 1. **Persona (Clase Abstracta Base)**

**Propósito:** Servir como clase base para todas las personas del sistema (clientes y empleados)

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `id` | `int` | Identificador único de la persona |
| `nombre` | `string` | Nombre de la persona |
| `apellido` | `string` | Apellido de la persona |
| `telefono` | `string` | Número de teléfono |
| `email` | `string` | Dirección de correo electrónico |
| `fechaNacimiento` | `DateTime` | Fecha de nacimiento |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `NombreCompleto()` | `string` | Concatena nombre y apellido |
| `Edad()` | `int` | Calcula la edad actual basada en fecha de nacimiento |
| `ObtenerRol()` | `string` | Método abstracto - Retorna el rol de la persona |
| `ObtenerInfo()` | `string` | Método abstracto - Retorna información completa |
| `ToString()` | `string` | Retorna el nombre completo |

---

### 2. **Cliente (Hereda de Persona)**

**Propósito:** Representar clientes del restaurante con sistema de puntos de fidelidad

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `idCliente` | `int` | Identificador único del cliente |
| `puntosFidelidad` | `int` | Puntos acumulados para programas de lealtad |

**Métodos Implementados:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `ObtenerRol()` | `string` | Retorna "Cliente" |
| `ObtenerInfo()` | `string` | Retorna información formateada del cliente |

---

### 3. **Empleado (Clase Abstracta - Hereda de Persona)**

**Propósito:** Servir como clase base para tipos de empleados específicos

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `idEmpleado` | `int` | Identificador único del empleado |
| `salario` | `decimal` | Salario base del empleado |
| `turno` | `string` | Turno de trabajo (Mañana, Tarde, Noche) |
| `fechaContrato` | `DateTime` | Fecha en que se contrató al empleado |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `BonoAntiguedad()` | `decimal` | Calcula bonificación si tiene 5+ años de antigüedad ($150) |
| `CalcularSalario()` | `decimal` | Método abstracto - Calcula salario total con bonificaciones |
| `ObtenerRol()` | `string` | Método abstracto |
| `ObtenerInfo()` | `string` | Método abstracto |

---

### 4. **Mesero (Hereda de Empleado)**

**Propósito:** Representar personal de servicio con capacidad de atención a mesas

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `mesasAsignadas` | `int` | Número de mesas bajo responsabilidad |
| `propinas` | `decimal` | Propinas acumuladas |

**Métodos Implementados:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `CalcularSalario()` | `decimal` | Retorna `Salario + Propinas + BonoAntiguedad()` |
| `ObtenerRol()` | `string` | Retorna "Mesero" |
| `ObtenerInfo()` | `string` | Retorna información formateada del mesero |

---

### 5. **Cocinero (Hereda de Empleado)**

**Propósito:** Representar personal de cocina con especialización

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `especialidad` | `string` | Especialidad culinaria (ej: "Comida Ecuatoriana", "Parrilla") |
| `experiencia` | `int` | Años de experiencia en cocina |

**Métodos Implementados:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `BonoExperiencia()` | `decimal` | Retorna $200 si experiencia >= 5 años, sino $50 |
| `CalcularSalario()` | `decimal` | Retorna `Salario + BonoExperiencia() + BonoAntiguedad()` |
| `ObtenerRol()` | `string` | Retorna "Cocinero" |
| `ObtenerInfo()` | `string` | Retorna información formateada del cocinero |

---

### 6. **Mesa**

**Propósito:** Representar las mesas del establecimiento y su estado de disponibilidad

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `numero` | `int` | Número identificador de la mesa |
| `capacidad` | `int` | Número máximo de personas que puede acomodar |
| `disponible` | `bool` | Estado de disponibilidad (true = libre, false = ocupada) |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `Reservar()` | `void` | Marca la mesa como disponible (true) |
| `Liberar()` | `void` | Marca la mesa como no disponible (false) |
| `ImprimirMesa()` | `string` | Retorna información formateada de la mesa |
| `ToString()` | `string` | Retorna el número de la mesa como string |

---

### 7. **Plato**

**Propósito:** Representar items del menú del restaurante con gestión de inventario

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `id` | `int` | Identificador único del plato |
| `nombre` | `string` | Nombre del plato |
| `descripcion` | `string` | Descripción de ingredientes y preparación |
| `precio` | `decimal` | Precio unitario en moneda local |
| `categoria` | `string` | Categoría del plato (Plato Fuerte, Sopa, Bebida, etc.) |
| `disponible` | `bool` | Indica si el plato está disponible para venta |
| `stock` | `int` | Cantidad disponible en inventario |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `ObtenerPrecio()` | `decimal` | Retorna el precio del plato |
| `CambiarDisponibilidad()` | `void` | Invierte el estado de disponibilidad (true ↔ false) |
| `DisminuirStock(int cantidad)` | `void` | Reduce el stock si hay suficiente cantidad disponible |
| `ImprimirPlato()` | `string` | Retorna información formateada del plato |
| `ToString()` | `string` | Retorna el nombre del plato |

---

### 8. **Pedido**

**Propósito:** Representar pedidos de clientes con composición de múltiples referencias

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `idPedido` | `int` | Identificador único del pedido |
| `cliente` | `Cliente` | Referencia al cliente que realiza el pedido |
| `mesero` | `Mesero` | Referencia al mesero que atiende |
| `mesa` | `Mesa` | Referencia a la mesa asignada |
| `plato` | `Plato` | Referencia al plato ordenado |
| `cantidad` | `int` | Cantidad de unidades del plato |
| `subtotal` | `decimal` | Monto antes de impuestos |
| `iva` | `decimal` | Impuesto al valor agregado (15%) |
| `total` | `decimal` | Monto total (subtotal + IVA) |
| `estado` | `string` | Estado del pedido (Pendiente, Preparando, Completado, Cancelado) |
| `fechaHora` | `DateTime` | Fecha y hora en que se realizó el pedido |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `CalcularTotal()` | `decimal` | Calcula IVA y Total automáticamente (IVA = Subtotal * 0.15) |
| `CambiarEstado(string nuevoEstado)` | `void` | Actualiza el estado del pedido |
| `ImprimirPedido()` | `string` | Retorna información formateada del pedido |
| `ToString()` | `string` | Retorna el ID del pedido |

---

### 9. **Pago**

**Propósito:** Representar transacciones de pago asociadas a pedidos

| Propiedad | Tipo | Descripción |
|-----------|------|-------------|
| `idPago` | `int` | Identificador único de la transacción |
| `pedido` | `Pedido` | Referencia al pedido relacionado |
| `monto` | `decimal` | Monto pagado |
| `metodoPago` | `string` | Método de pago (Efectivo, Tarjeta, Cheque, etc.) |
| `fechaPago` | `DateTime` | Fecha y hora del pago |
| `pagado` | `bool` | Indica si la transacción fue procesada exitosamente |

**Métodos Principales:**

| Método | Retorno | Descripción |
|--------|---------|-------------|
| `ProcesarPago()` | `bool` | Valida y procesa el pago (retorna true si monto > 0) |
| `GenerarRecibo()` | `string` | Genera un recibo formateado con detalles de la transacción |

---

## 🖼️ Formularios de la Aplicación

### Tabla de Formularios Implementados

| # | Formulario | Clase | Propósito | Operaciones |
|---|-----------|-------|----------|-------------|
| 1 | **Menu Principal** | `frmMenu.cs` | Punto central de navegación | Cargar datos iniciales, abrir otros formularios |
| 2 | **Gestión de Clientes** | `frmClientes.cs` | ABM de clientes | Create, Read, Update, Delete, Search |
| 3 | **Gestión de Platos** | `frmPlatos.cs` | ABM de catálogo de platos | Create, Read, Update, Delete |
| 4 | **Gestión de Pedidos** | `frmPedidos.cs` | ABM de pedidos con cálculos | Create, Read, Update, Delete, Calculate |
| 5 | **Procesamiento de Pagos** | `frmPagos.cs` | Gestión de transacciones y recibos | Create, Read, Delete, ProcessPayment, PrintReceipt |
| 6 | **Administración de Empleados** | `frmEmpleados.cs` | Visualización de personal | Read (Meseros/Cocineros), GetInfo |
| 7 | **Gestión de Mesas** | `frmMesas.cs` | Control de disponibilidad | Reserve, Release, ViewDetails |

---

## 🔄 Operaciones CRUD

El sistema implementa operaciones **CRUD (Create, Read, Update, Delete)** a través de clases controladoras genéricas:

### Patrón CRUD Genérico

```csharp
public class TListaCliente
{
    public static List<Cliente> Lista = new List<Cliente>();
    
    // CREATE
    public static void Insert(Cliente op) { ... }
    
    // READ
    public static Cliente GetCliente(int pos) { ... }
    
    // UPDATE
    public static void Update(int pos, Cliente op) { ... }
    
    // DELETE
    public static void Delete(int pos) { ... }
    
    // SEARCH
    public static int Buscar(int idCliente) { ... }
}
```

### Tablas de Operaciones CRUD por Entidad

#### **CRUD de Clientes**

| Operación | Método | Parámetros | Retorno | Validación |
|-----------|--------|-----------|---------|-----------|
| **C**reate | `Insert(Cliente op)` | objeto Cliente | void | objeto ≠ null |
| **R**ead | `GetCliente(int pos)` | posición (0-basada) | Cliente / null | pos >= 0 && pos < Count |
| **U**pdate | `Update(int pos, Cliente op)` | posición, objeto | void | pos >= 0 && objeto ≠ null |
| **D**elete | `Delete(int pos)` | posición | void | pos >= 0 |
| **S**earch | `Buscar(int idCliente)` | ID del cliente | int (índice / -1) | búsqueda lineal |

---

## 🔀 Flujo de Funcionamiento del Sistema

### Flujo General de la Aplicación

```
INICIO (Program.cs)
    ↓
Crear frmMenu
    ↓
CargarDatos() - Inicializar datos de prueba
    ↓
Usuario selecciona módulo
    ├─ Clientes
    ├─ Platos
    ├─ Pedidos
    ├─ Pagos
    ├─ Empleados
    └─ Mesas
    ↓
Formulario se abre dinámicamente
    ↓
Usuario realiza operaciones CRUD
```

### Flujo Específico: Crear Nuevo Pedido

1. Usuario selecciona datos en combos (Cliente, Mesero, Mesa, Plato)
2. Ingresa cantidad
3. Sistema calcula automáticamente: Subtotal = Precio × Cantidad
4. Sistema calcula: IVA = Subtotal × 0.15
5. Sistema calcula: Total = Subtotal + IVA
6. Usuario confirma: pedido se crea y se disminuye stock del plato
7. Pedido aparece en DataGridView

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Versión | Propósito | Categoría |
|-----------|---------|----------|----------|
| **C#** | 7.0+ | Lenguaje de programación | Backend |
| **.NET Framework** | 4.7.2 | Framework base | Plataforma |
| **Windows Forms** | - | Interfaz gráfica de usuario | Frontend |
| **DataGridView** | - | Componente de tabla de datos | UI Control |
| **ComboBox** | - | Componente de selección | UI Control |
| **TextBox** | - | Componente de entrada | UI Control |
| **DateTimePicker** | - | Componente de fechas | UI Control |
| **List<T>** | - | Colección genérica en memoria | Estructura de Datos |

---

## 🎓 Principios de Programación Orientada a Objetos

### 1. **Encapsulación**
- Campos privados con propiedades públicas
- Control de acceso a datos internos

### 2. **Herencia**
- Jerarquía de 3 niveles: Persona → Empleado/Cliente → Mesero/Cocinero
- Reutilización de código

### 3. **Polimorfismo**
- Sobrescritura de métodos abstractos (ObtenerRol, CalcularSalario, ToString)
- Comportamiento específico por tipo

### 4. **Abstracción**
- Clases abstractas Persona y Empleado
- Definición de contratos obligatorios

### 5. **Composición**
- Pedido contiene referencias a Cliente, Mesero, Mesa, Plato
- Pago contiene referencia a Pedido

### 6. **Cohesión**
- Cada clase tiene responsabilidad única y bien definida

### 7. **Acoplamiento Bajo**
- Separación clara entre capas
- Dependencias unidireccionales

---

## 📸 Capturas de Pantalla

**Sección reservada para futuras capturas de pantalla de la interfaz gráfica**

---

## 🖥️ Requisitos del Sistema

### Requisitos Mínimos

| Aspecto | Requisito |
|--------|-----------|
| **Sistema Operativo** | Windows 7 SP1 o superior |
| **Procesador** | Dual-Core 1.6 GHz o superior |
| **Memoria RAM** | 2 GB mínimo (4 GB recomendado) |
| **Espacio en Disco** | 100 MB |
| **.NET Framework** | 4.7.2 o superior |
| **Pantalla** | Resolución 1024x768 mínimo |

---

## 📥 Instrucciones de Instalación y Ejecución

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/Shotylan/SistemaRestaurante.git
cd SistemaRestaurante
```

### Paso 2: Abrir en Visual Studio

1. Abrir Visual Studio
2. File → Open → Project/Solution
3. Seleccionar `SistemaRestaurante.sln`

### Paso 3: Compilar el Proyecto

```
Build → Rebuild Solution  (Ctrl + Shift + B)
```

### Paso 4: Ejecutar la Aplicación

```
Presionar F5 o Ctrl + F5
```

### Paso 5: Navegar por la Aplicación

- Utilizar el menú principal para acceder a los diferentes módulos
- Realizar operaciones CRUD en cada formulario

---

## 🎯 Conclusiones Técnicas

### Logros del Proyecto

✅ Arquitectura modular en capas  
✅ Implementación completa de OOP  
✅ CRUD funcional para todas las entidades  
✅ Interfaz intuitiva con Windows Forms  
✅ Validaciones exhaustivas de datos  
✅ Cálculos automáticos de IVA y bonificaciones  

### Limitaciones Actuales

- Almacenamiento volátil (sin persistencia en BD)
- Datos se pierden al cerrar la aplicación
- No hay autenticación de usuarios
- Búsqueda lineal O(n)

### Mejoras Futuras Propuestas

- [ ] Integración con Base de Datos (SQL Server)
- [ ] Sistema de autenticación y roles
- [ ] Generación de reportes en PDF/Excel
- [ ] Aplicación móvil complementaria
- [ ] Dashboard con análisis avanzado
- [ ] API REST para terceros

---

## 👥 Autores y Contribuciones

**Desarrollador Principal:** [@Shotylan](https://github.com/Shotylan)

Se aceptan contribuciones mediante pull requests.

---

**Última actualización:** Junio 2026  
**Estado:** ✅ Funcional - Versión 1.0.0

---

¡Gracias por usar SistemaRestaurante! 🙏

## Pipeline CI activo con GitHub Actions
