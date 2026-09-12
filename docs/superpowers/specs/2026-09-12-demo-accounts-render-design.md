# Demo Accounts and Render Deployment

## Goal

Provide one ready-to-use account for each IADSS role and deploy the current application to Render without storing plaintext passwords in Git.

## Accounts

| Username | Role | Default local password |
|---|---|---|
| `doctor` | `doctor` | `Doctor@123` |
| `pharmacy` | `pharmacy` | `Pharmacy@123` |
| `moh` | `moh` | `Moh@123` |

Production passwords come from `DOCTOR_PASSWORD`, `PHARMACY_PASSWORD`, and `MOH_PASSWORD`. The defaults are for local/demo use only.

## Behavior

- On startup, create each demo account only when its username does not already exist.
- Use the existing PBKDF2 password hashing and role-specific IDs.
- Never overwrite an existing account or reset its password during startup.
- Keep startup idempotent across restarts and multiple deployments.
- Fail startup with a clear error in production when a required demo password is missing.

## Verification

- Add an API/database test that starts the app, logs in as all three roles, and verifies role-specific identity fields.
- Start the app again against the same database and verify that no duplicate users are created.
- Run the existing Node test suite before pushing.

## Deployment

- Add the three password variables to `.env.example` without real production secrets.
- Configure the variables in Render and deploy the existing `IADSS/render.yaml` service.
- Verify the deployed health endpoint and one login per role.

## Scope

No password-reset flow, account administration UI, or additional authentication dependency is added.
