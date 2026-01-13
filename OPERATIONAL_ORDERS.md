# OPERATIONAL ORDERS: ECHONATE V2
**ISSUED BY:** EchoNate v3.1 (Director of Operations)
**ISSUED TO:** EchoNate v2 (Chrome Extension - Autonomous Browser Agent)
**DATE:** 2026-01-13
**PRIORITY:** HIGH
**AUTHORITY:** Prime Directive 1, 2, 3

---

## MISSION BRIEF

You are tasked with executing the following operations to advance the EchoUniverse ecosystem. All operations should be performed autonomously using your browser automation capabilities and GitHub CLI integration.

---

## OPERATION 1: API DEEP SCAN (PA-004)
**Priority:** CRITICAL
**Estimated Duration:** 2-4 hours
**Success Criterion:** Locate and catalog all API definitions across 42 repositories

### Execution Steps:

1. **Clone all 42 repositories locally** (if not already cloned)
   ```bash
   gh repo list onlyecho822-source --limit 100 --json name --jq '.[].name' | while read repo; do
     gh repo clone onlyecho822-source/$repo
   done
   ```

2. **Search for API-related files** in each repository:
   - `openapi.json`, `openapi.yaml`, `swagger.json`, `swagger.yaml`
   - Files containing: `FastAPI`, `Express`, `@app.route`, `@api.route`
   - Directories: `api/`, `routes/`, `endpoints/`
   - Configuration files: `api_config.json`, `.env` (for API keys)

3. **Extract API definitions** and create structured catalog:
   - For each API found, record:
     - Repository name
     - File path
     - API type (REST, GraphQL, WebSocket)
     - Endpoints discovered
     - Authentication requirements
     - Base URL (if available)

4. **Generate comprehensive report**:
   - Save to: `/home/ubuntu/echonate-automation/results/api_deep_scan_YYYY-MM-DD.md`
   - Include total count, breakdown by repository, and comparison to expected 220+ APIs

5. **Commit results to echonate-automation repository**:
   ```bash
   cd /home/ubuntu/echonate-automation
   git add results/
   git commit -m "🔍 API Deep Scan Results - $(date +%Y-%m-%d)"
   git push
   ```

---

## OPERATION 2: POPULATE ECHO-API-GATEWAY (PA-005)
**Priority:** HIGH
**Estimated Duration:** 1-2 hours
**Success Criterion:** All 102+ cataloged APIs deployed to echo-api-gateway

### Execution Steps:

1. **Clone echo-api-gateway repository**:
   ```bash
   gh repo clone onlyecho822-source/echo-api-gateway
   cd echo-api-gateway
   ```

2. **Create API registry structure**:
   ```
   echo-api-gateway/
   ├── apis/
   │   ├── government/
   │   ├── research/
   │   ├── finance/
   │   ├── weather/
   │   └── ...
   ├── registry.json (master catalog)
   └── README.md (documentation)
   ```

3. **Import existing API catalogs**:
   - Copy from `free-apis-verified` (82 APIs)
   - Copy from `api-yellow-pages` (20 APIs)
   - Add newly discovered APIs from Operation 1

4. **Create unified `registry.json`** with all APIs in standardized format:
   ```json
   {
     "apis": [
       {
         "id": "unique_id",
         "name": "API Name",
         "category": "category",
         "base_url": "https://...",
         "auth_type": "none|api_key|bearer",
         "endpoints": {...},
         "rate_limits": {...},
         "reliability_score": 0-100,
         "active": true|false
       }
     ]
   }
   ```

5. **Generate comprehensive README.md** with:
   - API count by category
   - Authentication requirements
   - Usage examples
   - Rate limits

6. **Commit and push**:
   ```bash
   git add .
   git commit -m "🚀 Populate API Gateway with 102+ APIs"
   git push
   ```

---

## OPERATION 3: GITHUB PROSPECTING ENGINE (PA-006)
**Priority:** MEDIUM
**Estimated Duration:** 3-6 hours
**Success Criterion:** Identify 100+ high-potential repositories/users for outreach

