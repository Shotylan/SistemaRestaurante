# Entidad Pedido

## 📋 Propósito

La entidad **Pedido** representa los pedidos que realizan los clientes en el restaurante. Actúa como un nodo central que vincula múltiples referencias: clientes, meseros, mesas y platos. Su propósito principal es registrar y gestionar la composición de cada orden con su información de facturación y estado.

---

## 🏗️ Estructura y Atributos

### Atributos Privados

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `idPedido` | `int` | Identificador único del pedido |
| `cliente` | `Cliente` | Referencia al cliente que realiza el pedido |
| `mesero` | `Mesero` | Referencia al mesero que atiende el pedido |
| `mesa` | `Mesa` | Referencia a la mesa donde se sirve |
| `plato` | `Plato` | Referencia al plato ordenado |
| `cantidad` | `int` | Cantidad de unidades del plato ordenado |
| `subtotal` | `decimal` | Monto base del pedido (antes de impuestos) |
| `iva` | `decimal` | Impuesto al Valor Agregado calculado al 15% del subtotal |
| `total` | `decimal` | Monto total (subtotal + IVA) |
| `estado` | `string` | Estado actual del pedido: Pendiente, Preparando, Completado, Cancelado |
| `fechaHora` | `DateTime` | Fecha y hora en que se realizó el pedido |

### Propiedades Públicas (Get/Set)

```csharp
public int IdPedido { get; set; }
public Cliente Cliente { get; set; }
public Mesero Mesero { get; set; }
public Mesa Mesa { get; set; }
public Plato Plato { get; set; }
public int Cantidad { get; set; }
public decimal Subtotal { get; set; }
public decimal Iva { get; set; }
public decimal Total { get; set; }
public string Estado { get; set; }
public DateTime FechaHora { get; set; }
```

---

## 🔨 Constructores

### Constructor Sin Parámetros
```csharp
public Pedido() { }
```
Constructor vacío que permite crear instancias vacías de la clase.

### Constructor Parametrizado
```csharp
public Pedido(int idPedido,
              Cliente cliente,
              Mesero mesero,
              Mesa mesa,
              Plato plato,
              int cantidad,
              decimal subtotal,
              decimal iva,
              decimal total,
              string estado,
              DateTime fechaHora)
```
Constructor que inicializa todos los atributos de la instancia con los valores proporcionados.

---

## ⚙️ Métodos de Instancia

### `CalcularTotal()`
```csharp
public decimal CalcularTotal()
```
**Descripción:** Calcula automáticamente el IVA y el total del pedido.

**Lógica:**
- IVA = Subtotal × 0.15 (15%)
- Total = Subtotal + IVA

**Retorna:** El valor decimal del total calculado.

**Uso:** Se invoca cuando se está creando o modificando un pedido en el formulario.

---

### `CambiarEstado(string nuevoEstado)`
```csharp
public void CambiarEstado(string nuevoEstado)
```
**Descripción:** Actualiza el estado del pedido a un nuevo estado proporcionado.

**Parámetros:**
- `nuevoEstado` (string): El nuevo estado del pedido

**Estados válidos:** Pendiente, Preparando, Completado, Cancelado

**Retorna:** void

---

### `ImprimirPedido()`
```csharp
public string ImprimirPedido()
```
**Descripción:** Genera una representación formateada y legible del pedido completo.

**Retorna:** Un string con el siguiente formato:
```
PEDIDO
Código Pedido: [IdPedido]
Cliente: [Nombre Completo del Cliente]
Mesero: [Nombre Completo del Mesero]
Mesa: [Número de Mesa]
Subtotal: $[Subtotal]
IVA: $[IVA]
Total: $[Total]
Estado: [Estado]
```

**Uso:** Se utiliza para mostrar información del pedido en reportes o pantallas de detalle.

---

### `ToString()`
```csharp
public override string ToString()
```
**Descripción:** Retorna una representación simplificada del pedido.

**Retorna:** El ID del pedido como string.

**Uso:** Se utiliza para mostrar el pedido en listas (DataGridView, ComboBox, etc.).

---

## 📊 Operaciones CRUD

Las operaciones CRUD para la entidad Pedido se gestionan a través de la clase controladora `TListaPedido`, que mantiene una lista estática de pedidos en memoria.

### **Create (Crear)**

**Método:** `TListaPedido.Insert(Pedido op)`

```csharp
public static void Insert(Pedido op)
{
    if (op != null)
        Lista.Add(op);
    else
        MessageBox.Show("Objeto null");
}
```

**Proceso:**
1. Se valida que el objeto no sea null
2. Se agrega el pedido a la lista estática `Lista`
3. Si es null, muestra un mensaje de error

