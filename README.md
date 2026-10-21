# REPORT CARD MAKER

report-card-maker/
├── meson.build                     # Main configuration (checks for gtk4 AND sqlite3)
├── data/                           # Application metadata
│├── 
│└── 
└── src/                            # Source code directory
├── meson.build                     # Source-specific compilation rules
├── main.c                          # App entry point (initializes app and DB)
│
├── database/                       # --- DATABASE LAYER ---
│├── db-manager.c                   # Opens/closes DB, runs migrations (tables creation)
│├── db-manager.h
│├── user-model.c
│└── user-model.h                   # CRUD operations for specific entities (e.g., Users)
│
├── ui/                             # --- VIEW LAYER (UI Layouts) ---
│├── window.ui                      # Main window GtkBuilder XML file
│└── user-row.ui                    # Custom list item widget template
│
├── widgets/                        # --- CONTROLLER LAYER (UI Logic) ---
│├── my-window.c                    # Fetches data from user-model and populates UI
│├── my-window.h
│├── user-row.c
│└── user-row.h                     # Controller for individual list items
│
└── resources.gresource.xml         # Compiles the .ui files into the app binary

