# WeltNexus — Field Work: Drone Image to 3D Building Model

> **Smart India Hackathon 2026** · Problem Statement **SIH26011** — *3D ULPIN Generation and Vertical Property Mapping System*
> **Team:** Neural@Ninjas (Team ID 178769)

This repository documents our real-world field trial: capturing a residential building with a drone and converting the imagery into a measurable 3D model. The trial validates the first stage of the WeltNexus pipeline — **drone imagery → 3D mesh → building height** — on real data, not simulated data.

---

## Key Results

| Metric | Result |
|---|---|
| Drone images captured | **120** |
| Processing time (images → 3D model) | **~30 minutes** |
| Building height error | **±10 cm** |
| Published benchmark for drone photogrammetry | 10–15 cm (compared against LiDAR) |
| Outputs | Point cloud, textured 3D mesh, orthophoto, DSM, DTM |

**How height error was measured:** `[ADD METHOD — e.g., model height compared with tape / laser-distance measurement of the actual building]`

---

## Objective

1. Prove that a building can be reconstructed in 3D from consumer-accessible drone imagery using open-source tools.
2. Measure how accurately building height can be derived from the model (nDSM = DSM − DTM).
3. Produce a real dataset to feed into the WeltNexus 3D ULPIN prototype.

---

## Field Work Process

### 1. Drone access
We requested drone equipment and imagery support from the **AICTE–AVPL Aero Vision Lab, Centre of Excellence for Drones**.

### 2. Data capture
| Parameter | Value |
|---|---|
| Location | Coimbatore, Tamil Nadu |
| Date of flight | `[ADD DATE]` |
| Drone model | `[ADD MODEL]` |
| Camera | `[ADD CAMERA / SENSOR]` |
| Flight altitude | `[ADD — metres AGL]` |
| Flight pattern | `[ADD — e.g., grid + orbit / oblique]` |
| Image overlap | `[ADD — e.g., 75% front / 65% side]` |
| Ground Sampling Distance | `[ADD — cm/pixel, from ODM report]` |
| Ground Control Points | `[ADD — number used, or "none"]` |

Flights were carried out within permitted airspace under the Drone Rules, 2021. `[CONFIRM zone — green/yellow — from the Digital Sky airspace map]`

### 3. Processing pipeline

```
120 drone images
      │
      ▼
OpenDroneMap (ODM)  ── structure-from-motion + dense matching
      │
      ├── Point cloud (LAS/LAZ)
      ├── Textured 3D mesh
      ├── Orthophoto
      └── DSM + DTM
              │
              ▼
      nDSM = DSM − DTM  →  building height
```

| Step | Tool |
|---|---|
| Photogrammetry & 3D reconstruction | OpenDroneMap |
| Point-cloud processing | PDAL |
| Visualisation | CesiumJS (web prototype) |

**Hardware used for processing:** `[ADD CPU / RAM / GPU]`

### 4. Exterior and interior models
- **Exterior model:** generated automatically from drone imagery with OpenDroneMap.
- **Interior model:** `[STATE HOW IT WAS CREATED — e.g., modelled from the building's floor plan in Blender / captured by phone scan]`

> Drones capture only the outer shell of a building. Interior layouts in WeltNexus come from building plans and are validated against the drone-derived 3D shell.

---

## Repository Structure

```
fieldwork/
├── README.md
├── images/          # sample drone images (full set: see Data Access)
├── outputs/
│   ├── orthophoto/
│   ├── dsm_dtm/
│   ├── pointcloud/
│   └── mesh/
├── reports/         # ODM processing report
└── screenshots/     # field photos and model previews
```

`[EDIT to match your actual folders]`

---

## Links

| Resource | Link |
|---|---|
| Live prototype | https://weltnexus-flax.vercel.app/login |
| Exterior 3D model | `https://snihaal2006.github.io/3D-ULPIN-Cadastre/` |
| Interior 3D model | `[ADD LINK]` |
| Demo video | `[ADD LINK]` |

---

## Limitations

- **Single building.** Results come from one residential building; accuracy on tall or densely packed buildings has not yet been tested.
- **Height accuracy depends on setup.** Error is expected to grow with building height and occlusion; RTK positioning and ground control points should reduce it to roughly 3–5 cm.
- **No interior capture from drones.** Unit boundaries must come from building plans or on-site verification.

## Next Steps

- [ ] Survey a multi-storey apartment building
- [ ] Add ground control points / RTK for higher accuracy
- [ ] Run Mask R-CNN footprint extraction on our own orthophoto and report IoU
- [ ] Measure processing time and cost per sq km

---

## Privacy

The surveyed building belongs to a team member. Exact coordinates and address are intentionally **not** published. Faces and neighbouring properties should be blurred in any shared imagery.

---

## Team — Neural@Ninjas

| Member | Role |
|---|---|
| Dharun Kumar | `TEAM LEADER` |
| Thanga Prakash | `TEAM member` |
| Sivasangar | `TEAM member` |
| Sanjeevi Kumar | `TEAM member` |
| Tarunika | `TEAM member` |
| Nihaal | `TEAM member` |

## Acknowledgements

- **AICTE–AVPL Aero Vision Lab, Centre of Excellence for Drones** — drone equipment and support
- **OpenDroneMap** — open-source photogrammetry
