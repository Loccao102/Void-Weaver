# 07 — Cosmic Entity Bible

## 1. Mục tiêu

Các entity trong Void Weaver không nên trông như quái vật fantasy được đặt vào background ngoài không gian.

Chúng phải có cảm giác **sinh ra từ chính vật chất vũ trụ**.

Một entity tốt nên thoả ít nhất 3 yếu tố:

1. silhouette nhận ra được từ xa,
2. material có tính cosmic/bioluminescent,
3. chuyển động không giống sinh vật trên mặt đất,
4. có quan hệ trực tiếp với particle/nebula/gravity xung quanh,
5. vừa đẹp vừa hơi khó giải thích bằng logic tự nhiên.

## 2. Shared visual DNA

Tất cả hero entities nên chia sẻ một số đặc điểm:

- dark translucent body hoặc deep-space surface,
- emissive veins / constellation nodes,
- fresnel glow ở viền,
- internal moving light,
- dust/particle shedding,
- chuyển động chậm, có quán tính,
- không quá nhiều chi tiết texture nhỏ.

Tránh:

- armour sci-fi,
- mechanical panel quá rõ,
- cyberpunk neon thuần,
- texture da realistic kiểu động vật Trái Đất,
- mắt/mồm literal nếu không có lý do nghệ thuật.

## 3. Star Whale

### Fantasy

Một sinh vật khổng lồ bơi qua khoảng không như đại dương. Cơ thể của nó gần như trong suốt và chứa một bầu trời sao nhỏ bên trong.

### Silhouette

- thân dài, mềm,
- fins rộng,
- tail lớn và thanh thoát,
- đầu đơn giản, không cần facial detail phức tạp.

### Surface

- deep blue/black translucent body,
- constellation veins,
- small stars visible inside,
- bright fresnel edge,
- occasional pulse đi từ head → tail.

### Motion

- bơi theo spline,
- body wave rất chậm,
- fins delay so với thân,
- tail ribbon kéo dài,
- không chuyển hướng gấp.

### Interaction

- xuất hiện từ portal,
- hơi nghiêng về phía hand cursor,
- khi người dùng đưa tay gần, constellation trên thân sáng hơn,
- có thể để lại star seeds sau khi đi qua.

## 4. Void Serpent

### Fantasy

Một đường sống dài tồn tại giữa gravity field và vật chất tối.

### Silhouette

- cực dài,
- đầu nhỏ hơn tưởng tượng,
- body được tạo từ nhiều segment hoặc energy vertebrae,
- không cần scale/skin truyền thống.

### Motion

- follow spline,
- body oscillation,
- có lúc đi xuyên galaxy plane,
- làm particle xung quanh lệch quỹ đạo.

### Material

- dark core,
- purple/cyan pulse chạy dọc spine,
- semi-transparent outer shell.

### Interaction

- bị hấp dẫn bởi black hole mạnh,
- có thể quấn quanh portal,
- entropy tăng khi nó xuất hiện.

## 5. Cosmic Jellyfish

### Fantasy

Một sinh vật nhẹ như nebula, trôi giữa các lớp không gian.

### Form

- translucent dome,
- internal star cluster,
- nhiều tentacle dạng energy curve,
- silhouette mềm và dễ nhận ra.

### Motion

- dome co/giãn chậm,
- tentacle lag theo inertia,
- drift theo noise field,
- không cần path rõ ràng.

### Interaction

- palm gần nó → tentacles hướng về bàn tay,
- open palm → body nở sáng,
- supernova gần đó → nó co lại rồi bỏ đi.

## 6. Eye Nebula

### Fantasy

Không phải “một con mắt bay ngoài vũ trụ”, mà là một cụm nebula tình cờ tổ chức thành cấu trúc có vẻ đang quan sát người dùng.

### Rules

- eye shape phải mơ hồ,
- iris hình thành từ particle density,
- pupil có thể là vùng void,
- eyelid là cloud flow chứ không phải da.

### Motion

- gaze follow cực chậm,
- blink bằng cách particle cloud khép lại,
- entropy cao → eye càng rõ.

## 7. Living Planet

### Fantasy

Một planet không phải sinh vật theo nghĩa truyền thống nhưng có nhịp sống.

### Visual

- pulse radius nhẹ,
- glowing cracks/veins,
- atmosphere co giãn,
- surface noise dịch chuyển như tissue nhưng không quá organic.

### Interaction

- hand cursor tiến gần → pulse nhanh hơn,
- pinch → có thể kéo planet,
- black hole gần → veins sáng mạnh do stress.

## 8. Parasite Moon

### Fantasy

Một moon nhỏ hút năng lượng từ planet chủ.

### Visual

- moon tối, ít emissive lúc đầu,
- energy tendrils nối với host,
- host dim dần,
- parasite sáng dần.

### Event

Người dùng có thể:

- tách nó ra bằng pinch,
- đẩy vào black hole,
- để nó hút cạn planet và tạo anomaly mới.

## 9. Ancient Relic

### Fantasy

Một cấu trúc không rõ do ai tạo, tồn tại trước universe hiện tại.

### Form

- geometric nhưng không mechanical,
- có thể là ring, monolith, broken polyhedron,
- floating segments,
- star-map engraving/emissive glyphs.

### Interaction

- chỉ phản ứng khi gesture nhất định xảy ra gần nó,
- có thể là nguồn mở secret portal,
- không cần giải thích lore trực tiếp.

## 10. Entity rarity

Để giữ cảm giác đặc biệt:

### Common anomaly
- Living Planet
- Broken Constellation
- Time Echo

### Uncommon
- Eye Nebula
- Parasite Moon
- Cosmic Jellyfish

### Rare hero event
- Star Whale
- Void Serpent
- Ancient Relic activation

Không nên cho hero entity xuất hiện liên tục.

## 11. Entity behavior rule

Entity không cần AI phức tạp. Chỉ cần phản ứng đủ để tạo ảo giác sống:

```text
idle procedural motion
+ attention to hand cursor
+ reaction to entropy
+ reaction to nearby cosmic event
+ entrance/exit behavior
```

Ví dụ Star Whale không cần pathfinding. Một spline đẹp + vài reaction đúng lúc đã đủ thuyết phục.

## 12. Prompt template cho concept art / AI 3D reference

```text
Design a [ENTITY NAME] for a strange living-cosmos interactive artwork.

The creature must feel born from nebulae, stardust and gravitational energy rather than from Earth biology.

Visual DNA:
- elegant readable silhouette
- dark translucent cosmic body
- subtle bioluminescent veins
- constellation-like internal lights
- ethereal fresnel glow around the silhouette
- sparse drifting particles
- mysterious and beautiful, not horror
- no armor, no machinery, no cyberpunk panels
- no busy surface texture

The design must remain recognizable from a distance and suitable for a real-time Three.js scene.
Provide clean front, side and 3/4 concept views with a neutral background for 3D modeling reference.
```

## 13. Final consistency test

Trước khi thêm một entity mới, hỏi 4 câu:

1. Nếu bỏ texture đi, silhouette có còn thú vị không?
2. Nó có trông như sinh ra từ Void Weaver universe không?
3. Nó có một interaction hoặc behavior riêng không?
4. Nó có làm scene thú vị hơn thay vì chỉ làm scene đông hơn không?

Nếu không trả lời “có” cho ít nhất 3/4 câu, chưa nên đưa entity đó vào project.