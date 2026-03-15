# HMIS Compliance Reporting Views

A collection of SQL Server views designed for HMIS reporting against relational case management databases. Built to support operational dashboards, compliance monitoring, and APR preparation.

## Views Included

### 1. Active Enrollments by Program
Current enrollment counts grouped by program and project type. Useful for capacity monitoring and operational dashboards.

### 2. Data Completeness Scorecard
Calculates non-null percentages for each HUD Universal Data Element across active enrollments. Designed to run weekly so administrators can catch data quality issues before they become APR problems.

### 3. Demographics Summary
Aggregated demographic breakdown of currently enrolled clients by program. Supports Point-in-Time count preparation, chronic homelessness identification, and program equity analysis.

### 4. Length of Stay Analysis
Average and range of length-of-stay for exited clients, grouped by program and exit destination category (permanent housing, temporary/institutional, other/unknown).

### 5. Housing Outcomes Tracker
Permanent housing placement rates by program for the current HUD fiscal year (Oct 1 - Sep 30). Tracks missing destination data. Key metric for APR reporting and program performance reviews.

### 6. Weekly Error Trend
Data quality error counts by week for trending analysis. Requires a DataQualityLog table populated by automated validation jobs. Shows whether data quality is improving or declining over time.

## Why These Exist

Most HMIS platforms have built-in reporting, but it doesn't always give administrators the flexibility they need. Custom SQL views let you build dashboards and reports tailored to your specific programs and compliance requirements without waiting for the vendor to build something.

These views use a generic HMIS schema. Table and column names need to be mapped to your specific platform (CaseWorthy, ClientTrack, Clarity, etc.) before deployment.

## Technical Notes

- Written for SQL Server 2016+
- Uses CTEs (Common Table Expressions) for readability
- HUD fiscal year logic is built into the housing outcomes view
- Chronic homelessness identification follows HUD's definition (disabling condition + specific prior living situations + 365+ days)
- Exit destination categories map to HUD's permanent, temporary, and other groupings

## Schema Assumptions

The views assume a normalized schema with these core tables:

- `Client` — demographic data (name, DOB, SSN, gender, race, ethnicity, veteran status)
- `Enrollment` — program enrollment records (entry date, exit date, program ID, household ID)
- `Program` — program metadata (name, project type, funding source)
- `EntryAssessment` — data collected at enrollment (prior living situation, income, disabilities)
- `ExitAssessment` — data collected at exit (destination)
- `DataQualityLog` — error tracking from automated validation (for the trending view)

## Usage

Map the table and column names to your platform, then deploy as views in your reporting database. Connect to your BI tool of choice (Power BI, Tableau, SSRS, Excel) for visualization.

## Author

James Calby — [jamescalby.com](https://jamescalby.com)

## License

MIT
