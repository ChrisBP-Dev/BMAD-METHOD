# User-Defined Preferred Patterns and Preferences - Flutter Stack


## 🎯 Stack Principal Flutter

### Mobile Development Framework
- **Framework**: Flutter 3.32.5+ (siempre última versión estable)
- **Language**: Dart 3.8.1+ (siempre última versión compatible)
- **Platforms**: iOS, Android, Web (mobile-first approach)
- **IDE**: Android Studio / VS Code con extensiones Flutter

### State Management
- **Primary**: Riverpod 2.6.1+ (flutter_riverpod + riverpod_annotation)
- **Architecture**: Provider pattern con code generation
- **State Types**: StateProvider, FutureProvider, StreamProvider según necesidad
- **Rationale**: Type-safe, compile-time safety, excellent DevTools

### Backend & Services
- **Primary Backend**: Firebase (ecosistema completo)
- **Authentication**: Firebase Auth 5.6.0+
- **Database**: Cloud Firestore 5.6.9+
- **Functions**: Cloud Functions 5.5.2+
- **Core**: Firebase Core 3.14.0+
- **Rationale**: Ecosystem completo, escalable, excelente DX

### Navigation
- **Router**: go_router 15.2.0+
- **Pattern**: Declarative routing con type-safe routes
- **Structure**: Nested routing para complex navigation
- **Rationale**: Más flexible que Navigator 2.0 nativo

### Internationalization
- **Primary**: flutter_localizations (SDK nativo)
- **Format**: intl 0.20.2+ para formateo
- **Pattern**: ARB files con code generation
- **Support**: Multi-language desde día 1

### Code Generation & Serialization
- **Models**: freezed 3.0.6+ + freezed_annotation 3.0.0+
- **JSON**: json_annotation 4.9.0+ + json_serializable 6.9.5+
- **Riverpod**: riverpod_annotation 2.6.1+ para providers
- **Build**: build_runner 2.4.15+ para code generation

## 🤖 Artificial Intelligence

### AI Platform
- **Primary**: Vertex AI (Google Cloud)
- **Integration**: Via Cloud Functions o directo desde Flutter
- **Use Cases**: Text generation, image analysis, recommendations
- **Rationale**: Integración perfecta con Firebase, pricing competitivo

### AI Packages (cuando sea necesario)
- **HTTP**: http package para calls directas a Vertex AI
- **Cloud Functions**: firebase_functions para AI processing
- **Local ML**: tflite_flutter si se necesita procesamiento local

## 🏗️ Arquitectura Flutter Preferida (Clean Architecture + SOLID)

### Principios Arquitectónicos
- **Clean Architecture**: Separation of concerns, dependency inversion
- **SOLID Principles**: Single responsibility, open/closed, Liskov substitution, interface segregation, dependency inversion
- **Features First**: Organize by business features, not technical layers
- **Composition over Inheritance**: Prefer widget composition over complex inheritance hierarchies

### SOLID Principles en Flutter
```dart
// S - Single Responsibility Principle
// ✅ CORRECTO - Una responsabilidad por widget
class UserAvatar extends StatelessWidget {
  const UserAvatar({super.key, required this.user});
  final User user;

  @override
  Widget build(BuildContext context) {
    return CircleAvatar(
      backgroundImage: user.avatarUrl != null 
        ? NetworkImage(user.avatarUrl!) 
        : null,
      child: user.avatarUrl == null 
        ? Text(user.name[0].toUpperCase()) 
        : null,
    );
  }
}

// O - Open/Closed Principle
// ✅ CORRECTO - Extensible sin modificar
abstract class BaseButton extends StatelessWidget {
  const BaseButton({super.key});
  
  Widget buildContent(BuildContext context);
  VoidCallback? get onPressed;

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: buildContent(context),
    );
  }
}

class LoadingButton extends BaseButton {
  const LoadingButton({super.key, required this.isLoading});
  final bool isLoading;

  @override
  Widget buildContent(BuildContext context) {
    return isLoading 
      ? const CircularProgressIndicator()
      : const Text('Submit');
  }

  @override
  VoidCallback? get onPressed => isLoading ? null : () {};
}

// L - Liskov Substitution Principle
// ✅ CORRECTO - Subclasses intercambiables
abstract class DataSource<T> {
  Future<List<T>> getData();
}

class RemoteDataSource<T> implements DataSource<T> {
  @override
  Future<List<T>> getData() async {
    // Implementation
    return [];
  }
}

class LocalDataSource<T> implements DataSource<T> {
  @override
  Future<List<T>> getData() async {
    // Implementation
    return [];
  }
}

// I - Interface Segregation Principle
// ✅ CORRECTO - Interfaces específicas
abstract class Readable {
  Future<String> read();
}

abstract class Writable {
  Future<void> write(String data);
}

abstract class Cacheable {
  Future<void> cache(String key, String value);
  Future<String?> getFromCache(String key);
}

// D - Dependency Inversion Principle
// ✅ CORRECTO - Depende de abstracciones
class UserService {
  final UserRepository _repository; // Abstraction, not concrete
  
  UserService(this._repository);
  
  Future<User?> getCurrentUser() => _repository.getCurrentUser();
}
```

