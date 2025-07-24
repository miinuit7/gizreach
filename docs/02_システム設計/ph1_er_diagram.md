erDiagram
    users {
        int id PK
        string name
        string name_kana
        date birth_date
        string affiliation
        string station
        string email
        string password
        string role
        string profile_image_url
        string hobbies
        date created_at
        date updated_at
    }

    skill_sheets {
        int id PK
        int user_id FK
        string skills
        string self_pr
        date available_from
        date created_at
        date updated_at
    }

    projects {
        int id PK
        int skill_sheet_id FK
        date start_date
        date end_date
        string title
        string description
        string role
        int total_members
        int team_members
        string responsibilities
        boolean req_def
        boolean basic_design
        boolean detail_design
        boolean implementation
        boolean unit_test
        boolean integration_test
        boolean maintenance
        date created_at
        date updated_at
    }

    languages {
        int id PK
        string name
    }

    frameworks {
        int id PK
        string name
    }

    databases {
        int id PK
        string name
    }

    tools {
        int id PK
        string name
    }

    oses {
        int id PK
        string name
    }

    phases {
        int id PK
        string name
    }

    language_project {
        int id PK
        int language_id FK
        int project_id FK
    }

    framework_project {
        int id PK
        int framework_id FK
        int project_id FK
    }

    database_project {
        int id PK
        int database_id FK
        int project_id FK
    }

    tool_project {
        int id PK
        int tool_id FK
        int project_id FK
    }

    os_project {
        int id PK
        int os_id FK
        int project_id FK
    }

    phase_project {
        int id PK
        int phase_id FK
        int project_id FK
    }
    users ||--o{ skill_sheets : has
    skill_sheets ||--o{ projects : has
    projects ||--o{ language_project : uses
    projects ||--o{ framework_project : uses
    projects ||--o{ database_project : uses
    projects ||--o{ tool_project : uses
    projects ||--o{ os_project : uses
    projects ||--o{ phase_project : includes

    languages ||--o{ language_project : used_by
    frameworks ||--o{ framework_project : used_by
    databases ||--o{ database_project : used_by
    tools ||--o{ tool_project : used_by
    oses ||--o{ os_project : used_by
    phases ||--o{ phase_project : in
