# 파이썬 os 함수 정리

## 기본 설정

```python
import os
```

---

## 1. 현재 작업 디렉토리

### getcwd() : 현재 작업 디렉토리 경로 반환

```python
path = os.getcwd()
print(path)  # /Users/user/Desktop/src
```

### chdir() : 작업 디렉토리 변경

```python
os.chdir('/Users/user/Documents')
print(os.getcwd())  # /Users/user/Documents

# 다시 원래 디렉토리로
os.chdir('..')
```

---

## 2. 디렉토리 조회

### listdir() : 디렉토리의 모든 파일과 폴더 나열

```python
files = os.listdir('.')
print(files)  # ['file1.txt', 'folder1', 'file2.py', ...]

# 특정 디렉토리
files = os.listdir('/Users/user/Documents')
print(files)
```

### scandir() : 디렉토리 항목을 DirEntry 객체로 반환 (더 효율적)

```python
for entry in os.scandir('.'):
    print(f"{entry.name} - {'파일' if entry.is_file() else '폴더'}")
```

---

## 3. 경로 확인

### path.exists() : 경로가 존재하는지 확인

```python
if os.path.exists('file.txt'):
    print("파일이 존재합니다")
else:
    print("파일이 없습니다")
```

### path.isfile() : 파일인지 확인

```python
if os.path.isfile('file.txt'):
    print("파일입니다")
else:
    print("파일이 아닙니다")
```

### path.isdir() : 디렉토리인지 확인

```python
if os.path.isdir('folder'):
    print("디렉토리입니다")
else:
    print("디렉토리가 아닙니다")
```

### path.islink() : 심볼릭 링크인지 확인

```python
if os.path.islink('link'):
    print("심볼릭 링크입니다")
```

### path.isabs() : 절대 경로인지 확인

```python
print(os.path.isabs('/home/user'))  # True
print(os.path.isabs('folder'))      # False
```

---

## 4. 경로 조작

### path.join() : 경로 결합

```python
path = os.path.join('folder', 'subfolder', 'file.txt')
print(path)  # folder/subfolder/file.txt (OS에 따라 \ 또는 /)
```

### path.dirname() : 디렉토리 경로 반환

```python
path = '/home/user/documents/file.txt'
dirname = os.path.dirname(path)
print(dirname)  # /home/user/documents
```

### path.basename() : 파일이름만 반환

```python
path = '/home/user/documents/file.txt'
basename = os.path.basename(path)
print(basename)  # file.txt
```

### path.split() : 경로를 디렉토리와 파일이름으로 분할

```python
path = '/home/user/documents/file.txt'
dirname, filename = os.path.split(path)
print(dirname)   # /home/user/documents
print(filename)  # file.txt
```

### path.splitext() : 파일이름을 이름과 확장자로 분할

```python
path = 'document.txt'
name, ext = os.path.splitext(path)
print(name)  # document
print(ext)   # .txt
```

### path.abspath() : 절대 경로로 변환

```python
path = os.path.abspath('file.txt')
print(path)  # /Users/user/Desktop/src/file.txt
```

### path.realpath() : 심볼릭 링크를 실제 경로로 변환

```python
path = os.path.realpath('link')
print(path)  # 심볼릭 링크의 실제 경로
```

### path.expanduser() : ~ 를 홈 디렉토리로 변환

```python
path = os.path.expanduser('~/Documents/file.txt')
print(path)  # /Users/user/Documents/file.txt
```

---

## 5. 파일/디렉토리 생성

### mkdir() : 디렉토리 생성

```python
os.mkdir('new_folder')  # 부모 디렉토리가 있어야 함
```

### makedirs() : 디렉토리 생성 (부모 디렉토리도 함께 생성)

```python
os.makedirs('parent/child/grandchild')  # 모든 부모 디렉토리 생성

# 이미 있으면 에러 발생하지 않게
os.makedirs('folder', exist_ok=True)
```

---

## 6. 파일/디렉토리 삭제

### remove() : 파일 삭제