### Project Structure (Clean Architecture + Features First)
```
lib/
├── core/
│   ├── di/                    # Dependency injection (Riverpod providers)
│   ├── router/                # go_router configuration
│   ├── constants/             # App-wide constants
│   ├── errors/                # Error handling, exceptions
│   ├── utils/                 # Pure utility functions
│   ├── theme/                 # App theming, colors, text styles
│   └── network/               # HTTP clients, interceptors
├── features/
│   └── [feature_name]/
│       ├── data/
│       │   ├── datasources/   # Remote/Local data sources
│       │   ├── models/        # Data models (JSON serializable)
│       │   └── repositories/  # Repository implementations
│       ├── domain/
│       │   ├── entities/      # Business entities (pure Dart)
│       │   ├── repositories/  # Repository abstractions
│       │   └── usecases/      # Business logic use cases
│       └── presentation/
│           ├── pages/         # Screen-level widgets
│           ├── widgets/       # Feature-specific reusable widgets
│           ├── providers/     # Feature-specific Riverpod providers
│           └── state/         # UI state models
├── shared/
│   ├── widgets/               # App-wide reusable widgets
│   ├── extensions/            # Dart extensions
│   └── mixins/                # Reusable widget mixins
└── main.dart
```

### Clean Architecture Layers

#### 1. Domain Layer (Business Logic)
```dart
// entities/ - Pure business objects
class User {
  final String id;
  final String email;
  final String name;
  
  const User({required this.id, required this.email, required this.name});
}

// repositories/ - Abstract contracts
abstract class UserRepository {
  Future<User?> getCurrentUser();
  Future<void> signOut();
}

// usecases/ - Business operations
class GetCurrentUserUseCase {
  final UserRepository _repository;
  
  GetCurrentUserUseCase(this._repository);
  
  Future<User?> call() => _repository.getCurrentUser();
}
```

#### 2. Data Layer (External Concerns)
```dart
// models/ - Data transfer objects
@freezed
abstract class UserModel with _$UserModel {
  const factory UserModel({
    required String id,
    required String email,
    required String name,
  }) = _UserModel;
  
  factory UserModel.fromJson(Map<String, dynamic> json) => _$UserModelFromJson(json);
}

// datasources/ - External data access
abstract class UserRemoteDataSource {
  Future<UserModel?> getCurrentUser();
}

class FirebaseUserDataSource implements UserRemoteDataSource {
  final FirebaseAuth _auth;
  
  FirebaseUserDataSource(this._auth);
  
  @override
  Future<UserModel?> getCurrentUser() async {
    final user = _auth.currentUser;
    if (user == null) return null;
    
    return UserModel(id: user.uid, email: user.email!, name: user.displayName ?? '');
  }
}

// repositories/ - Implementation
class UserRepositoryImpl implements UserRepository {
  final UserRemoteDataSource _dataSource;
  
  UserRepositoryImpl(this._dataSource);
  
  @override
  Future<User?> getCurrentUser() async {
    final userModel = await _dataSource.getCurrentUser();
    if (userModel == null) return null;
    
    return User(id: userModel.id, email: userModel.email, name: userModel.name);
  }
}
```