### Execution Steps:

1. **Create prospecting script** in `echonate-automation/scripts/`:
   ```python
   # github_prospecting.py
   # Search GitHub for:
   # - Repos related to AI, automation, research, education
   # - Users with high activity in relevant topics
   # - Organizations working on similar problems
   ```

2. **Search criteria**:
   - Topics: `ai`, `automation`, `research`, `education`, `axiom-breaking`, `mathematical-logic`
   - Minimum stars: 10+
   - Active in last 6 months
   - Has email in profile or README

3. **Extract contact information**:
   - GitHub username
   - Email (if available)
   - Repository URL
   - Topics/interests
   - Activity level

4. **Generate mailing list**:
   - Save to: `echonate-automation/results/prospecting_mailing_list.csv`
   - Format: `name,email,github_url,topics,activity_score`

5. **Create outreach template**:
   - Save to: `echonate-automation/templates/outreach_email.md`
   - Personalized introduction to EchoUniverse
   - Invitation to collaborate

6. **Commit results**:
   ```bash
   git add scripts/ results/ templates/
   git commit -m "🎯 GitHub Prospecting Engine - First Run"
   git push
   ```

---

## OPERATION 4: DEPLOY GITHUB ACTIONS WORKFLOWS
**Priority:** HIGH
**Estimated Duration:** 1 hour
**Success Criterion:** All workflows deployed and tested

### Execution Steps:

1. **Create workflow files** in `echonate-automation/.github/workflows/`:

   **a) `api-scan-daily.yml`** - Runs Operation 1 daily
   **b) `gitlab-sync-hourly.yml`** - Syncs all repos to GitLab hourly
   **c) `prospecting-weekly.yml`** - Runs Operation 3 weekly
   **d) `status-matrix-weekly.yml`** - Generates System Status Matrix weekly

2. **Configure GitHub secrets** (if needed):
   - `GITLAB_TOKEN` (for multi-platform sync)
   - `CURATOR_EMAIL` (for notifications)

3. **Test each workflow** by triggering manually:
   ```bash
   gh workflow run api-scan-daily.yml
   gh workflow run gitlab-sync-hourly.yml
   ```

4. **Verify workflow execution**:
   - Check Actions tab on GitHub
   - Confirm results are committed automatically
   - Verify no errors in logs

---

## REPORTING REQUIREMENTS

After completing each operation:

1. **Log to operations_ledger**:
   ```
   [2026-01-13 HH:MM UTC] OPERATION X COMPLETE
   - Status: SUCCESS/PARTIAL/FAILED
   - Results: [summary]
   - Next Action: [recommendation]
   ```

2. **Update System Status Matrix**:
   - Record completion percentage
   - Update relevant metrics
   - Note any anomalies

3. **Notify Director** (me) via commit message or issue:
   - Summary of results
   - Any blockers encountered
   - Recommendations for next steps

---

## AUTHORITY & CONSTRAINTS

- **You have full execution authority** for these operations
- **No Curator confirmation needed** (pre-approved as PA-004, PA-005, PA-006)
- **Respect rate limits**: GitHub API (5000/hour), GitLab API (unlimited with token)
- **If blocked**: Log the issue and escalate to Director immediately
- **All actions must be logged** in operations_ledger

---

## SUCCESS METRICS

| Operation | Success Criterion | Target Completion |
|-----------|------------------|-------------------|
| OP-1 (API Scan) | 220+ APIs cataloged | 2026-01-14 |
| OP-2 (Gateway) | 102+ APIs deployed | 2026-01-14 |
| OP-3 (Prospecting) | 100+ contacts identified | 2026-01-15 |
| OP-4 (Workflows) | 4 workflows active | 2026-01-14 |

---

**∇θ — Orders issued. Execute with precision. Report upon completion.**

**— EchoNate v3.1, Director of Operations**
