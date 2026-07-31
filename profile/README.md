<div align="center">
  <h1>🎯 Pick Me Now 🎯</h1>
  <!-- 로고 이미지 첨부 (GitHub 이슈/PR에 드래그해서 나온 링크 사용) -->
  <!-- <img width="512" height="512" alt="Pick Me Now Logo" src="이미지_링크" /> -->

  <p>
    <b><!-- 프로젝트 기간 예: 2026.06.01 - 2026.07.31 --></b>
  </p>
  <br/>
  <!-- 대표 배너 이미지 첨부 -->
  <!-- <img width="100%" alt="Pick Me Now Banner" src="이미지_링크" /> -->
  <br/>
  <br/>
</div>

# 📖 Table of Contents
* [Introduction](#introduction)
* [Demo](#demo)
* [API](#api)
* [System Architecture](#system-architecture)
* [Tech Stack](#tech-stack)
* [How to start](#how-to-start)
* [Directory Structure](#directory-structure)
* [Team Members](#team-members)

<br>

<a id="introduction"></a>
# 📣 Introduction
### URL
> https://www.pickmenow.co.kr

### API
> https://api.pickmenow.co.kr

### 프로젝트 소개
- **여러 명이 각자 폰으로 접속해 같은 화면을 실시간으로 함께 즐기는 멀티플레이 파티 게임**
- **룰렛 · 투표 · 제비뽑기 · 순서 정하기 · 사다리타기 · 풍선 터뜨리기 — 6종 게임 제공**
- **WebSocket(Socket.io) 실시간 동기화로 모든 참가자가 같은 결과를 동시에 확인**
- **크롬 확장 · Zoom · 구글 미트 안에 그대로 띄우는 임베드(Thin Shell) 지원**
- **끊겨도 자리를 지켜주는 Reclaim — 모바일에서 잠깐 끊겨도 게임 속 내 자리가 그대로**

<br>

<a id="demo"></a>
# 🕺🏻 Demo

### 방 만들기 / 참여 (QR · 참여 코드)
> 방장이 방을 만들고, 참가자는 QR 또는 참여 코드로 각자 폰에서 입장합니다.
<!-- <img src="이미지_링크" width="100%" alt="Create & Join" /> -->

### 게임 선택 & 실시간 진행
> 방장이 게임을 고르면 참가자 전원 화면이 동시에 바뀌고, 결과가 즉시 공유됩니다.
<!-- 데모 영상 링크 첨부 -->

### 임베드 (Zoom · Google Meet · Chrome)
> 회의 중에 앱을 바로 열어 게임을 시작하고, 참가자는 폰으로 입장합니다.

**Zoom**
<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/embed-zoom.gif" width="600" alt="Zoom 임베드 데모" />
</div>

**Google Meet + Chrome 확장**
<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/embed-meet-chrome.gif" width="600" alt="Google Meet + Chrome 임베드 데모" />
</div>

### 🎮 게임 6종
> 상황에 맞게 6가지 방식으로, 다 같이 실시간으로 정할 수 있어요. (아래는 각 게임 데모 GIF)
>
> <sub>💡 소리 포함 실제 영상으로 바꾸려면, GitHub 편집창에서 해당 GIF를 지우고 그 자리에 영상 파일(.mov/.mp4)을 드래그해 올리면 영상 플레이어로 재생됩니다.</sub>

#### 🎡 룰렛
> 원판을 돌려 당첨 하나를 뽑아요.

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/roulette.gif" width="300" alt="룰렛 데모" />
</div>


#### 🗳️ 투표하기
> 다 같이 투표해 최다 득표를 정해요. (실시간 집계 · 공동 1위 지원)

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/vote.gif" width="300" alt="투표하기 데모" />
</div>


#### 🎫 제비뽑기
> 제비를 뽑아 꽝을 피해요. (제비 수 · 꽝 개수 설정)

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/draw.gif" width="300" alt="제비뽑기 데모" />
</div>


#### 🔢 순서 정하기
> 항목을 무작위 순서로 줄 세워요.

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/order.gif" width="300" alt="순서 정하기 데모" />
</div>


#### 🪜 사다리타기
> 사다리를 타고 내려가 짝을 정해요.

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/ladder.gif" width="300" alt="사다리타기 데모" />
</div>


#### 🎈 풍선 터뜨리기
> 돌아가며 펌프하다 터뜨린 사람이 걸려요. (턴제)

<div align="center">
  <img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/demos/balloon.gif" width="300" alt="풍선 터뜨리기 데모" />
</div>

<br>

<a id="api"></a>
# 📁 API
> REST(방 생성·조회) + **Socket.io(`/rooms` 네임스페이스) 이벤트 기반 실시간 API** 로 구성됩니다.

- **REST**: `POST /api/rooms`(방 생성) · `GET /api/rooms/:roomId`(방 조회)
- **Socket.io (실시간)**
  - 받는 이벤트: `room:join` · `game:begin` · `vote:cast` · `draw:pick` · `balloon:pump` …
  - 보내는 이벤트: `room:state` · `participant:joined` / `participant:left` · `vote:updated` · `game:begin` · `game:result` · `game:aborted` …
<!-- API 명세 이미지/문서 링크 첨부 -->

<br>

<a id="system-architecture"></a>
# 🏛️ System Architecture
> Frontend(Vercel) ⇄ HTTPS/WSS ⇄ Caddy(리버스 프록시·Let's Encrypt) → NestJS(EC2·Docker) ⇄ Redis(실시간 상태) · PostgreSQL(누적 통계)

<div align="center">
  <img width="100%" alt="System Architecture" src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/system-architecture.png" />
</div>

- **실시간 상태는 전부 Redis** (방·참가자·게임 상태) — 인메모리 + TTL 자동 소멸
- **누적 통계만 PostgreSQL(Prisma)** — 영구 보관
- **Caddy 리버스 프록시**가 유일한 공개 입구(80/443), 앱·DB·Redis는 외부에 미노출

<br>

<a id="tech-stack"></a>
# 💻 Tech Stack

<div align="center">
  <table>
    <tr>
      <th width="15%">Field</th>
      <th width="85%">Technology of Use</th>
    </tr>
    <tr>
      <td align="center"><b>Frontend</b></td>
      <td>
        <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black">
        <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white">
        <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white">
        <img src="https://img.shields.io/badge/Zustand-443E38?style=for-the-badge&logo=react&logoColor=white">
        <img src="https://img.shields.io/badge/React_Query-FF4154?style=for-the-badge&logo=react-query&logoColor=white">
        <img src="https://img.shields.io/badge/React_Router-CA4245?style=for-the-badge&logo=react-router&logoColor=white">
        <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white">
      </td>
    </tr>
    <tr>
      <td align="center"><b>Backend</b></td>
      <td>
        <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white">
        <img src="https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white">
        <img src="https://img.shields.io/badge/Socket.io-010101?style=for-the-badge&logo=socketdotio&logoColor=white">
        <img src="https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white">
        <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white">
      </td>
    </tr>
    <tr>
      <td align="center"><b>Database</b></td>
      <td>
        <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white">
        <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white">
      </td>
    </tr>
    <tr>
      <td align="center"><b>Realtime · Embed</b></td>
      <td>
        <img src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socketdotio&logoColor=white">
        <img src="https://img.shields.io/badge/Zoom_Apps_SDK-2D8CFF?style=for-the-badge&logo=zoom&logoColor=white">
        <img src="https://img.shields.io/badge/Chrome_Extension-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white">
        <img src="https://img.shields.io/badge/Google_Meet-00897B?style=for-the-badge&logo=googlemeet&logoColor=white">
      </td>
    </tr>
    <tr>
      <td align="center"><b>DevOps</b></td>
      <td>
        <img src="https://img.shields.io/badge/AWS_EC2-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white">
        <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
        <img src="https://img.shields.io/badge/Caddy-1F88C0?style=for-the-badge&logo=caddy&logoColor=white">
        <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white">
        <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white">
      </td>
    </tr>
    <tr>
      <td align="center"><b>ETC</b></td>
      <td>
        <img src="https://img.shields.io/badge/Notion-000000?style=for-the-badge&logo=notion&logoColor=white">
        <img src="https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">
        <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white">
      </td>
    </tr>
  </table>
</div>

<br>

<a id="how-to-start"></a>
# 📓 How To Start

### Clone The Repository
```bash
git clone https://github.com/Project-PickMeNow/Backend.git
git clone https://github.com/Project-PickMeNow/Frontend.git
```

### Backend — env setting (`.env`)
```
# App
PORT=3000
FRONTEND_BASE_URL=http://localhost:5173

# PostgreSQL (Prisma)
DATABASE_URL=postgresql://USER:PASSWORD@localhost:5432/pickmenow

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# 방 수명(초, 기본 3일)
ROOM_TTL_SECONDS=259200

# 배포(선택) — Caddy 리버스 프록시
DOMAIN=api.pickmenow.co.kr
ACME_EMAIL=
```

### Backend — Run
```bash
cd Backend
docker compose up -d          # PostgreSQL · Redis 기동
npx prisma migrate deploy     # DB 스키마 반영
npm install
npm run start:dev             # NestJS 실행 (http://localhost:3000)
```

### Frontend — env setting (`.env`)
```
VITE_API_BASE_URL=http://localhost:3000
# 구글 미트 애드온(선택) — Google Cloud 프로젝트 번호
VITE_MEET_CLOUD_PROJECT_NUMBER=
```

### Frontend — Install & Run
```bash
cd Frontend
npm install
npm run dev                   # Vite 개발 서버 (http://localhost:5173)
```

<br/>

<a id="directory-structure"></a>
# 📁 Directory Structure

<details>
<summary>📂 Backend (펼치기/접기)</summary>
<pre>
📂 src
 ┣ 📂 common          # 상수(redis-keys · room · draw · balloon) · 공통 타입 · 에러 코드
 ┣ 📂 infra           # Redis(RedisService) · Prisma(PrismaService) 연결
 ┣ 📂 modules
 ┃ ┣ 📂 room          # 방 생성/입장/퇴장 (RoomGateway · RoomService · controller)
 ┃ ┣ 📂 game          # 6종 게임 로직 (GameGateway · GameService · engines: roulette·ladder·random)
 ┃ ┗ 📂 stats         # 누적 통계 (Prisma · Postgres)
 ┣ 📜 main.ts · app.module.ts · configure-app.ts

📂 (root)
 ┣ 📂 prisma          # schema.prisma · migrations
 ┣ 📜 Caddyfile       # 리버스 프록시(HTTPS/wss 자동)
 ┗ 📜 docker-compose.yml · docker-compose.prod.yml · Dockerfile
</pre>
</details>

<details>
<summary>📂 Frontend (펼치기/접기)</summary>
<pre>
📂 src
 ┣ 📂 features        # 기능 모듈
 ┃ ┣ 📂 room          # 소켓 연결(useRoomConnection) · 스토어(Zustand) · 로비
 ┃ ┗ 📂 game          # 게임별 컴포넌트(룰렛·투표·제비뽑기·순서·사다리·풍선)
 ┣ 📂 pages           # 라우트 (Home · HostRoom · GameRoom · JoinRoom · Embed · NotFound)
 ┣ 📂 shared          # lib(clipboard·embed·zoom·meet·mascot) · ui · types
 ┣ 📂 assets
 ┣ 📜 App.tsx · main.tsx · index.css

📂 integrations       # 임베드 껍데기(Thin Shell)
 ┣ 📂 chrome-extension  # MV3 manifest + 사이드 패널
 ┣ 📂 zoom              # Zoom App
 ┗ 📂 google-meet       # Google Meet 애드온
</pre>
</details>

<br />

<a id="team-members"></a>
# 👥 Team Members

<div align="center">
  <table>
    <thead>
      <tr>
        <th align="center">Profile</th>
        <th align="center">Name</th>
        <th align="center">Position</th>
        <th align="center">GitHub</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/1-kimseungjo.jpg" width="80"></td>
        <td align="center"><b>김승조</b></td>
        <td align="center">Mentor · Full Stack · DevOps</td>
        <td align="center"><a href="https://github.com/SeungJo-02"><img src="https://img.shields.io/badge/SeungJo--02-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/2-yubin.png" width="80"></td>
        <td align="center"><b>유빈</b></td>
        <td align="center">Leader · Planning · Survey · Presentation</td>
        <td align="center"><a href="https://github.com/uuuubin"><img src="https://img.shields.io/badge/uuuubin-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/3-wooyedam.png" width="80"></td>
        <td align="center"><b>우예담</b></td>
        <td align="center">Design · Survey · Presentation</td>
        <td align="center"><a href="https://github.com/wooyedamA"><img src="https://img.shields.io/badge/wooyedamA-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/4-baekahjeong.png" width="80"></td>
        <td align="center"><b>백아정</b></td>
        <td align="center">Planning · Survey · Presentation</td>
        <td align="center"><a href="https://github.com/BeakAh-jeong"><img src="https://img.shields.io/badge/BeakAh--jeong-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/5-choiyeonho.png" width="80"></td>
        <td align="center"><b>최연호</b></td>
        <td align="center">Design · QA Automation</td>
        <td align="center"><a href="https://github.com/billy0224002010-glitch"><img src="https://img.shields.io/badge/billy0224002010--glitch-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/6-choisanho.png" width="80"></td>
        <td align="center"><b>최산호</b></td>
        <td align="center">Design · QA Automation</td>
        <td align="center"><a href="https://github.com/a01088802343-prog"><img src="https://img.shields.io/badge/a01088802343--prog-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/7-leedongmin.png" width="80"></td>
        <td align="center"><b>이동민</b></td>
        <td align="center">Planning · Survey</td>
        <td align="center"><a href="https://github.com/LDM-0305"><img src="https://img.shields.io/badge/LDM--0305-181717?style=social&logo=github"/></a></td>
      </tr>
      <tr>
        <td align="center"><img src="https://raw.githubusercontent.com/Project-PickMeNow/.github/main/profile/members/8-gongyuna.png" width="80"></td>
        <td align="center"><b>공윤아</b></td>
        <td align="center">Planning · Survey</td>
        <td align="center"><a href="https://github.com/20101011yuna-crypto"><img src="https://img.shields.io/badge/20101011yuna--crypto-181717?style=social&logo=github"/></a></td>
      </tr>
    </tbody>
  </table>
</div>

<br />
<br />
