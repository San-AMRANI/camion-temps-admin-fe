# System Overview

The Camion Temps Admin Frontend is a single-page application (SPA) built to provide administrative control and monitoring over fleet operations. It interfaces with the backend REST API to manage trucks, users, and trips, as well as providing analytical dashboards and reports.

## Technology Stack

- **Framework**: React 19
- **Build Tool**: Vite
- **Language**: TypeScript
- **Styling**: Tailwind CSS (v4)
- **Routing**: React Router DOM (v7)
- **State Management**: Zustand (for global authentication state)
- **HTTP Client**: Axios
- **Data Visualization**: Recharts
- **PDF/QR Generation**: `qrcode` + `jsPDF`

## Architectural Highlights

- **Vite-Powered**: Utilizes Vite for fast development server starts and optimized production builds.
- **Component-Driven**: Built using functional components and React Hooks, ensuring modularity and reusability.
- **Client-Side Routing**: Implements routing completely on the client side, with support for protected routes that require administrative privileges.
- **Defensive Data Parsing**: The application incorporates robust parsing logic to handle varying API response shapes (e.g., nested wrappers vs direct arrays) and normalizes pagination and error structures before they reach UI components.

## Environment Configuration

The application relies on Vite environment variables for configuration:

- `VITE_API_BASE_URL`: The base URL for the backend API (e.g., `http://localhost:8000/api`).
- `VITE_ROUTER_MODE`: Determines the routing mode (`hash` or `browser`).

### Deployment Considerations

When deployed (e.g., to Vercel, Netlify, or Nginx), the hosting environment must be configured to fallback to `index.html` for unknown routes to support SPA deep linking. The repository includes configurations (`vercel.json`, `public/_redirects`) to facilitate this.
