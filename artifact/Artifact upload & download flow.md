              BUILD-JOB
                  │
                  ▼
          pytest + coverage
                  │
                  ▼
             coverage.xml
                  │
                  ▼
           Upload Artifact
                  │
                  ▼
           GitHub Storage
                  │
                  ▼
             SCANNER JOB
                  │
                  ▼
          Download Artifact
                  │
                  ▼
            SonarQube Scan
                  │
                  ▼
            Jenkins CD