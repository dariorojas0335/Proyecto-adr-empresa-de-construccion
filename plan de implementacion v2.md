# Plan de Implementación: Aplicación Multiplataforma "Empresa de Construcción"

A continuación, se presenta el plan de desarrollo paso a paso para la creación de la aplicación utilizando Flutter, Dart y Firebase, respetando estrictamente tu solicitud de no incluir código en esta etapa.

---

## FASE 1: Preparación del Entorno y Herramientas

**Objetivo:** Configurar el entorno de desarrollo local y seleccionar las herramientas de diseño.

1. **IDE y SDK:** * Instalar/Actualizar el SDK de Flutter (con soporte habilitado para Android, iOS, Web y Windows).
* Configurar el entorno de desarrollo utilizando **VS Code** o **Antigravity**.
* Instalar las extensiones necesarias (Flutter, Dart, Firebase Explorer).


2. **Herramientas de UI/UX:**
* Utilizar **Figma** o **Penpot** para crear los wireframes y el diseño visual basado en Material Design 3.
* Definir la paleta de colores (ej. tonos industriales: amarillos, grises, azules oscuros) y la tipografía.


3. **Herramientas de Firebase:**
* Instalar **Firebase CLI** y **FlutterFire CLI** en la terminal para vincular el proyecto automáticamente.



---

## FASE 2: Configuración del Proyecto Firebase

**Objetivo:** Configurar el backend as a service en Firebase Console con las credenciales proporcionadas.

1. **Creación del Proyecto:**
* **Nombre:** BDcrudconstruccion
* **ID:** bdcrudconstruccion
* **Número:** 375962957660
* *Regla estricta:* Deshabilitar la opción de Google Analytics durante la creación.


2. **Registro de Aplicaciones (SDKs):**
* **Android:** Registrar con el paquete `com.example.crudconstruccion`, sobrenombre `mi app construccion` y el App ID proporcionado (`1:375962957660:android:...`).
* **iOS:** Registrar con el Bundle ID `com.ios.construccion`, App Store ID `1508`, sobrenombre `Buildings apple` y el App ID correspondiente.
* **Web y Windows:** Registrar las apps correspondientes en la consola.


3. **Configuración de Autenticación:**
* Habilitar el proveedor de **Correo electrónico/Contraseña** en Firebase Authentication.


4. **Configuración de Cloud Firestore:**
* Crear la base de datos Firestore.
* *Regla estricta:* Iniciar en **Modo de prueba** (estándar, sin reglas de producción restrictivas inicialmente para permitir lectura/escritura durante el desarrollo).



---

## FASE 3: Estructura del Proyecto Flutter y Dependencias

**Objetivo:** Inicializar el proyecto multiplataforma y definir las librerías en el archivo `pubspec.yaml`.

1. **Creación del Proyecto:** Ejecutar el comando de creación de Flutter especificando las plataformas (`android, ios, web, windows`).
2. **Gestión de Dependencias (`pubspec.yaml`):**
* *Core y Backend:* `firebase_core`, `cloud_firestore`, `firebase_auth`.
* *Gestor de Estado:* `provider` (para la inyección de dependencias y reactividad).
* *UI/UX:* `google_fonts` (tipografía), `flutter_svg` (iconografía), `cached_network_image` (manejo de imágenes).
* *Utilidades:* `intl` (para formato de fechas de contratación y presupuestos).


3. **Arquitectura de Carpetas:** Estructurar el proyecto (ej. Arquitectura limpia o por capas):
* `/models` (Clases de datos).
* `/screens` o `/pages` (Vistas de UI).
* `/widgets` (Componentes reutilizables).
* `/providers` (Lógica de estado y conexión a Firebase).
* `/services` (Servicios de autenticación y base de datos).



---

## FASE 4: Diseño de la Base de Datos Firestore (Estructura de Colecciones)

**Objetivo:** Mapear el diagrama Entidad-Relación (ER) proporcionado y las especificaciones a colecciones de NoSQL en Firestore.

1. **Colección Principal: `empleados**`
* Campos definidos: `nombre`, `apellido`, `puesto`, `email`, `teléfono`, `fecha_contratacion`.


2. **Mapeo del resto del Diagrama ER (Siguientes Fases):**
* Planificar las colecciones relacionadas basadas en el diagrama: `clientes`, `proyectos`, `contratos`, `presupuestos`, `asignaciones`, `fases`, `tareas`, `gastos`, `materiales`, `proveedores`, `ordenes_compra`, `inventario`, `equipos`.
* *Estrategia NoSQL:* Definir qué datos irán como subcolecciones (ej. `tareas` dentro de un `proyecto`) y cuáles como colecciones raíz con referencias (claves foráneas almacenadas como *Strings* de Document IDs).



