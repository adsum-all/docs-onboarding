# ADSUM - sprint progress registry (PLAYBOOK section 11)

Legend: TODO, IN PROGRESS, GREEN (CI green and section 10 audit conformant).

| Sprint | Title | Branch | CI | Audit | Status | Date | Notes |
|---|---|---|---|---|---|---|---|
| 0 | Foundations and governance | feat/sprint0-* | pending | partial | IN PROGRESS | 2026-06-28 | database CONFORME and applied on the real DB (Paris); ci-templates audit engine extended (gitleaks, jscpd). See audit 2026-06-28-sprint0. |
| 1 | Auth, RBAC and base | - | - | - | TODO | - | per role RLS policies, real Supabase auth |
| 2 | Members (CRUD, import, QR) | - | - | - | TODO | - | |
| 3 | Events and recurrence | - | - | - | TODO | - | |
| 4 | Controller offline scan | - | - | - | TODO | - | priority for the core Android APK |
| 5 | Volet B counting | - | - | - | TODO | - | |
| 6 | Stats and dashboards | - | - | - | TODO | - | materialized views |
| 7 | Full member app | - | - | - | TODO | - | |
| 8 | Admin exports, audit, settings | - | - | - | TODO | - | |
| 9 | Mobile Android and iOS | - | - | - | TODO | - | Capacitor, installable APK |
| 10 | Hardening and observability | - | - | - | TODO | - | |
| 11 | Acceptance and production | - | - | - | TODO | - | go live |

A sprint is GREEN only when its CI is green and its section 10 audit is conformant.
No sprint starts on a non green previous audit. No green sprint is ever regressed.
