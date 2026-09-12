# 02 — Interaction & Gesture System

## 1. Mục tiêu

Gesture system phải tạo cảm giác **continuous control** thay vì biến bàn tay thành một tập nút bấm.

Mỗi gesture có thể có 3 lớp dữ liệu:

- **Pose** — tay đang ở trạng thái gì.
- **Motion** — tay đang di chuyển theo hướng/tốc độ nào.
- **Relationship** — khoảng cách và tương quan giữa hai tay.

## 2. Gesture vocabulary

| Gesture | Cosmic action | Tham số liên tục |
|---|---|---|
| Hai tay kéo ra | Expand Universe | khoảng cách hai tay → expansion factor |
| Hai tay chụm vào | Collapse Matter | tốc độ chụm → collapse strength |
| Xoay cổ tay | Twist Spiral | góc xoay → spiral twist |
| Nắm tay | Create/charge Black Hole | thời gian giữ → gravity strength |
| Xòe tay nhanh | Supernova Burst | vận tốc mở tay → shockwave power |
| Chỉ bằng ngón trỏ | Seed Star | vị trí đầu ngón → spawn point |
| Pinch | Grab cosmic object | pinch distance → grab/release |
| Pinch + drag | Move object | trajectory → object position |
| Hai tay tạo vòng | Open Portal | kích thước vòng → portal radius |
| Dang rộng hai tay và giữ | Summon Entity | hold duration → summon charge |
| Swipe ngang | Shift cosmic layer | velocity → layer impulse |
| Hai lòng bàn tay hướng vào nhau | Compress field | palm distance → pressure |

## 3. Gesture states

Mỗi action nên có state machine đơn giản:

```text
Idle
  ↓
Candidate
  ↓
Recognized
  ↓
Active
  ↓
Release / Cooldown
```

Ví dụ với `Create Black Hole`:

```text
Open hand
  ↓
Fist detected for 250 ms
  ↓
Black-hole seed appears
  ↓
Keep fist closed → gravity grows
  ↓
Open hand → lock current strength / release event
```

Cách này giúp giảm trigger nhầm do landmark rung.

## 4. Spatial mapping

### 2D webcam → 3D world

Không nên map thẳng pixel camera sang world coordinate. Dùng một **interaction plane** nằm trước camera 3D:

```text
Webcam landmark
    ↓ normalize [0..1]
Interaction plane
    ↓ ray/project
World target
```

Ngón trỏ hoặc palm center có thể điều khiển một invisible 3D cursor.

### Depth giả lập

Nếu không có depth camera, có thể suy ra độ gần/xa tương đối bằng:

- kích thước bàn tay trên frame,
- khoảng cách giữa các landmark,
- tốc độ thay đổi scale của bàn tay.

Depth này chỉ nên dùng như input nghệ thuật, không coi là khoảng cách vật lý chính xác.

## 5. Smoothing

Hand landmark thô sẽ rung. Cần smoothing trước khi đưa vào scene.

Gợi ý:

- exponential smoothing,
- lerp theo frame,
- One Euro Filter cho input nhạy,
- hysteresis cho gesture threshold.

Pseudo flow:

```text
Raw landmarks
  ↓
Normalize
  ↓
Smooth
  ↓
Feature extraction
  ↓
Gesture classifier
  ↓
Gesture state machine
  ↓
Cosmic event bus
```

## 6. Gesture event model

Ví dụ event API nội bộ:

```ts
type GestureEvent = {
  type: 'expand' | 'collapse' | 'fist' | 'point' | 'pinch' | 'portal';
  hand: 'left' | 'right' | 'both';
  confidence: number;
  position?: [number, number, number];
  velocity?: [number, number, number];
  strength?: number;
};
```

Các hệ thống Three.js không cần biết MediaPipe hoạt động ra sao. Chúng chỉ nghe event hoặc đọc gesture state.

## 7. Visual feedback cho hand tracking

Không nên vẽ skeleton MediaPipe mặc định trong trải nghiệm final.

Thay vào đó dùng:

- subtle star particles tại fingertip,
- energy ribbon nối theo quỹ đạo tay,
- glow chỉ xuất hiện khi gesture gần được nhận diện,
- distortion field quanh palm,
- pulse khi gesture đã lock.

Debug mode mới hiển thị landmark/skeleton.

## 8. Error tolerance

Khi webcam mất track trong thời gian ngắn:

- giữ pose cuối trong 100–200 ms,
- fade effect thay vì snap về 0,
- không trigger release ngay lập tức,
- nếu mất lâu hơn threshold mới reset gesture.

## 9. Gesture priority

Một số gesture có thể xung đột. Dùng priority:

1. Two-hand macro gesture
2. Pinch/grab
3. Fist/open-palm action
4. Pointing
5. Passive motion

Ví dụ khi hai tay đang tạo portal thì không được đồng thời spawn star bằng ngón trỏ.

## 10. MVP gesture set

Giai đoạn đầu chỉ cần 4 gesture:

1. **Expand** — kéo hai tay ra.
2. **Collapse** — chụm hai tay vào.
3. **Black Hole** — nắm tay.
4. **Seed Star** — chỉ tay.

Nếu 4 gesture này đủ mượt và đẹp thì trải nghiệm đã có thể demo được.