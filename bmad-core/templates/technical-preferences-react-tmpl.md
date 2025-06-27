# User-Defined Preferred Patterns and Preferences - React/Next.js Stack

## 🎯 Stack Principal React/Next.js

### Frontend Framework
- **Framework**: Next.js 15.0+ (latest stable)
- **Language**: TypeScript 5.6+ (always latest compatible)
- **Platforms**: Web (desktop-first with responsive design)
- **IDE**: VS Code con extensiones TypeScript

### State Management
- **Primary**: Zustand 5.0+ (lightweight and TypeScript-first)
- **Alternative**: React Query v5 + Context API
- **Global State**: Zustand stores con middleware
- **Server State**: TanStack Query (React Query) para data fetching
- **Rationale**: Type-safe, minimal boilerplate, excellent DevTools

### Backend & Services
- **Primary Backend**: Next.js API Routes + Vercel
- **Database**: PostgreSQL con Prisma ORM
- **Authentication**: NextAuth.js v5
- **File Storage**: Vercel Blob o AWS S3
- **Rationale**: Full-stack TypeScript, excellent DX, serverless-ready

### Styling & UI
- **Primary**: Tailwind CSS 3.4+
- **Components**: Radix UI + Tailwind
- **Icons**: Lucide React
- **Animations**: Framer Motion
- **Rationale**: Utility-first, consistent design system, accessibility-first

### Data Fetching
- **Client**: TanStack Query v5 (React Query)
- **Server**: Next.js native data fetching (fetch, cache)
- **Real-time**: WebSockets o Server-Sent Events
- **Rationale**: Declarative, caching, optimistic updates

## 🏗️ Arquitectura React Preferida (Feature-Based + Clean)

### Principios Arquitectónicos
- **Feature-Based Structure**: Organize by business features
- **Component Composition**: Favor composition over prop drilling
- **Separation of Concerns**: Logic, UI, and data layers separated
- **TypeScript-First**: All code must be type-safe

### Project Structure (Feature-Based)
```
src/
├── app/                       # Next.js App Router
│   ├── (auth)/               # Route groups
│   ├── api/                  # API routes
│   ├── globals.css           # Global styles
│   └── layout.tsx            # Root layout
├── components/
│   ├── ui/                   # Reusable UI components (buttons, inputs)
│   └── layout/               # Layout components (header, footer)
├── features/
│   └── [feature-name]/
│       ├── components/       # Feature-specific components
│       ├── hooks/            # Custom hooks
│       ├── services/         # API calls and business logic
│       ├── stores/           # Zustand stores
│       └── types/            # TypeScript types
├── lib/
│   ├── auth.ts              # Authentication config
│   ├── db.ts                # Database connection
│   ├── utils.ts             # Utility functions
│   └── validations.ts       # Zod schemas
├── hooks/                    # Shared custom hooks
└── types/                    # Global TypeScript types
```

## 📱 UI/UX Preferences & Component Best Practices

### Component Architecture Principles
- **Single Responsibility**: Each component has one clear purpose
- **Composition over Configuration**: Use children and render props
- **TypeScript Props**: All props must be typed with interfaces
- **Accessibility First**: All components must be keyboard navigable

### Component Creation Standards
```typescript
// ✅ CORRECTO - Typed component with proper exports
interface ButtonProps {
  children: React.ReactNode
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'md' | 'lg'
  disabled?: boolean
  onClick?: () => void
}

export function Button({ 
  children, 
  variant = 'primary', 
  size = 'md',
  disabled = false,
  onClick 
}: ButtonProps) {
  return (
    <button
      className={cn(buttonVariants({ variant, size }))}
      disabled={disabled}
      onClick={onClick}
    >
      {children}
    </button>
  )
}

// Export types for reuse
export type { ButtonProps }
```

### Design System
- **Approach**: Design Tokens + Component Variants
- **Theme**: CSS Variables con Tailwind
- **Components**: Radix UI primitives con custom styling
- **Dark Mode**: Built-in con next-themes

## 🧪 Testing Strategy

### Testing Framework
- **Unit/Integration**: Vitest (faster than Jest)
- **Component Testing**: React Testing Library
- **E2E**: Playwright
- **Mocking**: MSW (Mock Service Worker)

### Testing Patterns
- **Components**: Test behavior, not implementation
- **Hooks**: Test with renderHook
- **API Routes**: Integration tests con MSW
- **E2E**: Critical user paths only

## 🔧 Development Tools & Quality

### Code Quality
- **Linting**: ESLint con TypeScript rules
- **Formatting**: Prettier con Tailwind plugin
- **Type Checking**: TypeScript strict mode
- **Imports**: Auto-sorting con @trivago/prettier-plugin-sort-imports

### Build & Performance
- **Bundler**: Next.js built-in (Turbopack)
- **Performance**: Bundle analyzer, Core Web Vitals monitoring
- **Images**: Next.js Image component con optimization
- **Fonts**: Next.js Font optimization

## ❌ Tecnologías a Evitar

### State Management
- **Avoid**: Redux/Redux Toolkit (demasiado boilerplate)
- **Avoid**: MobX (no TypeScript-first)
- **Avoid**: Recoil (experimental, poco mantenimiento)

### Styling
- **Avoid**: Styled-components (runtime overhead)
- **Avoid**: CSS-in-JS libraries (performance impact)
- **Avoid**: Bootstrap (no utility-first)

### Backend
- **Avoid**: Separate Express server (cuando Next.js API routes funcionan)
- **Avoid**: REST APIs complejos (preferir tRPC si es full-stack TypeScript)
- **Avoid**: ORMs complejos (preferir Prisma)

### Anti-Patterns to Avoid
- **Prop Drilling**: Use Context o Zustand para state compartido
- **useEffect Abuse**: Prefer React Query para data fetching
- **Inline Styles**: Always use Tailwind classes
- **Any Types**: Never use `any`, prefer `unknown` o specific types
- **Default Exports**: Prefer named exports para better tree-shaking

## 📝 Dependencies Standard Template

### Production Dependencies
```json
{
  "dependencies": {
    "next": "^15.0.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "typescript": "^5.6.0",
    "@next/font": "^15.0.0",
    "tailwindcss": "^3.4.0",
    "zustand": "^5.0.0",
    "@tanstack/react-query": "^5.0.0",
    "@radix-ui/react-slot": "^1.0.2",
    "lucide-react": "^0.400.0",
    "framer-motion": "^11.0.0",
    "zod": "^3.22.0",
    "prisma": "^5.15.0",
    "@prisma/client": "^5.15.0",
    "next-auth": "^5.0.0"
  }
}
```

### Development Dependencies
```json
{
  "devDependencies": {
    "@types/node": "^20.0.0",
    "@types/react": "^18.3.0",
    "@types/react-dom": "^18.3.0",
    "eslint": "^8.57.0",
    "eslint-config-next": "^15.0.0",
    "prettier": "^3.0.0",
    "prettier-plugin-tailwindcss": "^0.5.0",
    "vitest": "^2.0.0",
    "@testing-library/react": "^16.0.0",
    "@testing-library/jest-dom": "^6.0.0",
    "playwright": "^1.40.0",
    "msw": "^2.0.0"
  }
}
```

---

**Este perfil técnico está optimizado para desarrollo web moderno con React + Next.js + TypeScript, priorizando performance, type safety, y developer experience.** 