#### 3. Presentation Layer (UI)
```dart
// providers/ - State management
@riverpod
class UserNotifier extends _$UserNotifier {
  @override
  Future<User?> build() async {
    final useCase = ref.read(getCurrentUserUseCaseProvider);
    return await useCase();
  }
}

// state/ - UI state models
@freezed
class AuthState with _$AuthState {
  const factory AuthState.initial() = _Initial;
  const factory AuthState.loading() = _Loading;
  const factory AuthState.authenticated(User user) = _Authenticated;
  const factory AuthState.unauthenticated() = _Unauthenticated;
  const factory AuthState.error(String message) = _Error;
}
```

### Firebase Architecture (Clean Architecture Compliant)
- **Domain Layer**: Pure business entities sin dependencias de Firebase
- **Data Layer**: Firebase implementations como datasources
- **Repository Pattern**: Abstract contracts en domain, implementations en data
- **Dependency Injection**: Riverpod providers para inyección de dependencias

### Dependency Injection Patterns (Riverpod)
```dart
// core/di/ - Dependency injection setup
@riverpod
FirebaseAuth firebaseAuth(FirebaseAuthRef ref) => FirebaseAuth.instance;

@riverpod
UserRemoteDataSource userRemoteDataSource(UserRemoteDataSourceRef ref) {
  return FirebaseUserDataSource(ref.read(firebaseAuthProvider));
}

@riverpod
UserRepository userRepository(UserRepositoryRef ref) {
  return UserRepositoryImpl(ref.read(userRemoteDataSourceProvider));
}

@riverpod
GetCurrentUserUseCase getCurrentUserUseCase(GetCurrentUserUseCaseRef ref) {
  return GetCurrentUserUseCase(ref.read(userRepositoryProvider));
}
```

## 📱 UI/UX Preferences & Widget Best Practices

### Widget Architecture Principles
- **NEVER return widgets from methods** - Always create proper StatelessWidget/StatefulWidget classes
- **Single Responsibility**: Each widget has one clear purpose
- **Composition over Inheritance**: Build complex UI through widget composition
- **Reusable Components**: Create widget libraries, not one-off widgets
- **Immutable State**: Use @immutable annotations, prefer const constructors

### Widget Creation Standards
```dart
// ✅ CORRECTO - Widget class
class CustomButton extends StatelessWidget {
  const CustomButton({
    super.key,
    required this.text,
    required this.onPressed,
    this.isLoading = false,
  });

  final String text;
  final VoidCallback? onPressed;
  final bool isLoading;

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: isLoading ? null : onPressed,
      child: isLoading 
        ? const CircularProgressIndicator()
        : Text(text),
    );
  }
}

// ❌ INCORRECTO - Method returning widget
Widget _buildButton(String text, VoidCallback onPressed) {
  return ElevatedButton(
    onPressed: onPressed,
    child: Text(text),
  );
}
```

### Reusable Widget Guidelines
```dart
// shared/widgets/ - App-wide reusable widgets
class AppCard extends StatelessWidget {
  const AppCard({
    super.key,
    required this.child,
    this.padding,
    this.margin,
    this.elevation,
  });

  final Widget child;
  final EdgeInsets? padding;
  final EdgeInsets? margin;
  final double? elevation;

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: margin ?? const EdgeInsets.all(8.0),
      child: Card(
        elevation: elevation ?? 2.0,
        child: Padding(
          padding: padding ?? const EdgeInsets.all(16.0),
          child: child,
        ),
      ),
    );
  }
}

// Usage with composition
class UserProfileCard extends StatelessWidget {
  const UserProfileCard({super.key, required this.user});
  
  final User user;

  @override
  Widget build(BuildContext context) {
    return AppCard(
      child: Column(
        children: [
          CircleAvatar(child: Text(user.name[0])),
          const SizedBox(height: 8),
          Text(user.name),
          Text(user.email),
        ],
      ),
    );
  }
}
```

### Design System
- **Approach**: Material Design 3 (Material You)
- **Theme**: Dynamic theming con ColorScheme.fromSeed()
- **Components**: Prefer Material 3 components
- **Custom Widgets**: Component-based architecture siguiendo SOLID principles

### Widget Organization
```dart
// features/auth/presentation/widgets/
class LoginForm extends StatefulWidget { ... }
class SignUpForm extends StatefulWidget { ... }
class AuthButton extends StatelessWidget { ... }

// shared/widgets/
class AppButton extends StatelessWidget { ... }
class AppTextField extends StatelessWidget { ... }
class LoadingOverlay extends StatelessWidget { ... }
class ErrorWidget extends StatelessWidget { ... }
```

