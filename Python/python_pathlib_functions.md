# 파이썬 pathlib 함수 정리

## 기본 설정

```python
from pathlib import Path
```

---

## 1. Path 객체 생성

### Path() : Path 객체 생성

```python
# 현재 디렉토리
p = Path('.')
print(p)  # .

# 절대 경로
p = Path('/home/user/documents')
print(p)  # /home/user/documents

# 상대 경로
p = Path('folder/file.txt')
print(p)  # folder/file.txt

# 여러 경로 결합하여 생성
p = Path('folder', 'subfolder', 'file.txt')
print(p)  # folder/subfolder/file.txt
```

### Path.cwd() : 현재 작업 디렉토리 반환

```python
p = Path.cwd()
print(p)  # /Users/user/Desktop/src (현재 디렉토리)
```

### Path.home() : 홈 디렉토리 반환

```python
p = Path.home()
print(p)  # /Users/user (홈 디렉토리)
```

---

## 2. 경로 조합

### / 연산자 : 경로 결합

```python
p = Path('folder') / 'subfolder' / 'file.txt'
print(p)  # folder/subfolder/file.txt

# 절대 경로와 결합
p = Path('/home') / 'user' / 'documents' / 'file.txt'
print(p)  # /home/user/documents/file.txt
```

### joinpath() : 경로 결합

```python
p = Path('folder')
p = p.joinpath('subfolder', 'file.txt')
print(p)  # folder/subfolder/file.txt
```

---

## 3. 경로 정보 조회

### name : 파일이름 (확장자 포함) 반환

```python
p = Path('/home/user/documents/file.txt')
print(p.name)  # file.txt
```

### stem : 파일이름 (확장자 제외) 반환

```python
p = Path('/home/user/documents/file.txt')
print(p.stem)  # file
```

### suffix : 파일 확장자 반환

```python
p = Path('/home/user/documents/file.txt')
print(p.suffix)  # .txt

# 여러 확장자
p = Path('archive.tar.gz')
print(p.suffix)  # .gz
print(p.suffixes)  # ['.tar', '.gz']
```

### parent : 부모 디렉토리 반환

```python
p = Path('/home/user/documents/file.txt')
print(p.parent)  # /home/user/documents

# 여러 단계 위로
print(p.parent.parent)  # /home/user
```

### parents : 모든 부모 디렉토리 반환

```python
p = Path('/home/user/documents/subfolder/file.txt')
print(list(p.parents))
# [PosixPath('/home/user/documents/subfolder'),
#  PosixPath('/home/user/documents'),
#  PosixPath('/home/user'),
#  PosixPath('/home'),
#  PosixPath('/')]
```

### parts : 경로를 구성하는 모든 부분 반환

```python
p = Path('/home/user/documents/file.txt')
print(p.parts)  # ('/', 'home', 'user', 'documents', 'file.txt')
```

### drive : 드라이브 문자 반환 (Windows)

```python
p = Path('C:\\Users\\user\\file.txt')
print(p.drive)  # C:
```

### anchor : 드라이브와 루트 반환

```python
p = Path('/home/user/file.txt')
print(p.anchor)  # /

p = Path('C:\\Users\\user\\file.txt')
print(p.anchor)  # C:\
```

---

## 4. 경로 변환

### resolve() : 절대 경로로 변환 (심볼릭 링크 해석)

```python
p = Path('folder/file.txt')
abs_p = p.resolve()
print(abs_p)  # /Users/user/Desktop/src/folder/file.txt
```

### absolute() : 절대 경로로 변환 (심볼릭 링크 해석 안 함)

```python
p = Path('folder/file.txt')
abs_p = p.absolute()
print(abs_p)  # /Users/user/Desktop/src/folder/file.txt
```

### relative_to() : 상대 경로로 변환

```python
p = Path('/home/user/documents/file.txt')
base = Path('/home/user')
rel_p = p.relative_to(base)
print(rel_p)  # documents/file.txt
```

### as_posix() : 경로를 POSIX 형식으로 변환 (슬래시 사용)

```python
p = Path('folder\\file.txt')  # Windows 경로
print(p.as_posix())  # folder/file.txt
```

### as_uri() : 경로를 URI 형식으로 변환

```python
p = Path('/home/user/documents/file.txt')
print(p.as_uri())  # file:///home/user/documents/file.txt
```

---

## 5. 파일/디렉토리 확인

### exists() : 경로가 존재하는지 확인

```python
p = Path('file.txt')
if p.exists():
    print("파일이 존재합니다")
else:
    print("파일이 없습니다")
```

### is_file() : 파일인지 확인

```python
p = Path('file.txt')
if p.is_file():
    print("파일입니다")
else:
    print("파일이 아닙니다")
```

### is_dir() : 디렉토리인지 확인

