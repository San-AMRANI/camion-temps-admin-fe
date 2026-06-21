# Routing and Navigation

The application uses `react-router-dom` to manage client-side navigation. It strictly enforces role-based access control (RBAC) at the routing layer.

## Route Structure

The routing tree is divided into Public and Protected segments.

### Public Routes
- `/login`: The entry point for unauthenticated users. If an authenticated user attempts to access this route, they are automatically redirected to the dashboard.

### Protected Routes (Admin Layout)
All administrative routes are wrapped inside a protected layout component. This layout checks the Zustand store for a valid `ADMIN` session on mount.
- `/dashboard`: The main landing page post-login, displaying KPIs and charts.
- `/trucks`: Truck management interface.
- `/users`: User and operator management interface.
- `/trips`: Paginated list of all trips.
- `/trips/:id`: Dynamic route for viewing the detailed timeline and logs of a specific trip.
- `/reports`: Delay analysis and export interface.

### Fallbacks and Redirects
- **Root Redirect**: The root path `/` automatically redirects to `/dashboard`.
- **Catch-All**: Unknown paths redirect to a generic 404 Not Found page.

## Navigation Flow Protection

1. **On App Startup**: The application hydrates the Zustand store from `localStorage`.
2. **Mounting a Protected Route**:
   - The route component verifies the user role.
   - It optionally calls `GET /me` to ensure the session is still cryptographically valid on the server side.
   - If the role is not `ADMIN` or the session is invalid, the local state is cleared, and a redirection to `/login` is triggered.

## Router Mode Configuration

Controlled by the `VITE_ROUTER_MODE` variable:
- `hash` (`/#/dashboard`): Best for simple static hosting without URL rewrite capabilities.
- `browser` (`/dashboard`): Provides clean URLs but requires the hosting provider (Nginx, Vercel, Netlify) to rewrite all non-file requests to `index.html`.