**Validaciones en el formulario (frmPedidos):**
- ID de Pedido debe estar completo
- Cliente debe estar seleccionado
- Mesero debe estar seleccionado
- Mesa debe estar seleccionada
- Plato debe estar seleccionado
- Cantidad debe estar completa
- Estado debe estar seleccionado

**Efectos secundarios:**
- Reduce el stock del plato: `p.Plato.DisminuirStock(p.Cantidad)`

---

### **Read (Leer)**

**Método 1:** `TListaPedido.GetPedido(int pos)`

```csharp
public static Pedido GetPedido(int pos)
{
    if (pos >= 0 && pos < Lista.Count)
        return Lista[pos];
    else
        return null;
}
```

Retorna un pedido en una posición específica de la lista.

**Método 2:** `TListaPedido.Buscar(int idPedido)`

```csharp
public static int Buscar(int idPedido)
{
    for (int i = 0; i < Lista.Count; i++)
    {
        if (Lista[i].IdPedido == idPedido)
            return i;
    }
    return -1;
}
```

Busca un pedido por su ID y retorna su posición en la lista (o -1 si no existe).

---

### **Update (Actualizar)**

**Método:** `TListaPedido.Update(int pos, Pedido op)`

```csharp
public static void Update(int pos, Pedido op)
{
    if (pos >= 0 && op != null)
        Lista[pos] = op;
    else
        MessageBox.Show("Posición negativa o objeto null");
}
```

**Proceso:**
1. Valida que la posición sea válida y el objeto no sea null
2. Reemplaza el pedido en la posición indicada
3. Si hay error, muestra un mensaje

**Uso en formulario:** Se invoca desde el botón "Actualizar" en frmPedidos después de modificar los campos.

---

### **Delete (Eliminar)**

**Método:** `TListaPedido.Delete(int pos)`

```csharp
public static void Delete(int pos)
{
    if (pos >= 0)
        Lista.RemoveAt(pos);
    else
        MessageBox.Show("Posición negativa");
}
```

**Proceso:**
1. Valida que la posición sea válida
2. Elimina el pedido en esa posición de la lista
3. Si la posición es negativa, muestra un mensaje de error

**Uso en formulario:** Se invoca desde el botón "Eliminar" en frmPedidos.

---

## 📝 Formularios Relacionados

### **frmPedidos.cs** - Gestión de Pedidos

**Propósito:** Formulario principal para crear, actualizar, leer y eliminar pedidos.

**Componentes UI:**
- **textBox1:** ID del Pedido
- **comboBox1:** Seleccionar Cliente (cargado desde TListaCliente.Lista)
- **comboBox2:** Seleccionar Mesero (cargado desde TLista.ListaMeseros)
- **comboBox3:** Seleccionar Mesa (cargado desde TLista.ListaMesas)
- **comboBox4:** Seleccionar Plato (cargado desde TListaPlato.Lista)
- **textBox2:** Cantidad de unidades
- **textBox3:** Subtotal (calculado automáticamente)
- **textBox4:** IVA (calculado automáticamente)
- **textBox5:** Total (calculado automáticamente)
- **comboBox5:** Estado del Pedido (Pendiente, Preparando, Completado, Cancelado)
- **dateTimePicker1:** Fecha y hora del pedido
- **dataGridView1:** Listado de todos los pedidos registrados

**Métodos Principales:**

| Método | Descripción |
|--------|-------------|
| `CargarCombos()` | Carga las listas de clientes, meseros, mesas y platos en los ComboBox |
| `Listar()` | Muestra todos los pedidos en el DataGridView |
| `Calcular()` | Calcula subtotal, IVA y total basado en el plato seleccionado y cantidad |
| `CrearObjeto()` | Construye una instancia de Pedido con los datos del formulario |
| `Validar()` | Verifica que todos los campos estén completos |
| `Limpiar()` | Vacía todos los campos del formulario |

**Botones y Acciones:**

| Botón | Acción | Flujo |
|-------|--------|-------|
| **Agregar (button1)** | Crear nuevo pedido | Valida → Crea objeto → Reduce stock → Inserta en lista → Refresca vista |
| **Actualizar (button2)** | Editar pedido existente | Selecciona fila → Actualiza en lista → Refresca vista |
| **Eliminar (button3)** | Borrar pedido | Selecciona fila → Elimina de lista → Refresca vista |
| **Limpiar (button4)** | Limpiar formulario | Vacía todos los campos |

**Eventos:**
- `frmPedidos_Load()`: Carga datos iniciales
- `button1_Click()`: Crear pedido
- `button2_Click()`: Actualizar pedido
- `button3_Click()`: Eliminar pedido
- `button4_Click()`: Limpiar campos
- `comboBox4_SelectedIndexChanged()`: Recalcula valores cuando cambia el plato

