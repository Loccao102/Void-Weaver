# Void Weaver

> **Sculpt a living cosmos with your hands.**

**Void Weaver** là một interactive 3D web experience dùng webcam và hand tracking để biến hai bàn tay của người dùng thành công cụ kiến tạo vũ trụ.

Người chơi không điều khiển một nhân vật. Họ trực tiếp **kéo giãn, bóp méo, sinh ra, làm biến dị và phá huỷ một vũ trụ sống** bằng cử chỉ tay.

Project được định hướng như một **cosmic digital toy / interactive art sandbox**: không cần thắng thua, không cần quest phức tạp, mục tiêu chính là tạo cảm giác *“mình đang chạm vào một thứ gì đó sống, đẹp và hơi cấm kỵ.”*

## Core fantasy

- Hai tay kéo ra → vũ trụ giãn nở.
- Hai tay chụm vào → vật chất sụp về singularity.
- Xoay cổ tay → bẻ cong spiral arms và quỹ đạo.
- Nắm tay → tạo black hole.
- Xòe tay mạnh → supernova.
- Chỉ tay → gieo một ngôi sao mới.
- Tạo vòng bằng hai tay → mở cosmic portal.
- Tăng entropy → triệu hồi những anomaly và cosmic entity kỳ lạ.

## Project pillars

1. **Immediate interaction** — mở webcam và có thể nghịch ngay.
2. **Cosmic beauty** — galaxy, nebula, particle, shader, glow và procedural motion.
3. **Strange universe** — vũ trụ càng bị tác động càng trở nên sống và dị thường.
4. **Procedural first** — ưu tiên shader, particles và procedural geometry thay vì phụ thuộc vào nhiều model nặng.
5. **Toy, not a chore** — trải nghiệm phải vui để nghịch, không biến thành một game phải cày.

## Documentation

- [`docs/01-CONCEPT.md`](docs/01-CONCEPT.md) — vision, core loop, experience flow và identity của Void Weaver.
- [`docs/02-INTERACTION-GESTURES.md`](docs/02-INTERACTION-GESTURES.md) — gesture vocabulary và mapping cử chỉ → cosmic action.
- [`docs/03-VISUAL-ANOMALIES.md`](docs/03-VISUAL-ANOMALIES.md) — visual language, entropy system và cosmic anomalies.
- [`docs/04-3D-ASSET-STRATEGY.md`](docs/04-3D-ASSET-STRATEGY.md) — cách tạo galaxy, black hole, planet, portal và creature 3D hiệu quả.
- [`docs/05-TECHNICAL-ARCHITECTURE.md`](docs/05-TECHNICAL-ARCHITECTURE.md) — kiến trúc kỹ thuật dự kiến cho web realtime.
- [`docs/06-ROADMAP.md`](docs/06-ROADMAP.md) — MVP → Strange Cosmos → Living Universe.
- [`docs/07-COSMIC-ENTITY-BIBLE.md`](docs/07-COSMIC-ENTITY-BIBLE.md) — bộ creature/anomaly và quy tắc thiết kế để giữ art direction đồng nhất.

## Suggested stack

- React + TypeScript + Vite
- Three.js / React Three Fiber
- `@react-three/drei`
- MediaPipe Hand Landmarker
- Zustand
- GLSL custom shaders
- Three.js postprocessing / React Three Postprocessing
- Web Audio API hoặc Tone.js cho reactive ambience
- Blender + GLB chỉ cho các entity cần silhouette/model riêng

## One-line pitch

**Void Weaver is a webcam-driven cosmic sandbox where your hands sculpt, corrupt, collapse and rebirth a procedural living universe.**

---

This repository is intentionally documentation-first. The first goal is to lock the interaction fantasy and visual language before turning it into code.