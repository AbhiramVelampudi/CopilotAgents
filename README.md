# CopilotAgents


Analyze my codebase. Start with the backend Python files — read all route files, every file with SQL queries (cursor.execute, oracledb, cx_Oracle), any db connection or config files, and any models or schemas. Then move to the frontend React files to understand what features and pages exist. Take your time, be thorough, and once you have a solid understanding present it back to me before asking anything. Do not touch, execute, or connect to anything — read only.



Okay your understanding looks correct. Now proceed to Stage 2 — ask me your questions about the domain and business logic before designing the schema.


The schema looks good, I approve it. But do NOT generate Oracle DDL or touch anything Oracle related. Instead generate the Mermaid ER diagram first, then we implement on local PostgreSQL only using the connection string I'll provide.


Great. Now proceed with setting up SQLAlchemy 2.0 + Alembic on top of this — generate the ORM models from the schema we just created, configure Alembic to use the local PostgreSQL, and then start rewriting the raw Oracle SQL in the codebase into SQLAlchemy repository functions. Pause before touching any existing file.