---

## FASE 5: Diseño y Desarrollo de UI/UX

**Objetivo:** Construir la interfaz de usuario interactiva y responsiva (adaptable a móvil, web y escritorio).

1. **Pantalla de Autenticación (Login):**
* Diseño de formulario para Email y Password.
* Validación de campos de entrada y UX (indicadores de carga, mensajes de error).


2. **Navegación Principal:**
* Implementar un menú lateral (Drawer) o barra inferior (BottomNavigationBar) adaptativo según la plataforma (Web/Windows vs Móvil).


3. **Módulo CRUD de Empleados:**
* *Read:* Pantalla de lista de empleados con diseño en tarjetas (Cards) o tablas de datos (DataTables para web/escritorio).
* *Create/Update:* Formulario reutilizable para altas y modificaciones.
* *Delete:* Diálogos de confirmación para eliminar registros.


4. **Módulos de Construcción (Vistas futuras basadas en el ER):**
* Dashboards para visualizar Proyectos, Presupuestos vs Gastos, y control de Inventario.



---

## FASE 6: Lógica de Negocio e Integración (Provider y Firebase)

**Objetivo:** Conectar la interfaz gráfica con la base de datos y manejar los estados de la aplicación.

1. **Implementación de AuthProvider:**
* Manejar el estado de la sesión del usuario (Logueado / No logueado).
* Conectar el formulario de UI con los métodos de `firebase_auth`.


2. **Implementación de EmpleadosProvider:**
* Crear métodos para escuchar en tiempo real (Streams) la colección `empleados` de Firestore.
* Desarrollar funciones para agregar, editar y eliminar documentos.


3. **Vinculación de UI y Providers:**
* Envolver la aplicación (o sub-árboles) con `MultiProvider`.
* Usar `Consumer` en las pantallas para que la UI se reconstruya automáticamente cuando haya cambios en Firestore.



---

## FASE 7: Pruebas y Despliegue Multiplataforma

**Objetivo:** Asegurar el correcto funcionamiento en los distintos ecosistemas.

1. **Pruebas (Testing):**
* Verificar la persistencia de sesión en recargas (especialmente en Web).
* Probar la adaptabilidad de la UI cambiando el tamaño de la ventana (Windows/Web) y rotando el dispositivo (iOS/Android).
* Verificar el CRUD interactuando directamente viendo los cambios en tiempo real en la consola de Firebase.


2. **Compilación por Plataforma:**
* Generar APK/AppBundle para Android usando el `App ID` correspondiente.
* Configurar Xcode y generar el build de iOS usando el `Bundle ID` (`com.ios.construccion`).
* Compilar los binarios para Windows y Web.



---

## CRUD

Comprendo perfectamente. Cuando tratamos con 16 tablas interrelacionadas, intentar abarcar todo de golpe puede generar un código desordenado. La clave del éxito aquí es el **orden de implementación**. No podemos crear un "Proyecto" si antes no tenemos un "Cliente", ni asignar "Tareas" si no hay "Fases".

Aquí tienes el plan paso a paso definitivo, estructurado secuencialmente para desarrollar el CRUD (Crear, Leer, Actualizar, Eliminar) de todas las tablas sin generar cuellos de botella.

---

## FASE 1: Inicialización y Herramientas Comunes (Semana 1)

**Objetivo:** Tener el esqueleto de la aplicación listo para empezar a inyectar lógica.

1. **Generación del Proyecto:** Crear el proyecto en VS Code o Antigravity con soporte para Android, iOS, Web y Windows (`com.example.crudconstruccion` / `com.ios.construccion`).
2. **Vinculación Firebase:** Ejecutar FlutterFire CLI para enlazar el proyecto con el ID `375962957660` y configurar Firestore.
3. **Configuración de `pubspec.yaml`:** Definir las dependencias núcleo (sin programar aún):
* `cloud_firestore`, `firebase_core`, `firebase_auth` (Backend).
* `provider` (Gestión de estado).
* Dependencias visuales y de formato.


4. **Creación de Widgets Reutilizables (Vital para 16 tablas):**
* Diseñar un formulario genérico (`CustomTextField`, `CustomDropdown`).
* Diseñar una tabla o cuadrícula genérica para listar datos, de modo que no tengamos que programar la vista de lista 16 veces desde cero.
* Diseñar un diálogo estándar para confirmar eliminaciones (Delete).



---

## FASE 2: Desarrollo del Grupo "Tablas Maestras" (Catálogos Independientes)

**Objetivo:** Desarrollar el CRUD de las tablas que no dependen de ninguna otra. Estas deben existir primero porque las demás las usarán como "llaves foráneas".

