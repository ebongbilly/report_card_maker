# Report Card Maker — Project Architecture

The project is structured around an MVC (Model-View-Controller) design pattern to separate database operations, UI layouts, and application logic.

```text
report-card-maker/
├── meson.build                   # Main build configuration (checks for GTK4 & SQLite3)
│
├── data/                         # Application metadata and assets
│
└── src/                          # Source code directory
    ├── meson.build               # Source-specific compilation rules
    ├── main.c                    # Application entry point (initializes GTK and DB)
    │
    ├── database/                 # --- MODEL LAYER (Database & Entities) ---
    │   ├── db-manager.c          # Opens/closes DB, runs migrations (table creation)
    │   ├── db-manager.h          
    │   ├── user-model.c          # CRUD operations for specific entities (e.g., Users)
    │   └── user-model.h          
    │
    ├── ui/                       # --- VIEW LAYER (UI Layouts) ---
    │   ├── window.ui             # Main window GtkBuilder XML file
    │   └── user-row.ui           # Custom list item widget template
    │
    ├── widgets/                  # --- CONTROLLER LAYER (UI Logic) ---
    │   ├── my-window.c           # Fetches data from user-model and populates the UI
    │   ├── my-window.h           
    │   ├── user-row.c            # Controller for individual list items
    │   └── user-row.h            
    │
    └── resources.gresource.xml   # Compiles .ui files into the application binary
```

### Architectural Breakdown

* **Model Layer (`src/database/`)**: Handles raw SQL data manipulation. Your business models (like `user-model.c`) query SQLite directly and return clean C structs.
* **View Layer (`src/ui/`)**: Defines the visual layouts using GTK4 XML (`.ui` files). These are compiled natively into the binary via GResource.
* **Controller Layer (`src/widgets/`)**: Binds the views and models together. Files like `my-window.c` listen for UI signals (clicks, inputs), fetch data using the database models, and dynamically update the GTK widgets.

