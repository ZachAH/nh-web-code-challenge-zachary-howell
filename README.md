# 🏥 Nice Healthcare: Clinician Dispatch Dashboard

[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)

A specialized internal tool designed for healthcare coordinators to efficiently assign clinicians to home visits by calculating optimal round-trip travel distances.

---

## 🚀 Technical Approach

- **Deterministic Logic (Bonus)**: To exceed the requirement for a random distance generator, I implemented the **Haversine Formula**. This ensures consistent, mathematically sound results by calculating the "as-the-crow-flies" distance between geographic coordinates.
- **Loop Logic**:
  - **Standard Visit**: Home → Patient → Home.
  - **Lab Visit**: Home → Patient → Optimal Lab → Home.
- **State Management**: Developed using React hooks with explicit **loading states** to prevent UI flickering, handle async-simulated calculations, and eliminate infinite re-render loops.

---

## 🧠 Assumptions

In the absence of specific product requirements for edge cases, the following engineering decisions were made:

1.  **Optimal Lab Selection**: I assumed the "best" lab is the one that minimizes the **total round-trip** for the clinician (Home → Patient → Lab → Home), rather than simply the lab closest to the patient. This prioritizes the clinician's total time on the road.
2.  **Patient Location**: As no Geocoding API was provided for this assessment, the system currently anchors the patient's coordinates to **Central Minneapolis** (44.9778° N, 93.2650° W) to demonstrate the logic across the provided mock data.

---

## 🛠️ Production Considerations

### 1. MVP Limiting Factors & User Issues
* **Geocoding Strategy**: The current solution relies on mocked patient coordinates. In a production environment, a Geocoding API (e.g., Google Maps, Mapbox) would be integrated to convert user-entered strings into real-time latitude/longitude data.
* **Geographic Impediments**: Haversine measures direct distance. A production-ready app must account for actual road networks, traffic congestion, and physical barriers (like the Mississippi River) that significantly impact drive time in the Twin Cities.
* **Data Architecture**: Currently, data is stored in static mock files. For scaling to a national provider level, this would require a backend with spatial indexing (e.g., PostGIS) and API-driven data fetching.

### 2. Optimization Factors (Future Roadmap)
* **Clinician Specialty Matching**: Aligning specific patient needs (e.g., pediatric expertise) with provider credentials.
* **Load Balancing**: Factoring in a clinician's existing daily workload to prevent provider burnout, even if they are geographically the closest.
* **Shift Management**: Cross-referencing route duration with remaining shift hours to avoid unauthorized overtime.
* **Predictive Routing**: Utilizing live traffic APIs to optimize for **Estimated Time of Arrival (ETA)** rather than just physical mileage.

---

## 📦 Installation & Setup

1. **Clone and Install**:
   ```bash
   npm install
