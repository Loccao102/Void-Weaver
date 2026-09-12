# 04 — 3D Asset Strategy

## 1. Nguyên tắc quan trọng nhất

**Không model cả vũ trụ thành `.glb`.**

Void Weaver nên dùng đúng công cụ cho đúng loại asset:

| Loại asset | Cách làm chính |
|---|---|
| Galaxy | GPU particles + shader |
| Nebula | particles / billboard / volumetric-style shader |
| Starfield | points / instancing |
| Black hole | primitive mesh + custom shader + post FX |
| Planet | sphere + procedural/material shader |
| Portal | ring/torus + shader + particles |
| Energy trail | curve/ribbon/particle trail |
| Star Whale | GLB + shader + particles |
| Void Serpent | spline/procedural segments hoặc GLB hybrid |
| Cosmic Jellyfish | procedural body + curve tentacles hoặc GLB hybrid |
| Ancient Relic | GLB |

Model 3D chỉ nên chịu trách nhiệm cho **silhouette và form**. Phần khiến asset có chất cosmic đến từ material, shader, motion, lighting và particles.

## 2. Galaxy

### Geometry

Không dùng mesh cho từng star.

Dùng `THREE.Points` với hàng chục nghìn particle.

Mỗi particle có thể lưu:

- radius,
- branch index,
- angle,
- randomness,
- size,
- brightness,
- seed.

### Spiral generation

Một mô hình đơn giản:

```text
angle = radius * spin + branchOffset + randomness
x = cos(angle) * radius + randomOffset
z = sin(angle) * radius + randomOffset
y = verticalNoise
```

Shader chịu trách nhiệm:

- twinkle,
- core brightness,
- color variation,
- distortion khi hand tác động,
- entropy deformation.

## 3. Nebula

Nebula không cần volumetric raymarching ngay từ MVP.

Có thể bắt đầu bằng:

- layered transparent sprites,
- noise texture,
- additive/alpha blending,
- depth variation,
- slow flow field.

Sau này mới thử raymarching hoặc 3D noise nếu performance cho phép.

## 4. Black hole

Black hole gồm nhiều lớp:

```text
Black Hole
├── dark core
├── event horizon rim
├── accretion disk
├── orbiting particles
└── screen-space distortion / pseudo lensing
```

Core có thể chỉ là sphere/plane đen.

Accretion disk dùng ring geometry hoặc particle belt.

Điểm quan trọng nhất là **distortion + motion**, không phải polygon count.

## 5. Planet

Planet base chỉ cần sphere.

Material có thể gồm:

- base procedural noise,
- fresnel rim,
- emissive veins,
- animated displacement,
- atmosphere shell,
- cloud layer tùy biến thể.

Một sphere có thể trở thành nhiều loại planet chỉ bằng shader preset:

```text
Sphere + molten shader      → Ember Planet
Sphere + emissive veins     → Living Planet
Sphere + translucent shell  → Ghost Planet
Sphere + dark tendrils      → Corrupted Planet
```

## 6. Portal

Portal nên được tạo procedural:

- torus/ring làm biên,
- shader noise làm edge biến dạng,
- particle stream chạy quanh vòng,
- inner plane hiển thị distorted universe khác,
- scene refraction giả lập bằng render texture nếu cần.

Không cần model riêng.

## 7. Creature workflow

Các creature có silhouette đặc thù mới cần model thật.

Workflow:

```text
Concept silhouette
    ↓
Blender hoặc AI 3D base mesh
    ↓
Cleanup / retopology
    ↓
UV nếu thực sự cần texture
    ↓
Rig nếu cần animation xương
    ↓
Export GLB
    ↓
Three.js custom material
    ↓
Particles / trails / bloom
```

## 8. Star Whale example

### Model cần gì?

- body rõ silhouette,
- fins lớn,
- tail đẹp khi nhìn từ xa,
- topology đủ sạch để deform,
- không cần skin detail dày đặc.

### Cosmic layer trong Three.js

- semi-transparent surface,
- fresnel glow,
- emissive constellation veins,
- noise flow chạy dọc thân,
- stardust emit từ fins,
- tail ribbon,
- subtle body deformation.

Một model 20k–50k triangles có shader tốt thường hiệu quả hơn model cực nặng nhưng material bình thường.

## 9. Void Serpent example

Có thể tránh GLB hoàn toàn ở bản đầu.

- tạo spline dài,
- sinh nhiều segment theo curve,
- head là primitive/model nhỏ,
- body dùng instanced mesh,
- shader tạo pulse chạy dọc cơ thể.

Ưu điểm: dễ thay đổi độ dài và chuyển động procedural.

## 10. Cosmic Jellyfish example

Hybrid procedural rất hợp:

- dome = sphere bị cắt/deform,
- tentacles = curves/tubes,
- translucent fresnel material,
- particles bên trong body,
- tentacle motion dùng sine/noise.

## 11. Cosmic Material System

Nên tạo material abstraction dùng lại cho nhiều asset.

Ví dụ API ý tưởng:

```tsx
<CosmicMaterial
  preset="living"
  emissiveIntensity={2.2}
  fresnel={1.4}
  noiseScale={3.0}
  distortion={0.16}
  pulse={0.35}
  entropy={entropy}
/>
```

Các preset có thể gồm:

- `stellar`
- `living`
- `void`
- `corrupted`
- `spectral`
- `portal`

## 12. Asset performance budget

Các con số ban đầu chỉ là guideline:

- galaxy/star particles: GPU-driven,
- creature hero asset: khoảng 20k–80k triangles,
- secondary creature: thấp hơn,
- texture ưu tiên 1K/2K,
- dùng KTX2/Basis khi bắt đầu tối ưu,
- Draco/Meshopt cho GLB khi cần,
- tránh transparency overlap quá nhiều.

## 13. Khi nào dùng Blender?

Dùng Blender khi cần:

- silhouette độc bản,
- rig/animation,
- UV/model cleanup,
- baked mesh,
- creature/ancient object có form rõ.

Không cần Blender cho:

- galaxy,
- black hole,
- nebula,
- portal,
- starfield,
- simple planet.

## 14. Asset creation rule

Trước mỗi asset hãy hỏi:

> “Form này có thật sự cần mesh riêng, hay shader + particle + primitive đã tạo được 90% hiệu quả?”

Nếu câu trả lời là shader/procedural đã đủ, không tạo GLB.