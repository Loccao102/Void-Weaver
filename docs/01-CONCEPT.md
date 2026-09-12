# 01 — Concept & Experience Vision

## 1. High concept

**Void Weaver** là một interactive 3D cosmic sandbox điều khiển bằng webcam. Hai bàn tay của người dùng được hiểu như lực tự nhiên có thể kéo giãn, xoắn, sinh ra, làm biến dị và phá huỷ vật chất vũ trụ.

Project không đặt nặng gameplay truyền thống. Nó là một **digital toy**: người dùng vào để nghịch, thử gesture, gây ra những phản ứng bất ngờ và tạo ra một vũ trụ riêng.

## 2. Fantasy chính

Người dùng phải có cảm giác:

> “Mình không đang điều khiển giao diện. Mình đang chạm trực tiếp vào một vũ trụ sống.”

Vì vậy mọi interaction nên có quán tính, độ trễ thị giác nhẹ, âm thanh phản hồi và hậu quả dây chuyền thay vì chỉ bật/tắt hiệu ứng.

## 3. Core loop

1. **Create** — sinh sao, vật chất, planet seed hoặc energy node.
2. **Shape** — kéo, xoắn, nén, mở rộng và đổi quỹ đạo.
3. **Disturb** — tạo black hole, supernova, portal, gravity tear.
4. **Mutate** — entropy tăng, universe bắt đầu xuất hiện anomaly.
5. **Encounter** — cosmic entity xuất hiện và phản ứng lại người chơi.
6. **Collapse** — universe mất ổn định và đi đến Big Crunch / Void Event.
7. **Rebirth** — tạo một universe seed mới với biến thể visual khác.

## 4. Trải nghiệm theo nhịp

### Phase A — Wonder

- Một spiral galaxy nhỏ hiện giữa không gian.
- Hand tracking phản hồi ngay với chuyển động tay.
- Kéo hai tay ra làm galaxy mở rộng.
- Chỉ tay tạo một star seed.

Mục tiêu: người dùng hiểu interaction trong vài giây mà không cần tutorial dài.

### Phase B — Control

- Xoay cổ tay làm galaxy twist.
- Chụm hai tay nén vật chất.
- Nắm tay tạo vùng gravity mạnh.
- Orbit và particle trail bắt đầu phản ứng rõ rệt.

Mục tiêu: tạo cảm giác đang thật sự “nắn” hệ thống.

### Phase C — Strangeness

- Entropy tăng.
- Nebula có hành vi sống.
- Một constellation quay lại nhìn người dùng.
- Planet có pulse hoặc hút ánh sáng từ vật thể lân cận.

Mục tiêu: chuyển từ đẹp → đẹp nhưng bất an.

### Phase D — Cosmic Event

- Portal mở.
- Star Whale / Void Serpent / Eye Nebula xuất hiện.
- Space distortion tăng.
- Âm thanh trở nên dày và trầm hơn.

### Phase E — Collapse & Rebirth

- Người dùng có thể chủ động collapse hoặc universe tự mất ổn định khi entropy quá cao.
- Vật chất bị kéo về singularity.
- Màn hình gần như tối hoàn toàn.
- Một seed mới phát sáng và universe mới bắt đầu.

## 5. Design pillars

### Immediate
Không có menu dày đặc. Interaction chính phải xảy ra trong scene.

### Physical
Gesture không nên map thành nút bấm đơn giản. Khoảng cách, tốc độ và hướng chuyển động tay nên trở thành tham số vật lý.

### Procedural
Mỗi universe nên hơi khác về màu, spiral count, density, anomaly seed và entity event.

### Beautiful first
Nếu phải chọn giữa “nhiều feature” và “ít feature nhưng rất đẹp”, ưu tiên phương án thứ hai.

### Strange, not horror
Void Weaver có thể creepy nhưng không phải horror game. Dị thường nên gợi tò mò hơn là jumpscare.

## 6. One-session example

1. Người dùng mở webcam.
2. Hai tay xuất hiện dưới dạng subtle energy traces.
3. Kéo tay ra → galaxy nở lớn.
4. Xoay tay → spiral arms bị bẻ cong.
5. Chỉ vào khoảng trống → tạo một star.
6. Nắm tay → black hole xuất hiện.
7. Entropy tăng đến 45% → một Living Planet bắt đầu pulse.
8. Tạo portal → Star Whale đi xuyên qua scene.
9. Entropy vượt 85% → gravity field trở nên bất ổn.
10. Chụm hai tay mạnh → Big Crunch.
11. Universe mới sinh ra với seed khác.

## 7. Không làm gì ở giai đoạn đầu

- Không quest tree.
- Không inventory.
- Không backend phức tạp.
- Không login/auth.
- Không multiplayer.
- Không cố mô phỏng vật lý thiên văn chính xác.
- Không build hàng chục creature trước khi interaction lõi đủ vui.

Void Weaver nên bắt đầu như một **beautiful interactive toy**, rồi mới mở rộng.