### Responsive Design
- **Approach**: Mobile-first con adaptive layouts
- **Breakpoints**: LayoutBuilder para responsive behavior
- **Platform**: Platform-specific adaptations cuando sea necesario
- **Widget Composition**: Different widgets for different screen sizes

### Performance & Best Practices
- **const Constructors**: Always use const when possible
- **Widget Keys**: Use keys for list items and dynamic widgets
- **Images**: Cached network images con fade transitions
- **Lists**: ListView.builder para listas largas
- **Navigation**: Hero animations para transitions suaves
- **Memory**: Dispose proper de controllers y subscriptions
- **Build Method**: Keep build methods pure, no side effects

## 🧪 Testing Strategy

### Testing Framework
- **Unit Tests**: flutter_test (SDK)
- **Mocking**: mocktail 1.0.4+ (more flexible than mockito)
- **Widget Tests**: flutter_test con testWidgets
- **Integration**: integration_test package cuando sea necesario

### Testing Patterns
- **Providers**: Test providers en isolation
- **Repositories**: Mock Firebase dependencies
- **Widgets**: Test UI behavior y state changes
- **Coverage**: 80%+ para business logic

## 🔧 Development Tools & Quality

### Code Quality
- **Linting**: very_good_analysis 9.0.0+ (más estricto que flutter_lints)
- **Additional**: flutter_lints 6.0.0+ como baseline
- **Format**: dart format con line length 120
- **Import**: Relative imports para proyecto, absolute para packages

### Development Dependencies
```yaml
dev_dependencies:
  build_runner: ^2.4.15      # Code generation
  flutter_lints: ^6.0.0       # Basic linting
  flutter_test:
    sdk: flutter              # Testing framework
  freezed: ^3.0.6            # Code generation for models
  json_serializable: ^6.9.5  # JSON serialization
  mocktail: ^1.0.4           # Mocking for tests
  riverpod_annotation: ^2.6.1 # Riverpod code generation
  very_good_analysis: ^9.0.0  # Strict analysis
```

### Build Configuration
- **Release**: --obfuscate --split-debug-info para production
- **Flavors**: Development, staging, production environments
- **Assets**: Organized por feature en assets/ folder

## 🚀 Deployment & DevOps

### App Distribution
- **iOS**: TestFlight para beta, App Store para production
- **Android**: Play Console Internal Testing → Closed Testing → Production
- **CI/CD**: GitHub Actions o Bitrise para automated builds

### Environment Management
- **Config**: flutter_dotenv para environment variables
- **Flavors**: Development (dev Firebase), Production (prod Firebase)
- **Secrets**: Environment variables, nunca hardcoded

### Performance Monitoring
- **Crashes**: Firebase Crashlytics
- **Performance**: Firebase Performance Monitoring
- **Analytics**: Firebase Analytics + custom events

## ❌ Tecnologías a Evitar

### State Management
- **Avoid**: setState para complex state
- **Avoid**: BLoC/Cubit (preferir Riverpod)
- **Avoid**: Provider package (legacy, usar Riverpod)

### Navigation
- **Avoid**: Navigator 1.0 manual para apps complejas
- **Avoid**: fluro (deprecated)
- **Avoid**: auto_route (más complejo que go_router)

### Backend
- **Avoid**: Custom backends para MVPs (usar Firebase)
- **Avoid**: REST APIs custom cuando Firebase funciona
- **Avoid**: GraphQL para apps simples (overkill)

### Dependencies
- **Avoid**: Packages sin null safety
- **Avoid**: Packages sin mantenimiento activo (>6 meses)
- **Avoid**: Packages con muchas dependencies transitivas

### Anti-Patterns to Avoid
- **God Widgets**: Widgets con más de 300 líneas o múltiples responsabilidades
- **Method Widget Builders**: Métodos que retornan widgets en lugar de clases
- **Tight Coupling**: Widgets que dependen directamente de servicios externos
- **Mutable State**: State classes sin @immutable o const constructors
- **Deep Widget Trees**: Más de 10 niveles de anidación sin composition

