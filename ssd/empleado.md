# Entidad Empleado - Sistema de Gestión de Restaurante

## 1. Propósito

La entidad **Empleado** es una clase abstracta que actúa como clase base para representar el personal del restaurante. Sirve como plantilla que define los atributos y comportamientos comunes a todos los tipos de empleados (Meseros, Cocineros, etc.), permitiendo la implementación de cálculos de salario específicos y la obtención de información detallada según el rol.

---

## 2. Estructura de Herencia

```
Persona (Clase Abstracta)
  ↓
Empleado (Clase Abstracta)
  ├─ Mesero (Clase Concreta)
  └─ Cocinero (Clase Concreta)
```

### Relación con Persona

La clase **Empleado** hereda de **Persona** y extiende sus atributos con información específica del empleo:

| Atributo Heredado (Persona) | Tipo | Descripción |
|---|---|---|
| `id` | `int` | Identificador único de la persona |
| `nombre` | `string` | Nombre del empleado |
| `apellido` | `string` | Apellido del empleado |
| `telefono` | `string` | Teléfono de contacto |
| `email` | `string` | Correo electrónico |
| `fechaNacimiento` | `DateTime` | Fecha de nacimiento (permite calcular edad) |

---

## 3. Atributos Propios de Empleado

| Atributo | Tipo | Descripción | Acceso |
|---|---|---|---|
| `idEmpleado` | `int` | Identificador único del empleado (diferente del id de Persona) | Público (Get/Set) |
| `salario` | `decimal` | Salario base mensual del empleado | Público (Get/Set) |
| `turno` | `string` | Turno de trabajo (Mañana, Tarde, Noche) | Público (Get/Set) |
| `fechaContrato` | `DateTime` | Fecha en que se contrató al empleado | Público (Get/Set) |

---

## 4. Métodos Implementados

### 4.1 Constructores

#### Constructor Vacío
```csharp
public Empleado()
```
- Inicializa una instancia vacía de Empleado
- Utilizado para inicializaciones genéricas

#### Constructor Parametrizado
```csharp
public Empleado(int id, string nombre, string apellido,
                 string telefono, string email,
                 DateTime fechaNacimiento,
                 int idEmpleado,
                 decimal salario,
                 string turno,
                 DateTime fechaContrato)
```
- Inicializa un Empleado con todos sus datos
- Invoca al constructor padre de Persona
- Parámetros:
  - Primeros 6: Heredados de Persona (id, nombre, apellido, teléfono, email, fechaNacimiento)
  - Últimos 4: Específicos de Empleado (idEmpleado, salario, turno, fechaContrato)

### 4.2 Métodos de Cálculo

#### BonoAntiguedad()
```csharp
public decimal BonoAntiguedad()
```
- **Retorno**: `decimal`
- **Descripción**: Calcula una bonificación basada en la antigüedad en la empresa
- **Lógica**:
  - Obtiene los años de antigüedad: `DateTime.Now.Year - FechaContrato.Year`
  - Si antigüedad >= 5 años: retorna **$150.00**
  - Si antigüedad < 5 años: retorna **$0.00**
- **Propósito**: Recompensa la lealtad y continuidad de empleados

#### CalcularSalario() [ABSTRACTO]
```csharp
public abstract decimal CalcularSalario()
```
- **Retorno**: `decimal`
- **Descripción**: Método abstracto que debe ser implementado por cada tipo de empleado
- **Propósito**: Permitir que cada especialización (Mesero, Cocinero) calcule su salario total de manera diferente
- **Implementaciones**:
  - **Mesero**: Retorna `Salario + Propinas + BonoAntiguedad()`
  - **Cocinero**: Retorna `Salario + BonoExperiencia() + BonoAntiguedad()`

### 4.3 Métodos Abstractos Heredados

#### ObtenerRol() [ABSTRACTO]
```csharp
public abstract override string ObtenerRol()
```
- **Retorno**: `string`
- **Descripción**: Retorna el rol/tipo del empleado
- **Implementaciones**:
  - **Mesero**: Retorna `"Mesero"`
  - **Cocinero**: Retorna `"Cocinero"`

#### ObtenerInfo() [ABSTRACTO]
```csharp
public abstract override string ObtenerInfo()
```
- **Retorno**: `string`
- **Descripción**: Retorna información formateada del empleado
- **Implementaciones**:
  - **Mesero**: Muestra nombre, turno, mesas asignadas, propinas y salario total
  - **Cocinero**: Muestra nombre, especialidad, años de experiencia, turno y salario total

---

## 5. Métodos Heredados de Persona

| Método | Retorno | Descripción |
|---|---|---|
| `NombreCompleto()` | `string` | Retorna nombre + apellido |
| `Edad()` | `int` | Calcula y retorna la edad actual del empleado |
| `ToString()` | `string` | Retorna el nombre completo del empleado |

