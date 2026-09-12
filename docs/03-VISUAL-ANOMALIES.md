# 03 — Visual Language, Entropy & Cosmic Anomalies

## 1. Art direction

Void Weaver cần đẹp theo hướng:

- deep-space, tối và có chiều sâu,
- tím / xanh / trắng / cyan thiên về emissive,
- ánh sáng không quá neon-cyberpunk,
- nhiều khoảng tối để bloom có chỗ thở,
- chuyển động chậm, mềm và có quán tính,
- cosmic nhưng **sống** và hơi bất thường.

Từ khoá: **cosmic, ethereal, living nebula, gravitational distortion, sacred geometry, bioluminescent space, strange beauty**.

## 2. Scene layers

```text
Void Weaver Scene
├── Deep Background
│   ├── distant starfield
│   ├── parallax dust
│   └── faint nebula volume
├── Main Galaxy
│   ├── core glow
│   ├── spiral particles
│   ├── dust lanes
│   └── orbiting debris
├── Dynamic Objects
│   ├── stars
│   ├── planets
│   ├── black holes
│   ├── portals
│   └── entities
└── Screen / FX Layer
    ├── bloom
    ├── trails
    ├── shockwave
    ├── distortion
    └── subtle chromatic split
```

## 3. Entropy / Strangeness system

Universe có một chỉ số `entropy` từ 0 đến 100.

Entropy tăng khi người dùng:

- tạo black hole,
- supernova liên tục,
- bẻ cong galaxy quá mạnh,
- mở portal,
- ép vật chất vượt ngưỡng ổn định,
- triệu hồi entity.

Entropy không chỉ là UI meter; nó điều khiển toàn scene.

### 0–20 — Stable Cosmos

- màu sắc sạch,
- orbit ổn định,
- nebula nhẹ,
- ít distortion.

### 20–40 — Subtle Anomaly

- star flicker bất thường,
- dust chuyển động như đang thở,
- một số constellation tự tái cấu trúc.

### 40–60 — Living Universe

- Living Planet pulse,
- Eye Nebula có thể xuất hiện,
- whispering star layer trong audio,
- orbit có sai lệch nhỏ.

### 60–80 — Corrupted Cosmos

- black-hole lensing rõ hơn,
- màu galaxy bắt đầu chuyển bất thường,
- portal tự flicker,
- Void Serpent / Parasite Moon có thể spawn.

### 80–100 — Unstable Reality

- gravity field méo mạnh,
- star trails kéo dài bất thường,
- constellation “nhìn” về phía người dùng,
- scene chuẩn bị collapse,
- entity lớn có xác suất xuất hiện.

## 4. Cosmic anomalies

### Eye Nebula

Một nebula khổng lồ dần tổ chức thành hình con mắt.

Behavior:
- pupil theo palm hoặc camera cursor,
- blink chậm,
- khi người dùng nắm tay, pupil co lại,
- khi entropy cao, eye có thể xuất hiện ở nhiều lớp depth.

Implementation:
- procedural nebula particles,
- billboard/sphere cho iris,
- shader noise + fresnel,
- gaze direction từ gesture cursor.

### Living Planet

Một hành tinh có nhịp pulse như sinh vật.

Behavior:
- emissive pulse,
- surface displacement theo nhịp,
- co nhẹ khi hand cursor tiến gần,
- phát “vein light” dọc bề mặt.

### Void Mouth

Black hole có cảm giác giống một cấu trúc hữu cơ mở ra trong không gian.

Không cần tạo literal mouth. Chỉ cần:
- asymmetric accretion disk,
- rim co giãn,
- gravitational distortion,
- dark center có shape biến đổi rất nhẹ.

### Broken Constellation

Các star node nối bằng line, sau đó tự đứt và tái cấu trúc thành hình sinh vật hoặc biểu tượng không rõ nghĩa.

### Parasite Moon

Một moon nhỏ bám vào planet và hút emissive energy.

Visual:
- tendril/energy arcs,
- planet bị tối dần,
- moon sáng lên.

### Time Echo

Gesture mạnh để lại “dư ảnh thời gian” trong không gian.

Ví dụ một cú swipe để lại hàng loạt silhouette particle ribbon của chính quỹ đạo bàn tay.

### Gravity Tear

Một vết rách dạng đường cong trong space.

- background bị refract,
- particles gần đó bị hút lệch,
- có thể mở rộng thành portal.

## 5. Major cosmic events

### Supernova

Phải có 3 phase:

1. charge — star sáng và co lại,
2. flash — white-hot burst,
3. aftermath — shell + nebula + debris.

### Big Crunch

- toàn bộ orbit mất ổn định,
- particle spiral vào tâm,
- âm thanh low-frequency tăng,
- scene exposure tăng ngắn rồi tụt về đen,
- còn lại một singularity point.

### Rebirth

- singularity pulse,
- shockwave mở rộng,
- star seed scatter,
- galaxy mới hình thành từ seed khác.

## 6. Post-processing rules

Bloom rất quan trọng nhưng phải kiểm soát:

- chỉ emissive object đủ threshold mới bloom,
- background không được wash-out,
- chromatic aberration chỉ dùng nhẹ hoặc khi entropy cao,
- noise/grain cực ít,
- motion trail ưu tiên entity/gesture, không blur toàn màn hình.

## 7. UI

UI nên tối thiểu.

Có thể chỉ gồm:

- camera permission / calibration,
- entropy indicator rất nhỏ,
- current gesture hint khi cần,
- screenshot button,
- debug toggle.

Không nên để panel HUD lớn phá trải nghiệm cosmic.

## 8. Visual success criteria

Một screenshot đứng yên của Void Weaver vẫn phải đủ đẹp để dùng làm artwork. Nếu scene chỉ đẹp khi chuyển động nhưng ảnh tĩnh trông rỗng, art direction chưa đủ mạnh.