## 📚 Lecciones Aprendidas

### Firebase
- Cloud Functions en TypeScript mejor DX que Python/Go
- Firestore compound queries require careful index planning
- Firebase Auth persistent state works excellent with Riverpod
- Cloud Functions cold starts can be mitigated with keep-warm strategies

### Flutter Performance
- ListView.builder es crucial para listas >100 items
- Image caching significant impact en user experience
- go_router navigation transitions smoother than Navigator 1.0
- Riverpod code generation prevents runtime errors

### Development Workflow
- freezed + json_serializable save significant boilerplate
- very_good_analysis catches issues early, worth the strict rules
- Firebase emulator suite essential for local development
- Hot reload works better with Riverpod than other state management

### Production Deployment
- iOS builds require specific Xcode versions, maintain compatibility matrix
- Android Play Store reviews faster than iOS App Store reviews
- Firebase Analytics data appears with ~24h delay
- App size optimization critical for emerging markets

## 🚀 Exploraciones Futuras

### Próximos a Evaluar
- **Flutter 3.32+**: Impeller engine improvements para better performance
- **Dart 3.9+**: New language features, pattern matching improvements
- **Firebase Data Connect**: New GraphQL layer for Firestore
- **Vertex AI Embeddings**: Para semantic search en apps

### Tecnologías en Radar
- **FlutterFlow**: Para rapid prototyping de UIs complejas
- **Shorebird**: Code push para Flutter apps
- **Flutter Web**: Cuando performance mejore para production apps
- **Flutter Desktop**: Para cross-platform desktop expansion

### AI Integration Opportunities
- **Vertex AI Generative APIs**: Text, image, multimodal generation
- **Firebase ML**: Custom model deployment
- **TensorFlow Lite**: Edge AI para offline capabilities
- **LangChain Dart**: Si ecosystem madura

## 🎮 Gaming Considerations (Flutter + Flame)

### Game Development (cuando aplique)
- **Engine**: Flame 1.12.0+ para 2D games
- **Performance**: Flame component system + object pooling
- **Audio**: audioplayers o flame_audio
- **Physics**: flame_forge2d para physics-based games
- **Backend**: Firebase para leaderboards, user progress, analytics

### Game-Specific Packages
```yaml
flame: ^1.29.0              # Game engine
flame_audio: ^2.11.6        # Audio system
flame_forge2d: ^0.19.0      # Physics engine
flame_riverpod: ^5.4.15     # Riverpod integration    
```

## 📝 Dependencies Standard Template

### Production Dependencies
```yaml
dependencies:
  cloud_firestore: ^5.6.9    # Always latest stable
  cloud_functions: ^5.5.2     # Always latest stable
  firebase_auth: ^5.6.0       # Always latest stable
  firebase_core: ^3.14.0      # Always latest stable
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter              # Internationalization
  flutter_riverpod: ^2.6.1   # State management
  freezed_annotation: ^3.0.0  # Code generation annotations
  go_router: ^15.2.0         # Navigation
  intl: 0.20.2               # Internationalization formatting
  json_annotation: ^4.9.0    # JSON serialization annotations
  riverpod: ^2.6.1           # State management core
```

### Development Dependencies
```yaml
dev_dependencies:
  build_runner: ^2.4.15      # Code generation runner
  flutter_lints: ^6.0.0       # Basic linting rules
  flutter_test:
    sdk: flutter              # Testing framework
  freezed: ^3.0.6            # Immutable classes generation
  json_serializable: ^6.9.5  # JSON serialization generation
  mocktail: ^1.0.4           # Testing mocks
  riverpod_annotation: ^2.6.1 # Riverpod code generation
  very_good_analysis: ^9.0.0  # Strict linting rules
```

---

## 📝 Notas de Mantenimiento

- **Última actualización**: Basado en Flutter 3.32.5 / Dart 3.8.1
- **Próxima revisión**: Cada release mayor de Flutter
- **Política de versiones**: Siempre usar latest stable, actualizar dependencies mensualmente
- **Testing**: Todas las preferencias validadas en proyectos de producción

**Este perfil técnico está optimizado para desarrollo mobile-first con Flutter + Firebase + Riverpod, priorizando developer experience, type safety, y maintainability a largo plazo.**
