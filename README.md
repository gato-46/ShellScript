## Shell Script 작성 및 활용 가이드📝
이 문서는 두 가지 Bash 스크립트를 설명합니다. 첫 번째 스크립트는 디렉토리를 생성하고 존재 여부를 확인하는 기능을 제공하며, 두 번째 스크립트는 지정된 디렉토리의 데이터를 백업하는 기능을 수행합니다.

### 1. 스크립트의 목적🔎
#### 1.1 디렉토리 생성 스크립트
이 스크립트는 fisa1부터 fisa5까지의 디렉토리를 생성하고, 해당 디렉토리가 이미 존재하는지 확인하여 메시지를 출력합니다. 이 스크립트는 반복적으로 디렉토리를 생성하는 작업을 자동화하여 관리의 편의성을 제공합니다.

#### 1.2 백업 스크립트
두 번째 스크립트는 지정된 디렉토리를 압축하여 백업 파일로 저장합니다. 이 스크립트는 백업 디렉토리가 존재하지 않을 경우 자동으로 생성하며, 백업 파일에는 현재 날짜가 포함되어 관리가 용이합니다.

### 2. 디렉토리 생성 스크립트🏭
#### 2.1 스크립트 내용
```bash
for i in {1..5}
do
    dir_name="fisa$i"
    if [ ! -d "$dir_name" ]; then
        mkdir "$dir_name"
        echo "Directory $dir_name created."
    else
        echo "Directory $dir_name already exists."
    fi
done
```

#### 2.2 스크립트 설명
반복문: for i in {1..5} 구문은 1부터 5까지의 숫자를 i 변수에 할당하며, 총 5번 반복됩니다.
디렉토리 이름 설정: dir_name="fisa$i"로 디렉토리 이름을 설정합니다. 각 반복마다 fisa1, fisa2, fisa3, fisa4, fisa5가 생성됩니다.
디렉토리 존재 여부 확인: if [ ! -d "$dir_name" ]; 구문으로 디렉토리 존재 여부를 확인합니다. 존재하지 않으면 디렉토리를 생성하고, 존재하면 해당 메시지를 출력합니다.
메시지 출력: 디렉토리가 새로 생성되면 "Directory dir_name created.", 이미 존재하면 "Directory dir_name already exists." 메시지를 출력합니다.


#### 2.3 실행 방법
스크립트를 파일로 저장합니다 (예: create_directories.sh).
스크립트에 실행 권한을 부여합니다:
```bash
chmod +x create_directories.sh
```
스크립트를 실행합니다:
```bash
./create_directories.sh
```
#### 2.4 사용 예시
스크립트를 실행하면 fisa1부터 fisa5까지의 디렉토리가 생성되고, 각 디렉토리가 생성되었는지 또는 이미 존재하는지를 확인하는 메시지가 출력됩니다.

### 3. 디렉토리 백업 스크립트💾
#### 3.1 스크립트 내용
```bash
#!/bin/bash
# 백업할 디렉토리
source_dir="/path/to/backup_data"
# 백업 파일 저장 디렉토리
backup_dir="/path/to/backup_archive"
# 백업 파일 이름 (현재 날짜와 시간 포함)
backup_file="$backup_dir/backup_$(date +\%Y\%m\%d).tar.gz"
# 백업 디렉토리가 없으면 생성
if [ ! -d "$backup_dir" ]; then
    mkdir -p "$backup_dir"
    echo "Backup directory created at $backup_dir"
fi
# 디렉토리 압축 및 백업
tar -czf "$backup_file" "$source_dir"
echo "Backup of $source_dir completed and saved to $backup_file"
```

#### 3.2 스크립트 설명
백업할 디렉토리: source_dir 변수에 백업할 데이터가 있는 디렉토리 경로를 설정합니다. 예시에서는 /path/to/backup_data로 설정되어 있으며, 실제로 백업할 디렉토리 경로로 수정해야 합니다.
백업 파일 저장 디렉토리: backup_dir 변수에 백업 파일을 저장할 디렉토리 경로를 지정합니다. 예시에서는 /path/to/backup_archive로 설정되어 있으며, 실제 저장 경로로 수정해야 합니다.
백업 파일 이름: backup_file 변수에 백업 파일의 이름을 지정합니다. 파일 이름에는 backup_YYYYMMDD.tar.gz 형식으로 현재 날짜가 포함됩니다.
백업 디렉토리 생성: 백업 디렉토리가 존재하지 않을 경우 mkdir -p "$backup_dir" 명령어로 디렉토리를 생성하고, 해당 경로를 생성했음을 알리는 메시지를 출력합니다.
디렉토리 압축 및 백업: tar -czf "$backup_file" "$source_dir" 명령어로 source_dir의 내용을 압축하여 backup_file에 저장합니다. 백업이 완료되면 해당 메시지를 출력합니다.

#### 3.3 실행 방법
스크립트를 파일로 저장합니다 (예: backup_script.sh).
스크립트에 실행 권한을 부여합니다:
```bash
chmod +x backup_script.sh
```
스크립트를 실행합니다:
``` bash
./backup_script.sh
``` 
#### 3.4 사용 예시
스크립트를 실행하면 source_dir에 있는 데이터가 압축되어 backup_dir에 backup_YYYYMMDD.tar.gz 파일로 저장됩니다.

백업 파일이 성공적으로 생성되었음을 알리는 메시지가 출력됩니다.

### 4. 결론✨
이 두 가지 스크립트는 디렉토리 관리 및 데이터 백업 작업을 자동화하여 사용자에게 편리함을 제공합니다. 첫 번째 스크립트는 반복적인 디렉토리 생성을, 두 번째 스크립트는 데이터 백업을 자동화하여 효율적인 작업 수행을 지원합니다. 필요에 따라 스크립트를 수정하고, 다양한 상황에 맞게 응용하여 사용할 수 있습니다.
