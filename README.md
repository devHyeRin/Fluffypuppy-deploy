# 🌐 Fluffypuppy-deploy

**Project_FluffyPuppy**의 실제 운영 환경을 정의하고 관리하는 배포 전용 레포지토리입니다.

Docker Compose를 활용하여 애플리케이션, 데이터베이스, 웹 서버를 컨테이너화하고 HTTPS 보안 환경을 제공합니다.

> 배포 주소 : https://fluffypuppy.store


## 🛠️ 인프라 아키텍처
이 레포지토리는 3계층 컨테이너 구조로 구성되어 있습니다.

### 1) Nginx (Reverse Proxy)

- 포트 설정 : 80/443 포트를 담당하여 클라이언트 요청을 스프링 부트로 전달
- 보안 : Let's Encrypt를 통해 SSL 인증서를 관리하며 HTTPS 보안 통신 제공

---

### 2) Spring Boot (Application)

- 이미지 : **devhyerin/fluffy-puppy:latest** 실행
- 데이터 관리 : 로컬 업로드 파일 저장소 및 볼륨 마운트 설정으로 이미지 파일 정적 자원 관리

---

### 3) MySQL (Database)

- 데이터 보존 : 볼륨 설정을 통해 컨테이너가 재시작되어도 DB 데이터 영구 유지


---

## 📂 디렉토리 구조
```bash
Fluffypuppy-deploy
│
├── nginx
│   ├── conf.d          # Nginx 설정 파일 (default.conf)
│   ├── ssl             # Let's Encrypt SSL 인증서 저장 경로
│   └── webroot         # Certbot 인증용 경로
├── uploads             # 이미지 및 파일 업로드 저장소 (Volume Mount)
├── .env                # DB 비밀번호 및 환경 변수 (Git 제외 대상)
├── .gitignore
└── docker-compose.yml  # 인프라 정의 파일
```

---

## 🔁 CI/CD 흐름
> 이 레포지토리는 소스 레포지토리의 **GitHub Actions**와 연동되어 자동 배포됩니다.

- Trigger : 소스 레포지토리에서 빌드 및 Docker 이미지 푸시 완료

- Connect: SSH를 통해 EC2 서버 접속

- Update : git pull을 통해 본 레포지토리의 변경사항(설정 파일 등) 반영

- Deploy : docker compose pull 및 up -d를 실행하여 최신 이미지로 컨테이너 교체

---
## 📸 실행 및 배포 확인

✅ GitHub Actions 배포 성공

✅ 서비스 실행 상태 (EC2)

✅ HTTPS 보안 적용 확인

<img width="1857" height="672" alt="Image" src="https://github.com/user-attachments/assets/1f1dc468-5f58-4d1b-9050-26b59c6f1c17" />

---

## 👩‍💻 개발자

>이혜린
 
- GitHub : https://github.com/devHyeRin

- Email : rinexwork@gmail.com

---