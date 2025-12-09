# 🍝 PastaViva - Aplicación Flutter
 
> Una moderna aplicación de reservas para un restaurante italiano
 
![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)
![Flutter](https://img.shields.io/badge/flutter-3.5.4%2B-blue)
![Dart](https://img.shields.io/badge/dart-3.5.4%2B-blue)
 
## ✨ Características principales
 
- 🏠 **Pantalla de inicio** con descripción elegante del restaurante
- 📋 **Carta digital** con listado de platos, precios y descripciones  
- 📅 **Sistema de reservas** con horarios disponibles
- 🔖 **Mis reservas** para ver y cancelar tus reservas
- 👤 **Perfil de usuario** con opciones de configuración
- 🎨 **Diseño moderno** con Material Design 3
- 🔐 **Integración Supabase** para base de datos y autenticación
- 📱 **Responsive design** compatible con múltiples dispositivos
 
## 🚀 Inicio rápido
 
### Requisitos
 
- Flutter 3.5.4+
- Dart 3.5.4+
- [Supabase](https://supabase.com) (cuenta gratuita)
 
### Instalación
 
1. **Clonar el proyecto**
   ```bash
   cd c:\pata_viva\PastaViva\PastaViva
   ```
 
2. **Obtener dependencias**
   ```bash
   flutter pub get
   ```
 
3. **Configurar variables de entorno**
   
   Crear archivo `.env` en la raíz:
   ```
   SUPABASE_URL=https://tu-proyecto.supabase.co
   SUPABASE_ANON_KEY=tu_anon_key_aqui
   ```
 
4. **Configurar base de datos**
   
   - Ve a tu proyecto Supabase
   - Abre SQL Editor
   - Ejecuta el contenido de `DATABASE_SCHEMA.sql`
 
5. **Ejecutar la aplicación**
   ```bash
   flutter run
   ```
 
## 📱 Estructura de la aplicación
 
```
lib/
├── main.dart                 # Punto de entrada y navegación
├── screens/                  # 6 pantallas principales
│   ├── home_screen.dart
│   ├── carta_screen.dart
│   ├── reservas_screen.dart
│   ├── crear_reserva_screen.dart
│   ├── mis_reservas_screen.dart
│   └── perfil_screen.dart
├── models/                   # Modelos de datos
│   ├── dish.dart
│   ├── schedule.dart
│   └── reservation.dart
├── services/                 # Servicios
│   └── supabase_service.dart
├── theme/                    # Estilos y temas
└── widgets/                  # Componentes reutilizables
```
 
## 🎨 Diseño visual
 
### Colores
- **Primario:** `#D4423E` (Rojo restaurante)
- **Acento:** `#FFA500` (Naranja)
- **Fondo:** `#FAF9F6` (Crema)
 
### Componentes
- Material Design 3
- BottomNavigationBar con 5 secciones
- Cards personalizadas
- Formularios validados
- Animaciones suaves
 
## 🗺️ Navegación
 
### BottomNavigationBar
1. 🏠 **Inicio** - Pantalla principal
2. 📋 **Carta** - Menú del restaurante
3. 📅 **Reservas** - Horarios disponibles
4. 🔖 **Mis Reservas** - Tus reservaciones
5. 👤 **Perfil** - Configuración de usuario
 
## 📊 Pantallas
 
### HomeScreen
- Logo y nombre del restaurante
- Descripción y características
- Galería de fotos
- Botones de CTA: "Reservar Mesa" y "Ver Menú"
 
### CartaScreen
- ListView de platos
- Cards con: foto, nombre, precio, descripción
- Carga desde Supabase tabla `dishes`
 
### ReservasScreen
- Horarios disponibles
- Información: fecha, hora, cupos disponibles
- Botón para crear nueva reserva
- Carga desde Supabase tabla `horarios`
 
### CrearReservaScreen
- Formulario de reserva con validación
- Campos: cantidad de personas, comentarios
- Almacena en Supabase tabla `reservas`
- Confirmación con SnackBar
 
### MisReservasScreen
- Listado de reservas del usuario
- Muestra: fecha, hora, personas, estado
- Opción para cancelar reservas
- Requiere autenticación
 
### PerfilScreen
- Avatar de usuario
- Menú de opciones de configuración
- Botón de cerrar sesión
 
## 🔧 Funcionalidades técnicas
 
### Servicios Supabase
```dart
// Obtener platos
List<Dish> dishes = await SupabaseService.getDishes();
 
// Obtener horarios
List<Schedule> schedules = await SupabaseService.getSchedules();
 
// Obtener mis reservas
List<Reservation> reservations =
  await SupabaseService.getUserReservations(userId);
 
// Crear reserva
await SupabaseService.createReservation(
  userId: userId,
  date: date,
  time: time,
  numberOfPeople: people,
  comment: comment,
);
 
// Cancelar reserva
await SupabaseService.cancelReservation(reservationId);
```
 
## 📚 Documentación
 
- **[SETUP_GUIDE.md](SETUP_GUIDE.md)** - Guía de instalación detallada
- **[DATABASE_SCHEMA.sql](DATABASE_SCHEMA.sql)** - Schema de Supabase
- **[NAVIGATION_MAP.md](NAVIGATION_MAP.md)** - Mapa de navegación
- **[PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)** - Estructura del proyecto
- **[TODO.md](TODO.md)** - Tareas pendientes
 
## 🧪 Testing
 
Para verificar que el proyecto compila correctamente:
```bash
flutter analyze
flutter pub get
flutter run
```
 
## 🔒 Seguridad
 
- Row Level Security (RLS) implementada en Supabase
- Políticas de acceso para proteger datos de usuarios
- Validación de formularios en cliente
- Autenticación via Supabase Auth
 
## 📱 Tabla de base de datos
 
### dishes
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | UUID | ID único |
| name | text | Nombre del plato |
| image | text | URL o emoji de foto |
| price | decimal | Precio en USD |
| description | text | Descripción del plato |
 
### horarios
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | UUID | ID único |
| date | text | Fecha (YYYY-MM-DD) |
| time | text | Hora (HH:MM) |
| available_seats | integer | Cupos disponibles |
 
### reservas
| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | UUID | ID único |
| user_id | UUID | Usuario (FK) |
| date | text | Fecha de reserva |
| time | text | Hora de reserva |
| number_of_people | integer | Cantidad de personas |
| comment | text | Comentarios opcionales |
| status | text | 'confirmed' o 'cancelled' |
| created_at | timestamp | Fecha de creación |
 
## 🚀 Próximos pasos
 
- [ ] Implementar autenticación completa
- [ ] Agregar carrito de compras
- [ ] Sistema de pagos (Stripe/PayPal)
- [ ] Calificaciones y comentarios
- [ ] Búsqueda y filtros avanzados
- [ ] Push notifications
- [ ] Historial de órdenes
 
## 📱 Plataformas soportadas
 
- ✅ Android
- ✅ iOS
- ✅ Web
- ✅ macOS
- ✅ Windows
- ✅ Linux
 
## 📄 Licencia
 
MIT License
 
---
 
**Última actualización:** Diciembre 2, 2025
**Versión:** 1.0.0 - Structure Complete ✅
 
- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)
 
For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
 
 
