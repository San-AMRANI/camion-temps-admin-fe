# Known Gaps and Inconsistencies

During the development and operation of the Camion Temps Admin Frontend, a few architectural gaps and UX inconsistencies have been identified. These should be addressed in future sprints.

## 1. Export Format Mismatch
- **Issue**: The UI button for exporting reports indicates "CSV / Excel". However, the actual implementation currently downloads a JSON payload.
- **Impact**: UX mismatch and potential confusion for admins expecting spreadsheet formats.
- **File affected**: Export logic in the Reports view (generating `rapport-trajets.json`).

## 2. API Base URL Configuration
- **Issue**: While the `constants.ts` file correctly attempts to read `import.meta.env.VITE_API_BASE_URL`, the project documentation (`PROJECT_STATUS.md`) historically noted it as being hardcoded. The current fallback is hardcoded to `https://scans-api.somasteel.ma/api` rather than failing loudly if the environment variable is missing during development.
- **Recommendation**: Ensure the `.env.example` is strictly followed and remove hardcoded production fallbacks in development builds to prevent accidental cross-environment requests.

## 3. Project Documentation (README)
- **Issue**: The `README.md` file contains standard template details combined with some project-specific instructions, but it could be further enhanced to fully document all local setup, Vite-specific configurations, and detailed deployment scripts for the custom SPA routing fallbacks.
- **Impact**: Developer onboarding might require additional context beyond the README.
