# 06 — Development Roadmap

## Phase 0 — Visual proof

Mục tiêu: chứng minh rằng chỉ riêng galaxy đã đủ đẹp để tiếp tục.

Deliverables:

- deep-space background,
- procedural spiral galaxy,
- bloom,
- basic camera motion,
- 1–2 palette preset,
- stable 60 FPS trên máy dev.

Không webcam ở phase này.

Success criteria:

> Screenshot scene tĩnh đã đủ đẹp để dùng làm cover image.

---

## Phase 1 — Hand-driven galaxy MVP

Mục tiêu: tạo phiên bản đầu tiên thực sự “chơi được”.

### Features

- webcam permission,
- MediaPipe hand tracking,
- smoothing,
- 2-hand expand/collapse,
- point → seed star,
- fist → black-hole seed,
- hand energy trail,
- subtle reactive audio.

### Definition of done

Người dùng mới mở app có thể tự khám phá interaction chính mà không cần tutorial dài.

---

## Phase 2 — Cosmic material & black-hole polish

Mục tiêu: làm interaction trông không còn như tech demo.

### Features

- reusable Cosmic Material System,
- accretion disk,
- pseudo gravitational lensing,
- star/debris attraction,
- better particle trails,
- supernova event,
- gesture charge/release feedback.

### Focus

Ít feature nhưng phải thật đẹp.

---

## Phase 3 — Strange Cosmos

Mục tiêu: tạo bản sắc riêng cho Void Weaver.

### Features

- entropy 0–100,
- entropy-driven palette/distortion,
- Eye Nebula,
- Living Planet,
- Broken Constellation,
- Time Echo,
- Gravity Tear,
- reactive ambient audio layers.

### Definition of done

Sau vài phút nghịch, scene phải thay đổi rõ rệt từ “beautiful galaxy” sang “living strange cosmos”.

---

## Phase 4 — Portal & first entity

Mục tiêu: có khoảnh khắc wow lớn đầu tiên.

### Features

- two-hand portal gesture,
- procedural portal,
- render-texture hoặc distorted inner-space effect,
- first hero entity: **Star Whale**,
- entity entrance/exit sequence,
- entity reacts subtly to hand position.

### Star Whale scope

Không làm hệ AI phức tạp.

Chỉ cần:

- đi xuyên portal,
- bơi theo spline,
- glow/constellation veins,
- stardust trail,
- nhìn hoặc đổi hướng nhẹ theo gesture cursor.

---

## Phase 5 — Collapse & Rebirth

Mục tiêu: hoàn thành một vòng trải nghiệm.

### Features

- unstable state ở entropy cao,
- Big Crunch sequence,
- singularity,
- universe rebirth,
- procedural universe seed,
- palette/branch/density variation.

### Definition of done

Một session có mở đầu, escalation, cosmic event và kết thúc/rebirth tự nhiên mà vẫn không biến thành game tuyến tính.

---

## Phase 6 — Content expansion

Chỉ làm sau khi loop chính thật sự vui.

Possible additions:

- Void Serpent,
- Cosmic Jellyfish,
- Parasite Moon,
- Ancient Relic,
- multiple galaxy archetypes,
- universe mutation presets,
- screenshot mode,
- shareable seed,
- hidden gestures / easter eggs.

---

## Optional future phase

Không nằm trong core scope nhưng có thể cân nhắc sau:

- WebXR,
- two-player shared cosmos,
- saved universe gallery,
- generative ambient soundtrack,
- mobile hand interaction,
- Leap Motion / depth-camera input,
- installation/kiosk mode.

---

# Suggested 7-day prototype sprint

## Day 1

- setup React + R3F,
- camera,
- starfield,
- basic spiral galaxy.

## Day 2

- improve particle distribution,
- shader color/size/twinkle,
- bloom,
- polish composition.

## Day 3

- webcam,
- MediaPipe,
- hand landmark smoothing,
- debug overlay.

## Day 4

- 2-hand expand/collapse,
- pointing cursor,
- hand energy trails.

## Day 5

- black-hole prototype,
- fist gesture,
- particle attraction,
- distortion experiment.

## Day 6

- entropy prototype,
- one anomaly: Eye Nebula hoặc Living Planet,
- simple reactive audio.

## Day 7

- polish transitions,
- performance pass,
- camera calibration UX,
- record first demo.

---

# Scope rule

Nếu một feature mới không làm một trong ba thứ sau tốt hơn, hãy trì hoãn nó:

1. cảm giác điều khiển bằng tay,
2. vẻ đẹp cosmic,
3. sự kỳ lạ/sống động của universe.

Void Weaver không cần nhiều feature. Nó cần **một vài interaction thật sự đã tay và một scene khiến người ta muốn nghịch tiếp**.