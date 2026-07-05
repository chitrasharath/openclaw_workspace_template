# Skills Log — 4Geeks API Integration

> Saved: 2026-07-05 20:39 ET

---

## Token Status

- **Valid:** ✅ Yes
- **User ID:** 20980
- **Token type:** `login`
- **Expires:** 2026-07-11T20:40:45Z (~6 days from save)
- **Tested endpoint:** `GET /v1/auth/token/{token}` returned valid response

---

## Skill Verification Results

### (1) Authenticate — ✅ WORKING

```
GET /v1/auth/token/{token}
```
Returns token info with expiry and user_id. Confirmed active.

**Also works:** `GET /v1/auth/user/me` — returns full profile, roles, permissions.

---

### (2) Get My Projects — ✅ WORKING

```
GET /v1/assignment/user/me/final_project
```
Returns `[]` (no final projects yet).

```
GET /v1/assignment/user/me/task
```
Can filter tasks by `task_type`:
| Type | Count |
|------|-------|
| PROJECT | 51 |
| EXERCISE | 142 |
| LESSON | 46 |
| **Total** | **242** |

---

### (3) Get Pending Work — ✅ WORKING

```
GET /v1/assignment/user/me/task
```

Task statuses:
| Status | Count |
|--------|-------|
| DONE | 206 |
| PENDING | 36 |

Revision statuses:
| Revision Status | Count |
|----------------|-------|
| PENDING | 196 |
| APPROVED | 46 |

---

### (4) Get Progress Summary — ✅ BUILDABLE

Between these endpoints, a progress summary can be assembled:

| Endpoint | What it gives |
|----------|---------------|
| `GET /v1/admissions/user/me` | Cohorts with syllabus versions, kickoff dates |
| `GET /v1/assignment/user/me/task` | All tasks with status, type, delivery dates |
| `GET /v1/admissions/syllabus/{slug}/version/{version}` | Full curriculum structure |

---

## Chitra's Profile (Quick Reference)

- **Name:** Chitra Sharathchandra
- **Email:** chitrasharathchandra001@gmail.com
- **User ID:** 20980
- **Joined:** 2026-02-25
- **GitHub:** chitrasharath
- **Timezone:** America/New_York

### Roles

| Academy | Role |
|---------|------|
| 4Geeks Miami (id: 4) | Student |
| 4Geeks.com (id: 47) | Student |

### Active Cohorts

| Cohort | Slug | Notes |
|--------|------|-------|
| Application telemetry | `application-telemetry-miami` | Never-ending, syllabus v2 |
| Container applications with Docker | `container-applications-with-docker-miami` | Has tasks assigned |

---

## Two Additional Skills Identified

### 🔍 Skill 5: Check Syllabus Progress

**Endpoint:** `GET /v1/admissions/syllabus/{slug}/version/{version}`

Once you have a cohort's syllabus slug and version (available from `/v1/admissions/user/me`), this endpoint returns the full module/lesson structure. Cross-reference with completed tasks to answer "how far through the program am I?"

### 📊 Skill 6: Activity & Engagement Report

**Endpoint:** `GET /v2/activity/me/activity`

Returns 100+ activity entries with `kind`, `created_at`, and metadata. Can derive:
- Last active day
- Weekly engagement patterns
- Most common activity types (dashboard views, cohort access, etc.)

---

## Notes

- All endpoints use `Authorization: Token <token>` header
- API base: `https://breathecode.herokuapp.com`
- Token stored in `TOOLS.md` as `4GEEKS_TOKEN`
- Skill file at `skills/4geeks-api-access/SKILL.md`