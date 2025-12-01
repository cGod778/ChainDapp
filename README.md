```mermaid
erDiagram
    JOB {
        uuid job_id PK
        string name
        string description
        string git_url
        string run_command
        string compile_command
        string test_type
        string status
        jsonb config
        string created_by
        timestamp created_date
        string updated_by
        timestamp updated_date
    }

    TEST_BATCH {
        uuid id PK
        string batch_name
        bigint schedule_id
        date start_time
        date last_time_run
        boolean active
        string created_by
        timestamp created_date
        string updated_by
        timestamp updated_date
    }

    BATCH_JOBS {
        uuid batch_id PK, FK
        uuid job_id PK, FK
    }

    TEST_RESULT {
        uuid result_id PK
        int job_type
    }

    PERF_TEST_RESULT {
        uuid result_id PK, FK
        int p50_latency_ms
        int p95_latency_ms
        int p99_latency_ms
        int volume_last_minute
        int volume_last_5_minutes
        float error_rate_percent
    }

    PERF_TEST_RESULT_CODE {
        uuid result_id PK, FK
        int error_code PK
        int count
    }

    JOB ||--o{ BATCH_JOBS : "is linked to"
    TEST_BATCH ||--o{ BATCH_JOBS : "groups jobs"

    TEST_RESULT ||--|| PERF_TEST_RESULT : "performance details"
    PERF_TEST_RESULT ||--o{ PERF_TEST_RESULT_CODE : "per error code"

raw raw

