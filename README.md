# StreakUp — Focus & Productivity Tracker

Cross-platform mobile application for structured study sessions, task management, and peer motivation. Built with **Flutter** and **Firebase** — featuring real-time group leaderboards, background Pomodoro tracking, and daily streak mechanics.

---

## Screenshots

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/00c3c2ad-b4cb-4cb1-9148-e1b340432f6b" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/3316fced-e02c-4ec2-a203-0f295e306f86" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/6abcc63b-70ec-4fd5-bafe-9e683c3405be" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/2dbff529-3510-4cb1-beae-7deb764f3d28" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/9d973f74-b210-4d15-ba81-6018516bb76e" width="180" /></td>
  </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/76c0bd58-13cd-45ad-aef4-900bda425a35" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/591ae2e9-ceff-4fe7-a147-f9366df3ded1" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/79d369ca-919b-4b56-8cda-0ce8e88bbfbf" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/436f5360-1e0e-4244-9884-ad23bd4ad4bc" width="180" /></td>
    <td><img src="https://github.com/user-attachments/assets/9eb72846-51a3-4fc7-b6a4-f599f1eb5478" width="180" /></td>
  </tr>
</table>

---

## UI/UX Design & Prototyping (Figma)

Prior to writing any code, high-fidelity prototypes and a cohesive design system were established in Figma to ensure a consistent interface layout, smooth navigation flow, and structured Material Design 3 implementation.

### High-Fidelity Wireframes & User Flows
<img src="https://github.com/user-attachments/assets/67fe151b-9c1d-44ca-a262-e5efb0e59a89" width="100%" alt="Figma User Flow" />
<img src="https://github.com/user-attachments/assets/e6fc8162-ddf4-4c70-9360-6e1f0cbb3c58" width="100%" alt="Figma User Flow" />

### Material 3 Component & Asset Design
<img src="https://github.com/user-attachments/assets/e82d480d-600f-4f82-b200-4a9167d879f7" width="100%" alt="Figma Design System" />


---

## Technical Implementation

### State Management (Provider)
- **Reactive UI Architecture** — All application state (timer, tasks, user session, group data, theme) managed through `ChangeNotifier` providers. Widgets rebuild only when their specific dependencies change, avoiding unnecessary redraws.
- **Separation of Business Logic** — Timer logic, streak calculation, and leaderboard aggregation live in dedicated provider classes. UI layer consumes state; it never mutates it directly.

### Real-Time Backend (Firebase)
- **Cloud Firestore** — Real-time document listeners for group leaderboards and shared task boards. Changes by any group member propagate to all connected clients within milliseconds via Firestore's `snapshots()` streams.
- **Authentication Flow** — Email/password auth with persistent sessions via `FirebaseAuth.instance.authStateChanges()`. Session state drives the entire navigation graph.
- **Data Modeling** — Normalized Firestore collections (`users`, `groups`, `tasks`, `sessions`) with document references for relational queries. Group membership resolved through subcollections to minimize read costs.

### Background Timer Processing
- **Foreground Service** — Pomodoro timer continues running when the app is minimized or the screen is locked. Uses `flutter_local_notifications` to maintain a persistent foreground notification with live countdown.
- **State Persistence** — Timer start time and remaining duration written to `SharedPreferences` on every tick. If the OS kills the process, the timer reconstructs its state from the last saved timestamp on relaunch — no lost sessions.

### Architecture & UX
- **Material Design 3** — Full M3 component library with dynamic color theming. Light and dark mode toggle persisted across sessions.
- **Group System** — Invite-code-based group creation and joining. Leaderboard computed server-side from aggregated session durations, ranked in real time.
- **Streak Engine** — Daily streak counter incremented on first completed Pomodoro of the day. Reset logic checks calendar date boundaries, not 24-hour windows.

---

## Firebase Schema

<img src="https://github.com/user-attachments/assets/40e790be-81b1-4f50-8303-3a979fefda9f" width="100%" alt="Firebase Schema Diagram" />

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Flutter 3.24+ |
| Language | Dart |
| State Management | Provider (ChangeNotifier) |
| Backend | Firebase (Auth + Cloud Firestore) |
| Local Storage | SharedPreferences |
| Notifications | flutter_local_notifications |
| UI System | Material Design 3 |
| Design | Figma |
| Version Control | Git / GitHub |

---

## Documentation

| Document | Description |
|---|---|
| Technical Requirements | Data models, algorithms, test strategy | [`docs/tr/TECHNICAL_REQUIREMENTS.md`](docs/tr/TECHNICAL_REQUIREMENTS.md) |
| Design Document | UI/UX guidelines and color palette | [`docs/tr/DESIGN_DOCUMENT.md`](docs/tr/DESIGN_DOCUMENT.md) |
| Development Roadmap | 8-week sprint plan | [`docs/tr/DEVELOPMENT_ROADMAP.md`](docs/tr/DEVELOPMENT_ROADMAP.md) |

---

## Academic Context

Developed as a capstone project for the Mobile Programming course at **Necmettin Erbakan University**, Department of Computer Engineering.

- **Advisor:** Prof. Dr. Mehmet Hacıbeyoğlu
- **Timeline:** 8 weeks, solo development
- **Platform:** Android (API 21+)