```python
p = Path('folder')
if p.is_dir():
    print("디렉토리입니다")
else:
    print("디렉토리가 아닙니다")
```

### is_symlink() : 심볼릭 링크인지 확인

```python
p = Path('link')
if p.is_symlink():
    print("심볼릭 링크입니다")
else:
    print("심볼릭 링크가 아닙니다")
```

### is_absolute() : 절대 경로인지 확인

```python
p1 = Path('/home/user/file.txt')
p2 = Path('folder/file.txt')

print(p1.is_absolute())  # True
print(p2.is_absolute())  # False
```

---

## 6. 파일 생성 및 삭제

### touch() : 빈 파일 생성 (이미 존재하면 수정 시간 업데이트)

```python
p = Path('new_file.txt')
p.touch()  # new_file.txt 생성
```

### mkdir() : 디렉토리 생성

```python
p = Path('new_folder')
p.mkdir()  # 디렉토리 생성

# 부모 디렉토리도 함께 생성
p = Path('parent/child/grandchild')
p.mkdir(parents=True, exist_ok=True)
```

### rmdir() : 빈 디렉토리 삭제

```python
p = Path('empty_folder')
p.rmdir()  # 비어있는 경우만 삭제 가능
```

### unlink() : 파일 삭제

```python
p = Path('file.txt')
p.unlink()  # 파일 삭제

# 없으면 에러 발생하지 않게
p.unlink(missing_ok=True)
```

---

## 7. 파일 읽기 및 쓰기

### read_text() : 파일 내용을 텍스트로 읽기

```python
p = Path('file.txt')
content = p.read_text(encoding='utf-8')
print(content)
```

### read_bytes() : 파일 내용을 바이트로 읽기

```python
p = Path('image.png')
content = p.read_bytes()
print(content)
```

### write_text() : 텍스트를 파일에 쓰기

```python
p = Path('file.txt')
p.write_text('Hello, World!', encoding='utf-8')
```

### write_bytes() : 바이트를 파일에 쓰기

```python
p = Path('data.bin')
p.write_bytes(b'binary data')
```

### open() : 파일 열기

```python
p = Path('file.txt')

# 읽기
with p.open('r', encoding='utf-8') as f:
    content = f.read()

# 쓰기
with p.open('w', encoding='utf-8') as f:
    f.write('Hello, World!')

# 추가
with p.open('a', encoding='utf-8') as f:
    f.write('\nNew line')
```

---

## 8. 디렉토리 탐색

### iterdir() : 디렉토리의 모든 항목 순회

```python
p = Path('folder')
for item in p.iterdir():
    print(item)
# folder/file1.txt
# folder/subfolder
# folder/file2.txt
```

### glob() : 패턴에 맞는 경로 검색 (하위 디렉토리 미포함)

```python
p = Path('.')

# 현재 디렉토리의 모든 .txt 파일
for file in p.glob('*.txt'):
    print(file)

# txt와 py 파일
for file in p.glob('*.[tp][yx]'):
    print(file)
```

### rglob() : 패턴에 맞는 경로 검색 (하위 디렉토리 포함)

```python
p = Path('.')

# 모든 하위 디렉토리의 .txt 파일
for file in p.rglob('*.txt'):
    print(file)
```

---

## 9. 파일 정보

### stat() : 파일의 상태 정보 반환

```python
p = Path('file.txt')
stat = p.stat()
print(stat.st_size)      # 파일 크기 (바이트)
print(stat.st_mtime)     # 수정 시간 (유닉스 타임스탐프)
print(stat.st_atime)     # 접근 시간
print(stat.st_ctime)     # 생성 시간 (또는 메타데이터 변경 시간)
```

### lstat() : 심볼릭 링크의 정보 반환

```python
p = Path('link')
stat = p.lstat()
```

### mkdir() + exists() 조합 : 디렉토리가 없으면 생성

```python
p = Path('folder')
p.mkdir(parents=True, exist_ok=True)
```

---

## 10. 경로 패턴 매칭

### match() : 경로가 패턴과 일치하는지 확인

```python
p = Path('/home/user/documents/file.txt')

print(p.match('*.txt'))           # True
print(p.match('documents/*.txt')) # True
print(p.match('*.md'))            # False
print(p.match('**/file.txt'))     # True
```

---

## 11. 파일 복사 및 이동

### rename() / replace() : 파일 또는 디렉토리 이름 변경

```python
p = Path('old_name.txt')
new_p = p.rename('new_name.txt')  # 파일 이름 변경, 새 Path 객체 반환
print(new_p)  # new_name.txt

# 다른 디렉토리로 이동
p = Path('file.txt')
new_p = p.rename('folder/file.txt')  # folder로 이동
```

### replace() : 파일 또는 디렉토리 덮어쓰기

