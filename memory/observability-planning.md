# Observability planning

Use this when production evidence can change a rollout, diagnosis, or outcome decision: new business behavior, background jobs, integrations, migrations, feature flags, retries, performance work, or failures that tests cannot reproduce fully. Skip a separate plan for trivial changes or when existing signals already answer the important question.

## Decide what to observe

Before adding telemetry, answer:

1. What decision will the signal support after deployment?
2. What does success look like, and what baseline or comparison window exists?
3. Which failures or regressions must be distinguishable?
4. Can existing logs, metrics, traces, or business data answer this?
5. Who will inspect the result, when, and what action follows a bad signal?

If a plan is useful, save observability-plan.md in the configured ticket_artifacts_dir or a user-chosen work folder. Include only relevant sections below. A plan is not permission to create an external dashboard or alert.

## Plan contents

- **Outcome and baseline:** Expected behavior, current value, comparison window, and useful segmentation.
- **Signals:** Existing and new logs, metrics, traces, or business KPIs; name their source and recording boundary.
- **Structured logs:** Static message, level, stable snake_case context fields, correlation identifier, expected volume, and retention. Exclude secrets, tokens, message bodies, and unnecessary personal data.
- **Metrics:** Type, stable domain name, unit, bounded-cardinality dimensions, numerator and denominator for ratios, and recording point. Do not use user, request, email, or other unbounded IDs as labels.
- **Dashboard instructions:** Data source, filters, time range, panels, grouping, formulas, baseline comparison, and links to relevant logs or runbooks. State the question each panel answers.
- **Thresholds and response:** Threshold, evaluation window, minimum volume, severity, owner, and action. Prefer a scheduled review when paging would not trigger immediate action.
- **Rollout checks:** What to inspect immediately, after a normal traffic cycle, and after the observation period; include rollback or feature-flag criteria.
- **Validation:** How to verify locally or in staging that signals appear with expected fields and no sensitive data.
- **Lifecycle:** Whether a signal is permanent or temporary; give temporary instrumentation an owner and removal condition.
- **Manual setup:** Steps and placeholders for external dashboard or alert links when external writes require a separate authorized action.

## Keep telemetry portable

Keep the application contract stable across visualization vendors: structured log messages, stable field names, correlation IDs, domain-oriented metrics, explicit units, and low-cardinality dimensions. Keep query syntax, dashboard JSON, alert rules, and vendor deep links outside application code.

Before changing ingestion or visualization backends, confirm the owners' decisions about format, label mapping, retention, sampling, histogram support, and log/trace correlation. Do not redesign application logs solely because the dashboard vendor changes.
