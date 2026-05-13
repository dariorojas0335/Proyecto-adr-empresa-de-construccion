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

**¿Estás de acuerdo con este plan?** Si lo apruebas, podemos proceder a desglosar el desarrollo y empezar con la generación del código de inicialización, modelos de datos o las primeras pantallas.