---

## 6. Subclases Específicas

### 6.1 Mesero

**Propósito**: Representar al personal de servicio encargado de atender a los clientes en las mesas.

**Atributos Adicionales**:
- `mesasAsignadas` (int): Número de mesas bajo su responsabilidad
- `propinas` (decimal): Total de propinas acumuladas

**Método Específico**:
- `CalcularSalario()`: `Salario + Propinas + BonoAntiguedad()`

**Ejemplo de Inicialización**:
```csharp
new Mesero(
    1, "Pedro", "Ruiz", "0996666666", "pedro@gmail.com", 
    new DateTime(1994, 3, 12), 201, 800m, "Mañana", 
    new DateTime(2021, 5, 10), 5, 120m
)
```

### 6.2 Cocinero

**Propósito**: Representar al personal de cocina especializado en la preparación de alimentos.

**Atributos Adicionales**:
- `especialidad` (string): Especialidad culinaria (ej: "Comida Ecuatoriana", "Parrilla")
- `experiencia` (int): Años de experiencia en cocina

**Métodos Específicos**:
- `BonoExperiencia()`: Retorna $200 si experiencia >= 5 años, sino $50
- `CalcularSalario()`: `Salario + BonoExperiencia() + BonoAntiguedad()`

**Ejemplo de Inicialización**:
```csharp
new Cocinero(
    3, "Ana", "Vera", "0998888888", "ana@gmail.com", 
    new DateTime(1988, 4, 15), 301, 1200m, "Mañana", 
    new DateTime(2018, 2, 10), "Comida Ecuatoriana", 8
)
```

---

## 7. Operaciones CRUD

### 7.1 Create (Crear)

**Ubicación**: `Formularios/frmMenu.cs` - Método `CargarDatos()`

Los empleados se instancian y se agregan a las listas estáticas:

```csharp
// MESEROS
TLista.ListaMeseros.Add(new Mesero(...));

// COCINEROS
TLista.ListaCocineros.Add(new Cocinero(...));
```

**Almacenamiento**: 
- Los datos se almacenan en memoria mediante las listas estáticas de `TLista`:
  - `TLista.ListaMeseros` (tipo `List<Mesero>`)
  - `TLista.ListaCocineros` (tipo `List<Cocinero>`)

### 7.2 Read (Leer)

**Ubicación**: `Formularios/frmEmpleados.cs`

**Métodos de Lectura**:

1. **ListarMeseros()**
   - Recupera todos los meseros de `TLista.ListaMeseros`
   - Muestra los datos en un `DataGridView`

2. **ListarCocineros()**
   - Recupera todos los cocineros de `TLista.ListaCocineros`
   - Muestra los datos en un `DataGridView`

3. **ListarTodos()**
   - Combina meseros y cocineros en una sola lista
   - Utiliza LINQ: `Concat()` para unir las colecciones

**Acceso a Información Detallada**:
- Seleccionar un empleado en el grid
- Hacer clic en "Ver información"
- Se muestra un `MessageBox` con `ObtenerInfo()`

### 7.3 Update (Actualizar)

**Ubicación**: No implementado en el código actual

**Nota**: El sistema actual no incluye funcionalidad de actualización de empleados. Para implementarla se requeriría:
- Agregar un método en `frmEmpleados` que permita editar propiedades
- Modificar el objeto en la lista correspondiente
- Refrescar el `DataGridView`

### 7.4 Delete (Eliminar)

**Ubicación**: No implementado en el código actual

**Nota**: El sistema actual no incluye funcionalidad de eliminación de empleados. Para implementarla se requeriría:
- Agregar un botón "Eliminar" en `frmEmpleados`
- Usar `TLista.ListaMeseros.Remove()` o `TLista.ListaCocineros.Remove()`
- Refrescar el `DataGridView`

---

## 8. Formularios Relacionados

### 8.1 frmEmpleados

**Archivo**: `Formularios/frmEmpleados.cs`

**Propósito**: Interfaz para visualizar y gestionar empleados.

**Componentes**:
- **ComboBox**: Selecciona tipo de empleado a mostrar (Mesero/Cocinero)
- **DataGridView**: Muestra lista de empleados con sus propiedades
- **Botón "Ver información"**: Muestra detalles del empleado seleccionado

**Funcionalidades**:

| Método | Descripción |
|---|---|
| `frmEmpleados_Load()` | Inicializa el combo box con tipos de empleados |
| `comboBox1_SelectedIndexChanged()` | Actualiza el grid según el tipo seleccionado |
| `button1_Click()` | Muestra información detallada del empleado seleccionado |
| `ListarMeseros()` | Carga meseros en el DataGridView |
| `ListarCocineros()` | Carga cocineros en el DataGridView |
| `ListarTodos()` | Carga todos los empleados en el DataGridView |