Para cada una de las siguientes tablas, el paso a paso es: *1. Crear Modelo (Dart) -> 2. Crear Servicio Firestore -> 3. Crear Provider -> 4. Crear Pantallas de Lista y Formulario.*

1. **CRUD de Clientes:** `nombre`, `tipo`, `contacto`, `email`, `teléfono`, `dirección`, `RFC/NIT`.
2. **CRUD de Empleados:** `nombre`, `apellido` (agregado por tu requerimiento), `puesto`, `email`, `teléfono`, `fecha_contratación`, `salario`, `estado`.
3. **CRUD de Proveedores:** `nombre`, `contacto`, `email`, `teléfono`, `condiciones_pago`.
4. **CRUD de Materiales:** Catálogo base con `nombre`, `descripción`, `unidad_medida`, `costo_unitario`.
5. **CRUD de Equipos:** Catálogo de maquinaria con `descripción`, `tipo`, `costo_adquisición`, `fecha_compra`, `estado`.

---

## FASE 3: Desarrollo del Grupo "Tablas de Primer Nivel" (Dependencias Simples)

**Objetivo:** Crear los módulos que requieren que las tablas maestras ya existan. En Firestore, guardaremos el ID del documento maestro como referencia.

El proceso (Modelo -> Servicio -> Provider -> UI) se repite, sumando la lógica de cargar listas desplegables (Dropdowns) para seleccionar las relaciones.

1. **CRUD de Proyectos:** Requiere seleccionar un Cliente (`cliente_id`). Maneja `nombre`, `fecha_inicio`, `fecha_fin`, `estado`, `presupuesto_estimado`.
2. **CRUD de Habilidades:** Sub-módulo de Empleados. Requiere `empleado_id`. Maneja `habilidad`, `nivel`, `certificación`.
3. **CRUD de Inventario:** Requiere seleccionar un Material (`material_id`). Maneja `cantidad_disponible`, `ubicación`.
4. **CRUD de Contratos:** Requiere seleccionar Cliente (`cliente_id`) y Proyecto (`proyecto_id`). Maneja `monto`, `estado`.

---

## FASE 4: Desarrollo del Grupo "Gestión Operativa" (Estructura de Proyectos)

**Objetivo:** Desarrollar el desglose de los proyectos. Esta es la parte más anidada del sistema.

1. **CRUD de Fases:** Requiere un Proyecto (`proyecto_id`). Maneja `nombre`, `fecha_inicio`, `fecha_fin`.
2. **CRUD de Tareas:** Requiere una Fase (`fase_id`). Maneja `nombre`, `descripción`, `estado`, `prioridad`.
3. **CRUD de Presupuestos:** Requiere un Proyecto (`proyecto_id`). Maneja el `monto_total`. (Podría estructurarse como una colección donde se detallan las partidas).

---

## FASE 5: Desarrollo del Grupo "Transacciones y Asignaciones"

**Objetivo:** Tablas de movimiento dinámico que vinculan recursos con los proyectos. Aquí la interfaz de usuario debe ser muy ágil.

1. **CRUD de Asignaciones (Personal):** Vincula un Empleado (`empleado_id`) con un Proyecto (`proyecto_id`). Registra `fecha_inicio` y `fin`.
2. **CRUD de Asignación de Equipos:** Vincula un Equipo (`equipo_id`) con un Proyecto (`proyecto_id`). Registra `fecha_inicio` y `fin`.
3. **CRUD de Órdenes de Compra:** Vincula Proveedor (`proveedor_id`) y Proyecto (`proyecto_id`). Registra `fecha`, `estado`.
4. **CRUD de Gastos:** Requiere un Proyecto (`proyecto_id`). Registra `categoría`, `monto`, `fecha`.

---

## FASE 6: Integración Final, Dashboards y Pruebas

**Objetivo:** Unir todos los módulos independientes en una experiencia cohesionada.

1. **Menú de Navegación (Drawer/SideBar):** Organizar el acceso a las 16 tablas agrupadas por categorías (RRHH, Logística, Operaciones, Finanzas).
2. **Consultas Cruzadas (Lecturas complejas):**
* En la vista de un "Proyecto", crear pestañas para leer (Read) sus Fases, Tareas, Gastos y Personal asignado (haciendo consultas a Firestore filtrando por `proyecto_id`).


3. **Validaciones de Eliminación:** Asegurar lógicamente que si intentas borrar un "Cliente", la app no te deje si este cliente tiene "Proyectos" activos (protección de integridad referencial).
4. **Pruebas Multiplataforma:** Compilar y testear la fluidez del CRUD en Web, Windows y simuladores móviles.

---

