# User-Defined Preferred Patterns and Preferences - Flutter Stack

## 🎯 Stack Principal Flutter

### Mobile Development Framework
- **Framework**: Flutter 3.32.4+ (siempre última versión estable)
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

## 🏗️ Arquitectura Flutter Preferida (Clean Architecture + SOLID)

### Principios Arquitectónicos
- **Clean Architecture**: Separation of concerns, dependency inversion
- **SOLID Principles**: Single responsibility, open/closed, Liskov substitution, interface segregation, dependency inversion
- **Features First**: Organize by business features, not technical layers
- **Composition over Inheritance**: Prefer widget composition over complex inheritance hierarchies

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

## 📱 UI/UX Preferences & Widget Best Practices

### Widget Architecture Principles
- **NEVER return widgets from methods** - Always create proper StatelessWidget/StatefulWidget classes
- **Single Responsibility**: Each widget has one clear purpose
- **Composition over Inheritance**: Build complex UI through widget composition
- **Reusable Components**: Create widget libraries, not one-off widgets
- **Immutable State**: Use @immutable annotations, prefer const constructors

### Design System
- **Approach**: Material Design 3 (Material You)
- **Theme**: Dynamic theming con ColorScheme.fromSeed()
- **Components**: Prefer Material 3 components
- **Custom Widgets**: Component-based architecture siguiendo SOLID principles

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

### Anti-Patterns to Avoid
- **God Widgets**: Widgets con más de 300 líneas o múltiples responsabilidades
- **Method Widget Builders**: Métodos que retornan widgets en lugar de clases
- **Tight Coupling**: Widgets que dependen directamente de servicios externos
- **Mutable State**: State classes sin @immutable o const constructors
- **Deep Widget Trees**: Más de 10 niveles de anidación sin composition

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

**Este perfil técnico está optimizado para desarrollo mobile-first con Flutter + Firebase + Riverpod, priorizando developer experience, type safety, y maintainability a largo plazo.** 