**Acceso**: Desde el menú principal `frmMenu` → Menú "Empleados"

---

## 9. Flujo de Funcionamiento en el Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                    SISTEMA RESTAURANTE                      │
└─────────────────────────────────────────────────────────────┘
                              ↓
                    ┌─────────────────┐
                    │   frmMenu       │ (Formulario Principal)
                    └────────┬────────┘
                             ↓
                   Menú: "Empleados" ← Click
                             ↓
                    ┌─────────────────┐
                    │ frmEmpleados    │ (Gestión de Empleados)
                    └────────┬────────┘
                             ↓
        ┌────────────────────┼────────────────────┐
        ↓                    ↓                    ↓
   ComboBox         DataGridView          Botón Ver Info
   (Mesero/         (Lista de           (Mostrar Detalles)
    Cocinero)       Empleados)                  ↓
        ↓                    ↓            MessageBox con
   Selecciona       Muestra propiedades   ObtenerInfo()
   Tipo             (Id, Nombre, Turno,
        ↓           Salario, etc.)
   Filtra lista                 ↓
   desde                    Seleccionar
   TLista                   Empleado
        ↓                        ↓
  ListaMeseros         button1_Click()
  o                         ↓
  ListaCocineros   Validar tipo
                   (Mesero/Cocinero)
                        ↓
                   Ejecutar
                   ObtenerInfo()
```

### 9.1 Carga Inicial de Datos

1. **Inicio del Sistema** (`frmMenu.Load`)
   - Se ejecuta `CargarDatos()`
   - Se crean instancias de Mesero y Cocinero
   - Se agregan a `TLista.ListaMeseros` y `TLista.ListaCocineros`

### 9.2 Visualización de Empleados

1. **Usuario abre frmEmpleados** desde el menú
2. **Se inicializa el ComboBox** con opciones "Mesero" y "Cocinero"
3. **Se selecciona un tipo** en el ComboBox
4. **Se filtra la lista** correspondiente
5. **DataGridView muestra** los empleados seleccionados

### 9.3 Visualización de Detalles

1. **Usuario selecciona** un empleado en el grid
2. **Hace clic en "Ver información"**
3. **Se valida el tipo** del objeto (Mesero o Cocinero)
4. **Se ejecuta `ObtenerInfo()`** del tipo específico
5. **Se muestra un MessageBox** con información formateada

---

## 10. Ejemplo de Datos

### Mesero Ejemplo

```
Nombre: Pedro Ruiz
ID Empleado: 201
Salario Base: $800.00
Turno: Mañana
Mesas Asignadas: 5
Propinas: $120.00
Fecha Contrato: 2021-05-10
Antigüedad: 3 años

Cálculo de Salario Total:
- Salario Base: $800.00
- Propinas: $120.00
- Bono Antigüedad: $0.00 (menos de 5 años)
- TOTAL: $920.00
```

### Cocinero Ejemplo

```
Nombre: Ana Vera
ID Empleado: 301
Salario Base: $1,200.00
Turno: Mañana
Especialidad: Comida Ecuatoriana
Experiencia: 8 años
Fecha Contrato: 2018-02-10
Antigüedad: 8 años

Cálculo de Salario Total:
- Salario Base: $1,200.00
- Bono Experiencia: $200.00 (8 años >= 5 años)
- Bono Antigüedad: $150.00 (8 años >= 5 años)
- TOTAL: $1,550.00
```

---

## 11. Consideraciones de Diseño

### 11.1 Patrón de Herencia

La clase **Empleado** utiliza el patrón **Template Method** mediante métodos abstractos, permitiendo que cada subtipo implemente su propia lógica de cálculo de salario.

### 11.2 Almacenamiento en Memoria

Los datos se almacenan en listas estáticas (`TLista`), por lo que:
- **Persisten** mientras la aplicación está en ejecución
- **Se pierden** al cerrar la aplicación (sin persistencia en BD)
- **Todos los formularios** acceden a los mismos datos

### 11.3 Validación

El sistema actual no incluye validación de datos de entrada. Las operaciones asumen que:
- Los valores numéricos son válidos
- Las fechas son coherentes
- Los strings no son null

---

## 12. Conclusión

La entidad **Empleado** es el núcleo de la gestión de personal en el sistema. Su estructura jerárquica permite manejar diferentes tipos de empleados con comportamientos específicos, mientras mantiene una interfaz común a través de métodos abstractos. El sistema actual proporciona funcionalidad básica de lectura y visualización, pero está preparado para futuras extensiones en actualización y eliminación de registros.
