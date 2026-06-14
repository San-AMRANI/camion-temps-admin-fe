# API Integration

All external communication with the backend REST API is centralized using an Axios instance. This setup ensures consistent headers, error handling, and authorization across the application.

## Axios Configuration

The base Axios instance is configured using the `VITE_API_BASE_URL` environment variable.

### Interceptors

#### Request Interceptor
- **Authorization**: Automatically attaches the `Authorization` header to every outgoing request.
- It retrieves the current token from the Zustand store.
- It is designed to be resilient, supporting tokens that already include the `Bearer ` prefix as well as raw tokens.

#### Response Interceptor
- **Global Error Handling**: intercepts failed responses.
- **401 Unauthorized**: If a `401` or `403` status is returned, the interceptor assumes the session is invalid or expired. It triggers a global logout (clearing the local store) and forces a redirect to the `/login` page.

## Data Parsing and Normalization

The backend API responses can occasionally vary in shape. The frontend API modules implement a defensive normalization layer to protect UI components from these inconsistencies.

### Payload Resilience
- Functions are written to safely extract lists whether the backend returns a direct array, or an object containing arrays under keys like `data`, `items`, `users`, `trucks`, or `trips`.

### Pagination Normalization
- Pagination metadata is extracted and standardized into a consistent interface (`page`, `perPage`, `total`, `lastPage`), regardless of slight differences in how the backend formats pagination headers or wrappers.

### Error Parsing
- A shared API error parser is utilized to map common HTTP statuses (400, 404, 422, 500) and backend validation error structures into user-friendly, localized error messages suitable for display in toast notifications or form error blocks.

## API Surface

The frontend currently consumes the following backend endpoints:

### Auth
- `POST /login`
- `POST /logout`
- `GET /me`

### Users
- `GET /users`
- `POST /users`
- `PATCH /users/:id`
- `DELETE /users/:id`

### Trucks
- `GET /trucks`
- `POST /trucks`
- `PATCH /trucks/:id`
- `DELETE /trucks/:id`
- `PATCH /trucks/:id/activate`
- `PATCH /trucks/:id/deactivate`
- `POST /trucks/:id/generate-qr`

### Trips
- `GET /trips`
- `GET /trips/active`
- `GET /trips/history`
- `GET /trips/:id`
- `GET /trips/:id/logs`

### Reports
- `GET /reports/summary`
- `GET /reports/durations`
- `GET /reports/delays`
- `GET /reports/truck/:truckId`
- `GET /reports/export`
