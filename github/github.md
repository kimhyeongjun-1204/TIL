# 깃허브

## 🌟 풀과 푸시 
#### 개념 : **로컬(local) 저장소** 와 **원격(remote) 저장소(github 등)** 간에 데이터를 주고  받는 과정

### 1️⃣ git push (푸시)
#### 개념 : 내 로컬에서 작업한 내용을 깃허브 원격 저장소에 올리기 

### ✅ 사용법

```bash
git push origin master

✔ origin : 원격 저장소 이름 (기본값: master)
         : 사용자가 설정한 깃허브의 URL을 가리킴. 

✔ master : 푸시할 브랜치 (보통 main 또는 master)
```
<br/>

### 📌 과정

```bash

1. 로컬 저장소 초기화 및 원격 저장소 연결 
git remote add origin https://github.com/kimhyeongjun-1204/Ai(레포지토리 주소)

2. 변경내용 스테이징
(1) 로컬 작업 디렉토리로 이동 
cd Ai 

(2) 변경된 모든 파일을 스테이징에 추가. 
git add . 

(3) 스테이징된 파일들을 커밋
git commit -m "커밋 메세지" 

(4) 커밋된 파일들을 원격 저장소(깃허브)에 푸시 
git push -u origin master

``` 

#### 🔹 커밋 : 변경 내용을 로컬 저장소에 저장하는 작업 

#### 🔹 푸쉬 : 로컬 저장소에 저장된 커밋들을 원격 저장소에 저장하는 작업 

<br/>

### 2️⃣ git pull (풀)
### ✅ 개념 : **github** 에 있는 최신 내용을 내 로컬 저장소(**컴퓨터**)로 가져오기 

### ✅ 사용법
```bash 
git pull origin main 
```

## 4️⃣ 브랜치 
### ✅ 개념 : git에서 독립적인 영역을 생성하여 여러 작업을 동시해 진행할 수 있게 해주는 기능 

### 🔍 주요 기능 
#### (1) 분기 : 새로운 브랜치를 사용하여 독립적인 작업 수행 

#### (2) 병합 : 완료된 작업을 메인 브랜치에 통합하여 변경사항을 반영 

<br/> 

### ✔️ 브랜치를 활용하면 여러 작업자가 동시에 작업하더라도 독립적으로 작업 가능 

