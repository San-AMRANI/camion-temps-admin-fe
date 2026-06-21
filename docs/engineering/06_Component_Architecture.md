# Component Architecture

The frontend application follows a modular, feature-based directory structure to ensure separation of concerns and maintainability.

## Directory Structure Overview

```text
src/
├── api/          # Axios instance, interceptors, and data fetching services
├── assets/       # Static assets (images, icons)
├── components/   # Reusable, stateless UI components (Buttons, Modals, Tables)
├── hooks/        # Custom React hooks (e.g., useAuth)
├── layouts/      # Structural layout components (e.g., AdminLayout with Sidebar)
├── pages/        # Top-level route components representing specific screens
├── routes/       # React Router configuration and route definitions
├── store/        # Zustand global state definitions
├── types/        # TypeScript interfaces and type definitions
└── utils/        # Helper functions, formatters, and error parsers
```

## Structural Layers

### 1. Presentation Layer (Pages & Layouts)
- **Pages** (`src/pages/`): These components correspond to specific routes (e.g., `Dashboard.tsx`, `Trucks.tsx`). They are responsible for fetching data, maintaining local state (filters, pagination), and orchestrating the rendering of smaller components.
- **Layouts** (`src/layouts/`): Provide the common structural shell. The `AdminLayout`, for example, includes the persistent sidebar navigation and the top header, wrapping the `Outlet` where page content is rendered.

### 2. UI Component Layer (`src/components/`)
Contains dumb/stateless components that receive data and callbacks via props.
- Examples include custom Tables, KPI Cards, Status Badges, and form inputs.
- Styled heavily with Tailwind CSS utility classes.

### 3. Service Layer (`src/api/`)
Encapsulates all logic related to backend communication.
- Prevents components from directly utilizing Axios.
- Handles the defensive parsing of responses and normalization of pagination and error payloads before returning clean, typed data to the Presentation Layer.

### 4. Global State Layer (`src/store/`)
Managed by Zustand. Currently restricted to Authentication state (`authStore.ts`). It avoids complex boilerplate by exposing simple actions (`login`, `logout`) and reactive state (`user`, `token`) that components can hook into directly.
