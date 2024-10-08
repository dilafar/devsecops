### github
    https://github.com/gitleaks/gitleaks

### docker commands
    export path_to_host_folder_to_scan = source file path
    docker pull zricethezav/gitleaks:latest
    docker run -v ${path_to_host_folder_to_scan}:/path zricethezav/gitleaks:latest detect --source="/path" --verbose

### pre-commit
    ls .git/hooks/pre-commit
    ls -l .git/hooks/pre-commit
    chmod +x .git/hooks/pre-commit
