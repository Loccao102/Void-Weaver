# 05 — Technical Architecture

## 1. Suggested stack

### Frontend

- React + TypeScript + Vite
- Three.js
- `@react-three/fiber`
- `@react-three/drei`
- Zustand
- MediaPipe Hand Landmarker
- React Three Postprocessing hoặc Three.js EffectComposer
- GLSL shaders
- Web Audio API / Tone.js

### Không cần backend trong MVP

Void Weaver có thể chạy hoàn toàn client-side:

```text
Webcam
  ↓
MediaPipe
  ↓
Gesture Engine
  ↓
Interaction State
  ↓
Three.js Simulation
  ↓
Shaders / Particles / Audio
```

Backend chỉ cần khi sau này muốn:

- lưu universe seed,
- gallery screenshot,
- share creations,
- multiplayer,
- leaderboard/event.

## 2. High-level architecture

```text
┌──────────────────────────────┐
│          Webcam Input        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│      Hand Tracking Layer     │
│ MediaPipe + landmarks        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│       Gesture Engine         │
│ smoothing + classifier       │
│ state machine + confidence   │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│       Interaction Store      │
│ gesture / cursor / entropy   │
└───────┬──────────┬───────────┘
        ↓          ↓
┌─────────────┐ ┌──────────────┐
│ Cosmos Sim  │ │ Audio Engine │
└──────┬──────┘ └──────────────┘
       ↓
┌──────────────────────────────┐
│         R3F Scene            │
│ galaxy / objects / entities  │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Shaders + Post Processing    │
└──────────────────────────────┘
```

## 3. Proposed folder structure

```text
src/
├── app/
│   ├── App.tsx
│   └── Experience.tsx
├── camera/
│   ├── WebcamProvider.tsx
│   ├── handLandmarker.ts
│   └── camera.types.ts
├── gestures/
│   ├── GestureEngine.ts
│   ├── GestureStateMachine.ts
│   ├── gestureFeatures.ts
│   ├── gestureEvents.ts
│   ├── smoothing.ts
│   └── detectors/
│       ├── detectFist.ts
│       ├── detectPoint.ts
│       ├── detectPinch.ts
│       └── detectTwoHandScale.ts
├── cosmos/
│   ├── Galaxy.tsx
│   ├── Starfield.tsx
│   ├── Nebula.tsx
│   ├── BlackHole.tsx
│   ├── Portal.tsx
│   ├── planets/
│   ├── entities/
│   └── events/
├── materials/
│   ├── CosmicMaterial.tsx
│   ├── galaxy/
│   ├── void/
│   └── portal/
├── simulation/
│   ├── entropy.ts
│   ├── universeSeed.ts
│   ├── gravityField.ts
│   └── cosmicEventDirector.ts
├── effects/
│   ├── PostProcessing.tsx
│   ├── Trails.tsx
│   ├── Shockwave.tsx
│   └── HandEnergy.tsx
├── audio/
│   ├── AudioEngine.ts
│   └── reactiveAmbience.ts
├── store/
│   ├── useGestureStore.ts
│   ├── useUniverseStore.ts
│   └── useSettingsStore.ts
├── ui/
│   ├── CameraPermission.tsx
│   ├── Calibration.tsx
│   └── DebugOverlay.tsx
└── utils/
```

## 4. Gesture layer isolation

MediaPipe không nên được gọi trực tiếp từ component galaxy/entity.

Sai:

```text
Galaxy → đọc MediaPipe landmark
BlackHole → đọc MediaPipe landmark
Portal → đọc MediaPipe landmark
```

Đúng:

```text
MediaPipe
  ↓
GestureEngine
  ↓
Normalized Gesture State
  ↓
Galaxy / BlackHole / Portal
```

Nhờ vậy sau này có thể thay MediaPipe bằng model khác mà không rewrite scene.

## 5. Stores

### `useGestureStore`

Giữ dữ liệu realtime đã normalize:

```ts
type GestureState = {
  leftHandTracked: boolean;
  rightHandTracked: boolean;
  leftPalm: Vector3Like;
  rightPalm: Vector3Like;
  pointingPosition?: Vector3Like;
  twoHandDistance: number;
  expansionVelocity: number;
  activeGesture?: string;
  gestureStrength: number;
};
```

Không nên lưu toàn bộ raw landmarks vào Zustand mỗi frame nếu không cần, vì sẽ gây rerender/overhead.

### `useUniverseStore`

```ts
type UniverseState = {
  seed: number;
  entropy: number;
  expansion: number;
  spiralTwist: number;
  blackHoles: CosmicObject[];
  stars: CosmicObject[];
  activeEvent?: CosmicEvent;
};
```

## 6. Frame-loop strategy

Các dữ liệu thay đổi 60 lần/giây nên ưu tiên `ref` hoặc mutable state trong render loop.

```text
MediaPipe frame (~30 FPS)
        ↓
latestGestureRef
        ↓
R3F useFrame (~60 FPS)
        ↓
lerp visual state
```

Không `setState()` React cho từng landmark ở mỗi frame.

## 7. Universe seed

Universe seed có thể quyết định:

- galaxy branch count,
- palette,
- star density,
- nebula distribution,
- initial anomaly chance,
- entity variants.

Ví dụ:

```ts
const universe = generateUniverse(seed);
```

Rebirth chỉ cần tạo seed mới rồi transition giữa parameter sets.

## 8. Cosmic Event Director

Một module điều phối event dựa trên:

- entropy,
- thời gian kể từ event trước,
- gesture gần đây,
- universe seed,
- object state.

Pseudo logic:

```ts
if (entropy > 40 && cooldownReady('living-planet')) {
  maybeSpawn('living-planet');
}

if (entropy > 70 && portalRecentlyOpened) {
  maybeSpawn('star-whale');
}

if (entropy > 92) {
  prepareCollapse();
}
```

Event Director giúp scene có cảm giác phản ứng có chủ đích thay vì random thuần túy.

## 9. Shader architecture

Shader nên nhận các uniform chung:

```ts
uTime
uEntropy
uInteractionPoint
uInteractionStrength
uUniverseSeed
```

Nhờ vậy galaxy, planet và nebula cùng phản ứng với một “luật vũ trụ”.

## 10. Performance strategy

Ưu tiên GPU cho số lượng lớn object.

Dùng:

- `THREE.Points` cho starfield/galaxy,
- `InstancedMesh` cho debris/asteroid lặp lại,
- shader animation thay vì update từng vertex bằng JS,
- culling cho entity xa,
- adaptive DPR,
- quality presets.

### Quality presets

**Low**
- ít particles,
- DPR cap thấp,
- distortion đơn giản,
- ít transparent layers.

**Medium**
- default.

**High**
- particle density cao,
- richer post FX,
- extra nebula layers,
- higher shadow/texture quality nếu có.

## 11. Debug mode

Debug overlay nên hiển thị:

- camera FPS,
- render FPS,
- tracking confidence,
- current gesture,
- gesture strength,
- entropy,
- particle count,
- draw calls,
- active cosmic event.

Có thể bật bằng query param:

```text
?debug=1
```

## 12. Development order

Đừng bắt đầu bằng creature.

Thứ tự kỹ thuật hợp lý:

```text
R3F scene
→ galaxy particle system
→ webcam
→ hand tracking
→ 1 gesture
→ visual response
→ remaining MVP gestures
→ black hole
→ entropy
→ anomaly
→ creature
```

Interaction lõi phải vui trước khi thêm content.