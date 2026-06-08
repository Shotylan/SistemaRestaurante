# 🍽️ SistemaRestaurante

Un sistema integral de gestión para restaurantes desarrollado en **C#**, diseñado para optimizar operaciones como la gestión de pedidos, mesas, inventario y reportes.

## 📋 Tabla de Contenidos

- [Características](#características)
- [Requisitos Previos](#requisitos-previos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Tecnologías](#tecnologías)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

## ✨ Características

- **Gestión de Mesas**: Control de disponibilidad y reservas de mesas
- **Sistema de Pedidos**: Registro y seguimiento de pedidos de clientes
- **Gestión de Menú**: Administración de platos, precios y disponibilidad
- **Control de Inventario**: Seguimiento de ingredientes y stock
- **Reportes y Estadísticas**: Análisis de ventas y datos del restaurante
- **Interfaz Intuitiva**: Diseño amigable y fácil de usar

## 🔧 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:

- [.NET Framework](https://dotnet.microsoft.com/download) (versión 6.0 o superior)
- [Visual Studio](https://visualstudio.microsoft.com/es/downloads/) o [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server](https://www.microsoft.com/es-es/sql-server) (si aplica)

## 📦 Instalación

1. **Clona el repositorio**
   ```bash
   git clone https://github.com/Shotylan/SistemaRestaurante.git
   cd SistemaRestaurante
   ```

2. **Restaura las dependencias**
   ```bash
   dotnet restore
   ```

3. **Configura la base de datos** (si es necesario)
   - Actualiza la cadena de conexión en `appsettings.json`
   ```bash
   dotnet ef database update
   ```

4. **Compila el proyecto**
   ```bash
   dotnet build
   ```

5. **Ejecuta la aplicación**
   ```bash
   dotnet run
   ```

## 🚀 Uso

### Ejecutar el Proyecto

```bash
dotnet run
```

La aplicación se abrirá en tu navegador por defecto o accede a `https://localhost:5001`

### Opciones Principales

- **Gestionar Mesas**: Asigna clientes a mesas disponibles
- **Crear Pedidos**: Registra nuevos pedidos desde el punto de venta
- **Consultar Inventario**: Verifica disponibilidad de ingredientes
- **Ver Reportes**: Analiza ventas y datos del restaurante

## 📁 Estructura del Proyecto

```
SistemaRestaurante/
├── Models/                 # Modelos de datos
├── Controllers/           # Controladores (lógica de negocio)
├── Views/                # Vistas (interfaz de usuario)
├── Services/             # Servicios
├── Data/                 # Contexto de base de datos
├── Migrations/           # Migraciones de base de datos
├── wwwroot/              # Archivos estáticos
├── appsettings.json      # Configuración de la aplicación
└── Program.cs            # Punto de entrada
```

## 🛠️ Tecnologías

- **Lenguaje**: C#
- **Framework**: .NET Core / ASP.NET Core
- **Base de Datos**: SQL Server (o según configuración)
- **ORM**: Entity Framework Core
- **Frontend**: HTML, CSS, JavaScript (Razor Views)

## 🤝 Contribuciones

¡Las contribuciones son bienvenidas! Si deseas mejorar este proyecto:

1. Haz un fork del repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-caracteristica`)
3. Realiza tus cambios y commit (`git commit -m 'Agrega nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está disponible sin licencia especificada. Siéntete libre de usarlo según sea necesario.

## 📧 Contacto

Para preguntas o sugerencias, contacta al propietario del proyecto:
- **Usuario de GitHub**: [@Shotylan](https://github.com/Shotylan)

---

**Última actualización**: Junio 2026

¡Gracias por usar SistemaRestaurante! 🙏
