# Actors and Use Cases

The Admin Frontend is strictly designed for users with administrative privileges. Any user attempting to log in without the `ADMIN` role is rejected at the authentication layer.

## Primary Actor: Administrator

The Administrator is responsible for managing the overarching fleet operations, monitoring ongoing trips, and analyzing performance metrics.

### Key Use Cases

#### 1. Authentication and Access Control
- **Login**: The admin authenticates using their credentials via the `/login` endpoint.
- **Session Protection**: The app verifies the active session. If the token expires or privileges are revoked, the app automatically logs the admin out and redirects to the login screen.

#### 2. Dashboard Monitoring
- **KPI Overview**: View high-level metrics including total trips, active trips, and average durations across different segments (company-to-port, port stay, port-to-company).
- **Trend Analysis**: Visualize daily trip volume evolution and duration distribution through interactive charts.
- **Responsive Rendering**: Utilizes `ResizeObserver` to render charts only when the container width is accurately available, preventing UI layout shifts.

#### 3. Truck Management
- **CRUD Operations**: Create, read, update, and delete truck records.
- **Status Management**: Activate or deactivate trucks depending on their operational status.
- **QR Code Generation**: Generate QR codes for trucks, which are used by operators/scanners in the field. Admins can preview these QR codes and download them as PDF documents (which include the registration number and QR image).

#### 4. User and Operator Management
- **CRUD Operations**: Manage the user accounts for operators and other personnel. When creating a user, the password length must be `>= 8` characters. For updates, the password field is optional.
- **Filtering and Pagination**: Filter the user list by role and location to easily find specific personnel.
- **Role Assignment**: Explicitly control and assign roles and locations during user creation and modification.

#### 5. Trip Tracking
- **List and Filter**: View a paginated list of all trips. Filter trips by current status, date ranges (from/to), and specific truck IDs.
- **Trip Detail View**: Open a specific trip to view its full timeline.
- **Duration Computation**: View computed durations for critical segments (Company to Port, Port Stay, Port to Company).
- **Log Inspection**: Inspect the detailed scanner/operator logs associated with a specific trip.

#### 6. Reporting and Analytics
- **Delay Analysis**: Fetch and chart delay data, categorizing delays by truck.
- **Export**: Export report payloads (currently generating a structured JSON file `rapport-trajets.json`) for external analysis.