Este plan garantiza que nunca te encontrarás intentando programar una pantalla que necesita datos de otra que aún no existe.

Para el primer paso táctico y empezar a generar los cimientos de la app: **¿Te gustaría que comencemos redactando exactamente cómo quedará el archivo `pubspec.yaml` con todas las dependencias necesarias, o prefieres que comencemos directamente diseñando las clases (Modelos en Dart) del Grupo de Tablas Maestras?**

## Estructura del proyecto

Para un proyecto de esta magnitud (16 tablas y múltiples plataformas), la clave es utilizar una arquitectura limpia (**Clean Architecture**) o basada en **Capas**. Esto evita que el código se vuelva inmanejable al crecer.

A continuación, te presento la estructura de carpetas recomendada para tu proyecto `bdcrudconstruccion` en VS Code, diseñada para separar la lógica de Firebase, los modelos de datos y la interfaz de usuario.

---

## Estructura de Directorios Recomendada

```text
lib/
├── core/                        # Utilidades globales y constantes
│   ├── constants/               # Colores, estilos y strings fijos
│   ├── utils/                   # Formateadores de fecha, validadores
│   └── widgets/                 # Componentes UI compartidos (Botones, Inputs)
│
├── models/                      # Clases Dart (Espejo de tus tablas ER)
│   ├── empleado_model.dart
│   ├── proyecto_model.dart
│   ├── cliente_model.dart
│   ├── material_model.dart
│   └── ... (un modelo por cada tabla del diagrama)
│
├── providers/                   # Gestión de estado (Lógica de negocio)
│   ├── auth_provider.dart       # Login y registro
│   ├── empleado_provider.dart   # CRUD de empleados
│   ├── proyecto_provider.dart   # CRUD de proyectos y fases
│   └── inventory_provider.dart  # CRUD de materiales e inventario
│
├── services/                    # Conexión directa con Firebase
│   ├── firebase_auth_service.dart
│   └── firestore_service.dart   # Métodos genéricos de CRUD
│
├── ui/                          # Capa de Presentación (Vistas)
│   ├── auth/                    # Pantallas de Login
│   ├── home/                    # Dashboard principal
│   ├── modules/                 # Carpetas por módulo operativo
│   │   ├── rrhh/                # Vistas de Empleados y Habilidades
│   │   ├── proyectos/           # Vistas de Proyectos, Fases y Tareas
│   │   ├── logistica/           # Vistas de Inventario, Materiales y Equipos
│   │   └── finanzas/            # Vistas de Contratos, Gastos y Presupuestos
│   └── shared/                  # Layouts (Sidebar para Windows/Web, BottomNav para móvil)
│
└── main.dart                    # Punto de entrada y configuración de Providers

```

---

## Análisis de Carpetas Clave

### 1. `/models`

Aquí transformamos cada caja de tu diagrama ER en una clase Dart. Cada archivo incluirá los métodos `fromMap()` y `toMap()`, esenciales para convertir los datos de **Firestore** a objetos de la app y viceversa.

### 2. `/providers`

Es el "cerebro" de la aplicación. Aquí es donde se usa el paquete `provider`. Por ejemplo, `ProyectoProvider` tendrá funciones como `crearProyecto()`, `obtenerProyectosActivos()` o `calcularGastoTotal()`. La UI solo escucha estos cambios.

### 3. `/services`

Para mantener el código limpio, no pondremos llamadas a Firebase directamente en los Providers. Crearemos un `FirestoreService` que se encargue de las peticiones técnicas (get, add, update, delete) a las colecciones de la base de datos.

### 4. `/ui/modules`

Dado que tienes 16 tablas, lo mejor es agruparlas por **contexto de negocio**:

* **RRHH:** Centraliza el CRUD de Empleados y sus Habilidades.
* **Logística:** Une Materiales, Inventario, Equipos y Proveedores.
* **Operaciones:** Todo lo relacionado a la construcción física (Proyectos, Fases, Tareas).
* **Finanzas:** Maneja la parte económica (Contratos, Presupuestos, Gastos, Órdenes de Compra).

---

## Archivos de Configuración Externos

Fuera de la carpeta `lib/`, recuerda que debido a tu configuración multiplataforma, tendrás:

* `/android/app/google-services.json` (Configuración de Firebase para Android).
* `/ios/Runner/GoogleService-Info.plist` (Configuración de Firebase para iOS).
* `/web/index.html` (Donde se añaden los scripts de Firebase para la versión Web).

**¿Te parece adecuada esta organización para empezar?** Si es así, el siguiente paso lógico es definir el archivo `pubspec.yaml` con las dependencias exactas para que el proyecto pueda compilar estas carpetas.