```python
os.remove('file.txt')  # 파일만 삭제 가능

# 없으면 에러 발생
# os.remove('nonexistent.txt')  # FileNotFoundError
```

### rmdir() : 빈 디렉토리 삭제

```python
os.rmdir('empty_folder')  # 비어있는 디렉토리만 삭제

# 비어있지 않으면 에러 발생
# os.rmdir('folder_with_files')  # OSError
```

### removedirs() : 빈 디렉토리들을 재귀적으로 삭제

```python
os.removedirs('parent/child/grandchild')  # 모두 비어있으면 모두 삭제
```

---

## 7. 파일/디렉토리 이름 변경

### rename() : 파일이나 디렉토리 이름 변경

```python
os.rename('old_name.txt', 'new_name.txt')  # 파일 이름 변경

os.rename('old_folder', 'new_folder')  # 폴더 이름 변경

# 다른 디렉토리로 이동도 가능
os.rename('file.txt', 'folder/file.txt')
```

### renames() : 경로를 변경하고 비어있는 부모 디렉토리 삭제

```python
os.renames('old_path/file.txt', 'new_path/file.txt')
```

---

## 8. 파일 정보

### stat() : 파일 정보 반환

```python
info = os.stat('file.txt')
print(info.st_size)   # 파일 크기 (바이트)
print(info.st_mtime)  # 수정 시간 (유닉스 타임스탐프)
print(info.st_atime)  # 접근 시간
print(info.st_ctime)  # 생성 시간 (또는 메타데이터 변경 시간)
print(info.st_mode)   # 파일 모드 (권한)
```

### path.getsize() : 파일 크기 반환 (바이트)

```python
size = os.path.getsize('file.txt')
print(size)  # 1024
```

### path.getmtime() : 파일 수정 시간 반환 (유닉스 타임스탐프)

```python
mtime = os.path.getmtime('file.txt')
print(mtime)  # 1699123456.789

# 읽기 쉬운 형식으로 변환
import time
readable_time = time.ctime(mtime)
print(readable_time)  # Tue Nov 5 12:30:56 2023
```

### path.getatime() : 파일 접근 시간 반환

```python
atime = os.path.getatime('file.txt')
print(atime)
```

---

## 9. 권한 및 접근성

### access() : 파일에 대한 접근 권한 확인

```python
# 파일이 존재하는지 확인
if os.access('file.txt', os.F_OK):
    print("파일이 존재합니다")

# 읽기 권한 확인
if os.access('file.txt', os.R_OK):
    print("읽기 권한이 있습니다")

# 쓰기 권한 확인
if os.access('file.txt', os.W_OK):
    print("쓰기 권한이 있습니다")

# 실행 권한 확인
if os.access('script.sh', os.X_OK):
    print("실행 권한이 있습니다")
```

### chmod() : 파일 권한 변경

```python
# 소유자: 읽기/쓰기, 그룹/기타: 읽기
os.chmod('file.txt', 0o644)

# 소유자: 읽기/쓰기/실행
os.chmod('script.sh', 0o755)
```

---

## 10. 환경 변수

### environ : 환경 변수 접근

```python
# 모든 환경 변수 조회
env_vars = os.environ
print(env_vars)

# 특정 환경 변수 조회
home = os.environ.get('HOME')
print(home)  # /Users/user

# 없는 환경 변수 (기본값 설정)
debug = os.environ.get('DEBUG', 'False')
print(debug)
```

### getenv() : 환경 변수 조회 (environ.get()과 동일)

```python
path = os.getenv('PATH')
print(path)

# 기본값 설정
timeout = os.getenv('TIMEOUT', '30')
print(timeout)
```

### putenv() : 환경 변수 설정

```python
os.putenv('MY_VAR', 'value')
print(os.getenv('MY_VAR'))  # value (이 프로세스에서만 유효)
```

---

## 11. 프로세스 관련

### system() : 시스템 명령어 실행

```python
# Windows
os.system('dir')      # 디렉토리 목록

# Linux/Mac
os.system('ls')       # 파일 목록
os.system('pwd')      # 현재 디렉토리
```

### name : 운영 체제 이름