```python
p = Path('old_name.txt')
new_p = p.replace('new_name.txt')  # 이미 존재하면 덮어씀
```

### shutil 함수로 파일 복사

```python
import shutil

p1 = Path('original.txt')
p2 = Path('copy.txt')

# 파일 복사
shutil.copy(p1, p2)

# 파일 이동
shutil.move(p1, p2)

# 디렉토리 복사
shutil.copytree('source_folder', 'dest_folder')

# 디렉토리 삭제
shutil.rmtree('folder')
```

---

## 12. 기타 유용한 함수

### samefile() : 두 경로가 같은 파일을 가리키는지 확인

```python
p1 = Path('file.txt')
p2 = Path('./file.txt')

if p1.samefile(p2):
    print("같은 파일입니다")
```

### with_name() : 파일이름만 변경

```python
p = Path('/home/user/documents/file.txt')
new_p = p.with_name('new_file.txt')
print(new_p)  # /home/user/documents/new_file.txt
```

### with_suffix() : 확장자만 변경

```python
p = Path('/home/user/documents/file.txt')
new_p = p.with_suffix('.md')
print(new_p)  # /home/user/documents/file.md
```

### with_stem() : 파일명만 변경 (확장자 유지)

```python
p = Path('file.txt')
new_p = p.with_stem('new_name')
print(new_p)  # new_name.txt
```

---

## 13. 실제 사용 예제

### CSV 파일 읽고 쓰기

```python
from pathlib import Path
import csv

# CSV 파일 읽기
csv_file = Path('data.csv')
with csv_file.open('r', encoding='utf-8') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# CSV 파일 쓰기
csv_file = Path('output.csv')
with csv_file.open('w', newline='', encoding='utf-8') as f:
    writer = csv.writer(f)
    writer.writerow(['이름', '나이', '도시'])
    writer.writerow(['Alice', 25, 'Seoul'])
    writer.writerow(['Bob', 30, 'Busan'])
```

### 디렉토리의 모든 이미지 파일 처리

```python
from pathlib import Path

image_dir = Path('images')

# jpg와 png 파일 찾기
for image_file in image_dir.glob('*.[jp][pn]g'):
    print(f"처리 중: {image_file.name}")

# 재귀적으로 모든 이미지 파일 찾기
for image_file in image_dir.rglob('*.png'):
    print(f"처리 중: {image_file.name}")
```

### 파일이 없으면 생성, 있으면 읽기

```python
from pathlib import Path

config_file = Path('config.txt')

if config_file.exists():
    content = config_file.read_text()
    print(f"기존 설정: {content}")
else:
    config_file.write_text("기본 설정값\n")
    print("기본 설정 파일을 생성했습니다")
```

### 디렉토리 구조 생성

```python
from pathlib import Path

# 프로젝트 구조 생성
project_dir = Path('my_project')
(project_dir / 'src').mkdir(parents=True, exist_ok=True)
(project_dir / 'tests').mkdir(parents=True, exist_ok=True)
(project_dir / 'data').mkdir(parents=True, exist_ok=True)
(project_dir / 'README.md').touch()

print("프로젝트 구조 생성 완료")
```

### 특정 확장자의 파일들을 다른 디렉토리로 이동

```python
from pathlib import Path
import shutil

source_dir = Path('source')
dest_dir = Path('backup')
dest_dir.mkdir(exist_ok=True)

for txt_file in source_dir.glob('*.txt'):
    shutil.move(str(txt_file), str(dest_dir / txt_file.name))
    print(f"이동: {txt_file.name}")
```

---

## 요약 테이블

| 함수 | 설명 |
|------|------|
| `Path()` | Path 객체 생성 |
| `Path.cwd()` | 현재 디렉토리 |
| `Path.home()` | 홈 디렉토리 |
| `/` | 경로 결합 |
| `name` | 파일이름 |
| `stem` | 파일명 (확장자 제외) |
| `suffix` | 파일 확장자 |
| `parent` | 부모 디렉토리 |
| `resolve()` | 절대 경로 변환 |
| `exists()` | 경로 존재 확인 |
| `is_file()` | 파일 확인 |
| `is_dir()` | 디렉토리 확인 |
| `mkdir()` | 디렉토리 생성 |
| `touch()` | 파일 생성 |
| `unlink()` | 파일 삭제 |
| `rmdir()` | 디렉토리 삭제 |
| `read_text()` | 텍스트 읽기 |
| `write_text()` | 텍스트 쓰기 |
| `iterdir()` | 디렉토리 순회 |
| `glob()` | 패턴으로 검색 |
| `rglob()` | 재귀적 패턴 검색 |
| `stat()` | 파일 정보 조회 |
| `with_name()` | 파일이름 변경 |
| `with_suffix()` | 확장자 변경 |

