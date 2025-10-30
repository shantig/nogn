# README.md

# 🧠 Nogn: Turn any room into a game

**Author:** Shant Donabedian | w0899687@student.hccs.edu

**Due Dates:** Midterm – Oct 30 | Final – Dec 4

---

## 💎 Project Tier

**Tier:** 3

**Difficulty:** ⭐️⭐️⭐️⭐️⭐️

**Time:** Very significant

**Resources:** Creative use of free datasets + commodity hardware

**Why Tier 3:** Real‑time multi‑object tracking, projector calibration, and on‑edge deployment hurdles.

---

## 🤷🏻 Problem Statement

Kids need physical play and social interaction. Parents want less “glued‑to‑glass” time without losing the magic of interactive worlds. Current AR systems either require headsets (friction) or screens (sedentary), leaving a gap for room‑scale, hands‑free play.

---

## 🧩 Solution Overview

**Nogn** is a projection‑mapped playground. A camera watches the floor/walls; computer vision detects players, props, or markers; a projector draws the game world directly onto the room. Think air‑hockey lines, lily pads, enemy zones, scoreboards—no goggles, no controllers.

Core loop: **see → understand → project → react** within a tight latency budget so actions feel instant.

---

## ⚙️ Technical Approach

**Perception**
- **CV Technique:** Real‑time object detection (players/balls/hand‑held props) + ID‑consistent multi‑object tracking. ArUco markers for absolute reference and homography.
- **Model:** Ultralytics **YOLOv11‑nano** (quantized) for detection; **ByteTrack** for MOT; **ArUco** for calibration.
- **Frameworks:** PyTorch + Ultralytics, OpenCV (ArUco, homography), HailoRT SDK.
- **Why this approach:** YOLOv11‑nano is small and fast; ByteTrack preserves identities without heavy re‑ID models; ArUco yields robust projector↔︎camera alignment.

**Projection & Calibration**
- Single DLP pico projector (DLPDLCR230NPEVM).
- Printed ArUco board and 4‑point interactive calibration to compute **camera→projector** homography.
- Continuous drift correction by re‑observing fixed room markers.

**Runtime Targets**
- End‑to‑end latency (camera→projector): **≤ 50 ms** at 720p.
- Spatial projection error: **≤ 1.5 cm** at center, **≤ 3 cm** at edges after correction.

**Deliverables**
- `notebooks/04_demo.ipynb` — inference + visualization walkthrough
- `src/nogn/runtime.py` — real‑time loop (capture → detect/track → project)
- `calibration/` — printable ArUco board + scripts

| Component | Choice |
| --- | --- |
| Detector | YOLOv11‑nano (Ultralytics) |
| Tracker | ByteTrack |
| Markers | ArUco (OpenCV) |
| Framework | PyTorch, OpenCV |
| Accelerator | Raspberry Pi **AI HAT+** (Hailo, 26 TOPS) |
| Output | Real‑time projection + notebook demo |

---

## 📊 Dataset

- **Strategy:** Start **zero‑shot** with common classes (person/ball). For game props (custom tokens), collect a **small, focused dataset**: ~**800–1200 images** from the target room at multiple lighting angles.
- **Acquisition:** Phone video → frame extraction at 5–10 fps; staged poses of props; optionally synthetic renders for rare views.
- **Labeling:** Roboflow or CVAT. Split **70/20/10** (train/val/test). Export **YOLO** format with `data.yaml`.
- **Augmentations:** Random brightness/contrast, blur, small perspective warps; avoid heavy crops that harm projection alignment.

---

## 🏆 Success Metrics

**Primary**
- **mAP50** (props + ball + player feet) ≥ **0.80** on held‑out test set.

**Secondary (experience)**
- **Latency** ≤ **50 ms** camera→projector pipeline.
- **Tracking stability:** **ID switches < 1 per 30 s** of play with 2–3 actors.
- **Projection error:** median **≤ 1.5 cm** at center.

Pass/fail for playability: children can complete a 60‑second mini‑game without missed hits due to system lag or drift.

---

## 📅 Week‑by‑Week Plan

| Week | Task | Deliverable |
| --- | --- | --- |
| 9 | Planning & hardware mounts | Repo scaffold, projector/camera mounted |
| 10 | Midterm proposal | Slides + updated README |
| 11 | Data collection & labeling | v1 dataset + `data.yaml` |
| 12 | Model training & export | Weights + Hailo‑compiled artifact |
| 13 | Runtime + calibration | Real‑time loop + drift correction |
| 14 | Game polish | 2 mini‑games (targets, zones) + video |
| 15 | Presentation | Live demo + final submission |

---

## 💸 Resources Needed

**Compute:** Raspberry Pi 5 + Raspberry Pi **AI HAT+** accelerator (Hailo).

**Optics:** **TI DLPDLCR230NPEVM** pico projector (~100 lm), **Raspberry Pi Camera Module 3**.

**Power (projector):** 5 VDC ≥ 4 A via 5.5×2.5 mm barrel (separate PSU).

**Mounting:** Simple ceiling/boom mount + printable ArUco board.

**APIs/Libraries:** Ultralytics, OpenCV, HailoRT, NumPy, PyTorch.

**Budget:** $$–$$$ (projector already purchased).

**Hardware Source of Truth:** Notion → *Nogn Midterm Project → Inventory/Hardware*.

---

## 😈 Risks & Mitigation

| Risk | Probability | Impact | Mitigation |
| --- | --- | --- | --- |
| Low light / motion blur | M | H | Faster shutter + more light; denoise; 720p@60fps |
| Calibration drift over time | M | M | Persistent ArUco anchors; periodic auto‑recal |
| Occlusion between players & props | M | M | Tracker with motion model; larger markers; game rules minimizing overlap |
| Hailo compile/ops incompatibility | L | M | Keep to supported ops; export via ONNX; have CPU fallback |
| Projector keystone distortion edges | M | M | Over‑sample border; per‑cell warp grid |
| Latency spikes on Pi I/O | M | M | Pre‑allocate buffers; pin threads; reduce copies |

---

## 🚀 Getting Started

**1) Setup**

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

**2) Calibrate**

```bash
python -m nogn.calibrate --print-boardpython -m nogn.calibrate --capturepython -m nogn.calibrate --solve --save ./calibration/homography.json
```

**3) Run demo**

```bash
python -m nogn.runtime \\
  --weights ./models/yolo11n.onnx \\
  --cal ./calibration/homography.json \\
  --camera rpicam

```

---

## 🧠 AI Usage Log (Summary)

Document all AI assistance in `/docs/AI_usage_log.md` — target **5–10 entries** describing prompts, outputs, and edits.

---

## 🧿 Current Status

- [x]  Repository created
- [x]  Proposal written
- [ ]  Dataset acquired
- [ ]  Model training started
- [ ]  Demo created
- [ ]  Final presentation ready

---

## 🧾 License

MIT License © 2025 Shant Donabedian