```python
print(os.name)  # 'posix' (Linux/Mac) 또는 'nt' (Windows)

if os.name == 'nt':
    print("Windows")
else:
    print("Linux/Mac")
```

### sep : 경로 구분자

```python
print(os.sep)  # '/' (Linux/Mac) 또는 '\\' (Windows)
```

### pathsep : PATH 구분자

```python
print(os.pathsep)  # ':' (Linux/Mac) 또는 ';' (Windows)
```

---

## 12. 파일 경로 탐색

### walk() : 디렉토리 트리를 재귀적으로 순회

```python
for dirpath, dirnames, filenames in os.walk('.'):
    print(f"현재 디렉토리: {dirpath}")
    print(f"  하위 디렉토리: {dirnames}")
    print(f"  파일: {filenames}")
```

### walk() 사용 예제 : 모든 Python 파일 찾기

```python
for dirpath, dirnames, filenames in os.walk('.'):
    for filename in filenames:
        if filename.endswith('.py'):
            full_path = os.path.join(dirpath, filename)
            print(full_path)
```

---

## 13. 실제 사용 예제

### 디렉토리가 없으면 생성하고 파일 저장

```python
folder = 'data/results'
if not os.path.exists(folder):
    os.makedirs(folder)

file_path = os.path.join(folder, 'output.txt')
with open(file_path, 'w') as f:
    f.write('Hello, World!')
```

### 특정 확장자의 모든 파일 찾기

```python
def find_files(directory, extension):
    files = []
    for dirpath, dirnames, filenames in os.walk(directory):
        for filename in filenames:
            if filename.endswith(extension):
                files.append(os.path.join(dirpath, filename))
    return files

py_files = find_files('.', '.py')
for file in py_files:
    print(file)
```

### 폴더의 모든 파일 백업

```python
import shutil
from datetime import datetime

source = 'documents'
backup_name = f'backup_{datetime.now().strftime("%Y%m%d_%H%M%S")}'
backup_path = os.path.join('backups', backup_name)

os.makedirs('backups', exist_ok=True)
shutil.copytree(source, backup_path)
print(f"백업 완료: {backup_path}")
```

### 파일 크기 확인 및 정렬

```python
folder = '.'
files = []

for filename in os.listdir(folder):
    if os.path.isfile(filename):
        size = os.path.getsize(filename)
        files.append((filename, size))

# 크기순으로 정렬
files.sort(key=lambda x: x[1], reverse=True)

for filename, size in files:
    print(f"{filename}: {size} bytes")
```

### 파일 이름 일괄 변경

```python
folder = '.'
for filename in os.listdir(folder):
    if filename.endswith('.txt'):
        old_path = os.path.join(folder, filename)
        new_path = os.path.join(folder, filename.replace('.txt', '_backup.txt'))
        os.rename(old_path, new_path)
        print(f"변경: {filename} -> {os.path.basename(new_path)}")
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `getcwd()` | 현재 작업 디렉토리 |
| `chdir()` | 작업 디렉토리 변경 |
| `listdir()` | 디렉토리 내용 나열 |
| `scandir()` | 디렉토리 항목 효율적으로 반환 |
| `path.exists()` | 경로 존재 확인 |
| `path.isfile()` | 파일 확인 |
| `path.isdir()` | 디렉토리 확인 |
| `path.join()` | 경로 결합 |
| `path.dirname()` | 디렉토리 경로 |
| `path.basename()` | 파일이름 |
| `path.splitext()` | 이름과 확장자 분할 |
| `mkdir()` | 디렉토리 생성 |
| `makedirs()` | 계층적 디렉토리 생성 |
| `remove()` | 파일 삭제 |
| `rmdir()` | 디렉토리 삭제 |
| `rename()` | 이름 변경 |
| `stat()` | 파일 정보 |
| `path.getsize()` | 파일 크기 |
| `access()` | 접근 권한 확인 |
| `chmod()` | 권한 변경 |
| `environ` | 환경 변수 |
| `system()` | 시스템 명령어 실행 |
| `walk()` | 디렉토리 재귀 순회 |

