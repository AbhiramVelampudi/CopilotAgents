# CopilotAgents


Analyze my codebase. Start with the backend Python files — read all route files, every file with SQL queries (cursor.execute, oracledb, cx_Oracle), any db connection or config files, and any models or schemas. Then move to the frontend React files to understand what features and pages exist. Take your time, be thorough, and once you have a solid understanding present it back to me before asking anything. Do not touch, execute, or connect to anything — read only.



Okay your understanding looks correct. Now proceed to Stage 2 — ask me your questions about the domain and business logic before designing the schema.


The schema looks good, I approve it. But do NOT generate Oracle DDL or touch anything Oracle related. Instead generate the Mermaid ER diagram first, then we implement on local PostgreSQL only using the connection string I'll provide.


Great. Now proceed with setting up SQLAlchemy 2.0 + Alembic on top of this — generate the ORM models from the schema we just created, configure Alembic to use the local PostgreSQL, and then start rewriting the raw Oracle SQL in the codebase into SQLAlchemy repository functions. Pause before touching any existing file.


Go in order starting from #1. Pause after each file swap and show me what changed before moving to the next.



Great work. Now handle the remaining files outside migration scope — runner.py, ban_stats.py, analytics.py and any others still importing db_connection. Same process, replace all Oracle code with SQLAlchemy. Then we'll do a final verification that zero Oracle imports remain in the entire codebase.



We were in the middle of migrating the remaining Oracle files to SQLAlchemy. The following files are still pending:

- activity_tracker.py (was mid-migration, lines 150-360 not yet read)
- infra_activity.py
- dbagent_sync.py
- sync_adba_data.py
- query.py

activities_stats.py is already done. Please read the greenfield-pg-schema.md memory file first to get context on our schema, then continue the migration from activity_tracker.py. Same rules — replace all Oracle/cx_Oracle/db_connection code with SQLAlchemy repository pattern, pause after each file.



from playwright.sync_api import sync_playwright

def test_yubikey_login():
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=False) # Keep False to see it work!
        context = browser.new_context()
        page = context.new_page()

        # 1. Create a CDP Session
        client = context.new_cdp_session(page)

        # 2. Enable WebAuthn and add a virtual device
        client.send("WebAuthn.enable")
        client.send("WebAuthn.addVirtualAuthenticator", {
            "options": {
                "protocol": "ctap2",      # Standard for YubiKey/FIDO2
                "transport": "usb",
                "hasResidentKey": True,
                "hasUserVerification": True,
                "isUserVerified": True,   # This "clicks" the button for you
                "automaticPresenceSimulation": True # Skips the manual touch requirement
            }
        })

        # 3. Navigate to your Office 365 / Teams login
        page.goto("https://login.microsoftonline.com")
        
        # Proceed with username/password... 
        # When the "Touch your security key" screen appears, 
        # the virtual authenticator will intercept it and signal success.

        browser.close()
        

Let's say I have a security key yubikey requirement for multiple sites

Instead of storing session.json and reusing it 

I don't want to store it, I want him to manually invoke local playwright browser and when he logs in , that session should be captured by the application website and be used in that (note: we should not store it anywhere it's security breach)


Fyi application is hosted on azure