---

### **frmPagos.cs** - Gestión de Pagos (Relacionado)

**Propósito:** Formulario para procesar pagos asociados a pedidos.

**Referencia a Pedido:**
- **comboBox1:** Combobox que carga los pedidos desde `TListaPedido.Lista`
- Muestra el ID del pedido como DisplayMember

**Integración:**
```csharp
public void CargarCombos()
{
    comboBox1.DataSource = null;
    comboBox1.DataSource = TListaPedido.Lista;
    comboBox1.DisplayMember = "IdPedido";
}
```

**Funcionalidad especial:**
- Cuando se selecciona un pedido, el campo de monto se llena automáticamente con el Total del pedido:

```csharp
private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
{
    if (comboBox1.SelectedItem != null)
    {
        Pedido p = (Pedido)comboBox1.SelectedItem;
        textBox2.Text = p.Total.ToString();
    }
}
```

---

## 🔄 Flujo de Funcionamiento en el Sistema

### Ciclo de vida de un Pedido:

1. **Creación del Pedido** (frmPedidos)
   - Usuario selecciona cliente, mesero, mesa y plato
   - Sistema calcula subtotal, IVA y total
   - Usuario especifica cantidad y estado
   - Se crea la instancia de Pedido
   - Se reduce el stock del plato: `Plato.DisminuirStock(cantidad)`
   - Se inserta en `TListaPedido.Lista`

2. **Visualización del Pedido**
   - Aparece en el DataGridView de frmPedidos
   - El método `ToString()` muestra solo el ID en ComboBox
   - El método `ImprimirPedido()` genera detalles completos

3. **Modificación del Pedido**
   - Usuario selecciona un pedido del DataGridView
   - Modifica los campos deseados
   - Sistema recalcula montos si es necesario
   - Se actualiza con `TListaPedido.Update()`

4. **Procesamiento de Pago**
   - Usuario accede a frmPagos
   - Selecciona un pedido del ComboBox (cargado desde `TListaPedido.Lista`)
   - El Total del pedido se muestra automáticamente
   - Se crea un objeto Pago vinculado al Pedido
   - El pago se procesa y se registra

5. **Eliminación del Pedido**
   - Usuario selecciona un pedido del DataGridView
   - Presiona botón Eliminar
   - Se invoca `TListaPedido.Delete(posición)`

---

## 📦 Relaciones con Otras Entidades

```
Pedido
  ├── Cliente (relación 1:N)
  │   └── Contiene referencia a Cliente
  ├── Mesero (relación 1:N)
  │   └── Contiene referencia a Mesero (tipo Empleado)
  ├── Mesa (relación 1:N)
  │   └── Contiene referencia a Mesa
  ├── Plato (relación 1:N)
  │   └── Contiene referencia a Plato
  └── Pago (relación 1:N)
      └── Pago referencia a Pedido
```

**Dependencias:**
- Un Pedido requiere un Cliente válido
- Un Pedido requiere un Mesero válido
- Un Pedido requiere una Mesa válida
- Un Pedido requiere un Plato válido
- Al crear un Pedido, reduce el stock del Plato
- Un Pago siempre se vincula a un Pedido existente

---

## 🎯 Ejemplos de Uso

### Crear un Pedido
```csharp
Pedido pedido = new Pedido(
    1,
    cliente,
    mesero,
    mesa,
    plato,
    2,
    20m,
    3m,
    23m,
    "Pendiente",
    DateTime.Now
);

// Calcular totales
pedido.CalcularTotal();

// Insertar en la lista
TListaPedido.Insert(pedido);
```

### Cambiar Estado
```csharp
Pedido pedido = TListaPedido.GetPedido(0);
pedido.CambiarEstado("Preparando");
```

### Buscar Pedido
```csharp
int posicion = TListaPedido.Buscar(1); // Busca pedido con ID = 1
if (posicion >= 0)
{
    Pedido pedido = TListaPedido.GetPedido(posicion);
}
```

### Imprimir Detalles
```csharp
Pedido pedido = TListaPedido.GetPedido(0);
string detalles = pedido.ImprimirPedido();
MessageBox.Show(detalles);
```

---

## 📌 Notas Importantes

1. **Cálculo de IVA**: El sistema usa un IVA fijo del 15% sobre el subtotal
2. **Stock de Platos**: Al crear un pedido, el stock del plato se reduce automáticamente
3. **Almacenamiento**: Los pedidos se almacenan en memoria (lista estática), no en base de datos
4. **Estados válidos**: Pendiente, Preparando, Completado, Cancelado
5. **Vínculo con Pagos**: Cada Pago debe estar asociado a un Pedido existente
6. **Identificación**: El ToString() retorna solo el ID, utilizado en interfaces de selección
