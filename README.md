# 🧠 Nogn: Turn any room into a game.
**Author:** Shant Donabedian | w0899687@student.hccs.edu 
**Due Dates:** Midterm – Oct 30 | Final – Dec 4  

---

## 💎 Project Tier
**Tier:** 2 or 3 likely
**Difficulty:** ⭐️⭐️⭐️⭐️⭐️
**Time:** Very Significant 
**Resources:** Creative use of free resources + Hardware 
**Why Tier 3:** Real-time multi-object tracking and engineering challenges

---

## 🤷🏻 Problem Statement
Kids want to have fun and crave to be active!
Parents are done with "glued-to-glass" time in a hyper-connected untrustworthy world.

---

## 🧩 Solution Overview
Nogn explores how embedded vision systems can enhance real-world interaction through projection and computer vision.

/*
The project aims to [your proposed solution: detection, classification, or generative task], using open-source datasets and pretrained models such as YOLOv8, BLIP, or custom fine-tuning.
*/

---

## ⚙️ Technical Approach
/*
Specify:

- **CV Technique:** Object detection? Classification? Segmentation? VLM?
- **Model:** YOLOv8? ResNet? CLIP? LLaVA?
- **Framework:** PyTorch? TensorFlow? Hugging Face?
- **Why this approach?** (1-2 sentences)
*/

| Component | Description |
|------------|-------------|
| Model | YOLOv11-nano / ByteTrack / [ArUco] |
| Framework | PyTorch |
| Dataset | Zero Shot |
| Environment | Hailo-8 |
| Output | Inference + Visualization Notebook (`04_demo.ipynb`) |

---

## 📊 Dataset
/*
- **Source:** Where will you get images/videos?
    - Public dataset? (COCO, ImageNet, Roboflow)
    - Collect your own? (Phone camera? Web scraping?)
    - Synthetic data?
- **Size:** How many images? (100? 1000? 10,000?)
- **Labels:** Do you need to label it? How?
*/

- Source dataset from Roboflow, Kaggle, or Hugging Face.  
- Clean, augment, and split data into `train`, `val`, and `test` subsets.  
- Use `data.yaml` for YOLO-compatible projects.  

---

## 🏆 Success Metrics
/*
Primary Metric: [Accuracy / mAP / F1-score / etc.] Target: [e.g., "90% accuracy"]
Secondary Metrics: [Speed, etc.]
*/

---

## 📅 Week-by-Week Plan
| Week | Task | Deliverable |
|------|------|-------------|
| 9 | Planning | Dataset + repo setup |
| 10 | Midterm proposal | Slides + README |
| 11–13 | Implementation | Working model |
| 14 | Demo polish | Final testing + video |
| 15 | Presentation | Live demo + final submission |

---

## 💸 Resources Needed
**Compute:** Hailo-8
**Cost:** $$$
**APIs:** ??

---

## 😈 Risks & Mitigation
| Risk | Probability | Mitigatioon |
|------|-------------|-------------|
| 1 | H/M/L | Plan B |

---

## 🧠 AI Usage Log (Summary)
Document all AI assistance in `/docs/AI_usage_log.md` — at least **5–10 entries** describing what was generated, modified, or debugged.

---

## 🧿 Current Status
✅ Repository created
✅ Proposal written
☑️ Dataset acquired
☑️ Model training started
☑️ Demo created
☑️ Final presentation ready

---

## 🧾 License
MIT License © 2025 Shant Donabedian
