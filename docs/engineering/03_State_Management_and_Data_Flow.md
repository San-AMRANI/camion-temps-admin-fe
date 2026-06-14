# State Management and Data Flow

The application employs a hybrid approach to state management, separating global session state from localized component and data-fetching state.

## Global State: Zustand

`Zustand` is used exclusively for managing the authentication state. It provides a lightweight, un-opinionated store that is accessible anywhere in the component tree or even outside of it (e.g., in Axios interceptors).

### Authentication Store Responsibilities
- **Token Storage**: Persists the JWT token and user profile in `localStorage` for cross-session persistence.
- **Hydration**: Hydrates the state on application startup to check for an existing valid session.
- **Session Control**: Provides actions to `login` (set token/user) and `logout` (clear token/user).

## Local Component State

Standard React hooks (`useState`, `useReducer`, `useRef`) are used for UI-specific state:
- **Form State**: Managing inputs for creating/editing trucks and users.
- **UI Toggles**: Modal visibility, dropdown states, and sidebar toggles.
- **Filters**: Managing the active filters for lists (e.g., selected date range, active status filter).

## Remote Data Fetching

Data fetching from the API is handled using Axios. Since the application does not currently use a sophisticated caching layer like React Query or SWR, the data flow pattern is manual but structured:

1. **Trigger**: A component mounts or a dependency (like a pagination page or filter) changes, triggering a `useEffect` hook.
2. **Fetch**: The component calls a service function (e.g., `getTrucks(filters)`).
3. **Parse**: The service function executes the Axios request. The API modules are highly defensive:
   - They normalize pagination data (extracting `page`, `perPage`, `total`, `lastPage`).
   - They support varied backend payload structures (direct arrays, `items` keys, `users` keys).
4. **Set State**: The component receives the normalized data and updates its local state using `useState`.
5. **Render**: The UI updates to reflect the new data.

## Real-time and Parallel Execution

- **Parallel Loading**: Dashboards and complex views (like Trip Detail) use `Promise.all` to fetch disparate data points (e.g., trip core data and trip logs) in parallel, minimizing load times.
- **Derived State**: Complex metrics, such as "Reports evolution" or "Segment Durations" (Company-to-Port, Port-stay), are computed client-side from the raw fetched data before rendering.
