**Project Overview**
- **Name**: Magical Christmas Forest — an immersive VR night-time pine forest scene with a cozy cottage, decorated Christmas tree, and interactive environmental details.
- **Focus**: Atmosphere, environmental storytelling, optimized particle systems, and intuitive VR interactions using Unity's XR Interaction Toolkit.

**Quick Facts**
- **Unity Version**: Unity 2023.6.0f1 (DX11)
- **Render Pipeline**: Universal Render Pipeline (URP)
- **XR**: XR Interaction Toolkit (OpenXR / target headset runtime)
- **Target Hardware**: Oculus Quest 2 (tested), HTC Vive, other PC VR headsets

**Getting Started**
- **Open**: Launch Unity Hub and open the project at the repository root (the folder containing `Assets/` and `ProjectSettings/`).
- **XR Setup**: If not already enabled, open `Edit > Project Settings > XR Plug-in Management` and enable the appropriate loader (OpenXR recommended). Install any required packages via the Package Manager (`Window > Package Manager`).
- **Play in Editor**: Use `Play` while a compatible XR runtime (e.g., SteamVR or Oculus Link/OpenXR) is running to test in the editor.
- **Build**: Use `File > Build Settings` to select your target platform (Android for Quest 2, PC for SteamVR) and configure Player settings (single-pass instanced, Vulkan/DX11 as appropriate).

**Controls & Interaction**
- **Locomotion**: Continuous movement with thumbstick and optional teleportation via raycast to snowy ground areas.
- **Turning**: Snap-turn (45° increments) to reduce motion sickness.
- **Grab/Use**: Tree ornaments, lantern handles, and other props are setup as `XR Grab Interactable` objects. Hover states use glow highlights and grabs trigger localized sound cues.
- **Fireflies**: Proximity triggers cause fireflies to disperse (trigger colliders + light Rigidbody forces).

**Scene Composition**
- **Static Geometry**: Snow-covered fir trees, low-poly cottage (UV-mapped wood textures), terrain, lamp posts, and a decorated Christmas tree. Materials assigned directly to Mesh Renderers (e.g., `Wood_Cottage.mat`) using URP Lit shader.
- **Dynamic Objects**:
  - Snow: Particle System (looping, ~5s lifetime, size ~0.15, local simulation space).
  - Chimney Smoke: ~40 particles with rising velocity curves and color fade.
  - Fireflies: Warm orange particles (~100) with velocity-over-lifetime.
  - Lamp Flicker: Lightweight sine-wave intensity animation for candle-like glow.

**Materials & Tuning**
- **Snow Density**: Controlled by Particle System emission rate (example: 500 particles/sec).
- **Light Emissive Strength**: Adjust `_EmissionColor` on lamp and cottage materials.
- **Sparkle / Glow**: Tweak Start Lifetime and Start Size on sparkle particle systems.
- **Access**: Expose parameters via the Inspector or hook them to VR UI sliders for runtime tweaking.

**Rendering & Optimization**
- **URP Configuration**: Forward rendering with Single-Pass Instanced (xR single-pass) enabled for improved performance.
- **Post**: Bloom and color adjustments are handled via URP post-processing for subtle glow on lights and ornaments.
- **Shaders**: URP Lit for geometry; Particle shader for snow, smoke, sparkles, fireflies.
- **Assets**: Low-poly meshes and compressed textures (ASTC for mobile/Quest) to reduce memory and draw calls.
- **Culling**: Frustum-based particle culling and optimized LODs used to maintain stable VR frame rates (>70 FPS in most tests).

**Physics & Particles**
- **Particles**: Built-in Particle System with gravity modifiers and velocity-over-lifetime for wind-like motion (avoids full Wind Zones to preserve performance).
- **Terrain**: Unity Terrain with Terrain Collider for grounding and footstep interactions.
- **Rigidbodies**: Applied to interactive props (ornaments, gifts) for natural movement and collisions.

**Performance Summary / Test Results**
- **VR FPS Stability**: 70–90 FPS depending on hardware (Quest 2 results vary when using different supersampling or graphics settings).
- **Draw Calls**: ~220 after static batching.
- **Memory Usage**: ~600 MB with compressed textures.
- **Particle Stress**: Stable up to ~800 particles with current optimizations.
- **User Testing**: Three users tested on Oculus Quest 2. Feedback prompted brightening tree lights and reducing snow density.

**Customization & Tuning Tips**
- **Expose Parameters**: Use inspector-exposed fields on particle systems and materials; consider a small VR settings panel that writes to those properties at runtime.
- **Texture Compression**: Use ASTC for Android builds (Quest), BC formats for PC builds.
- **Single-Pass Rendering**: Enable for XR to reduce GPU cost (check Player Settings and URP asset).
- **LOD & Batching**: Keep low-poly LODs and use static batching for non-moving geometry.

**Project Structure (Important Files)**
- **Scenes**: `Assets/Scenes/` — main environment scene(s).
- **Input**: `Assets/InputSystem_Actions.inputactions` — input action map for controls.
- **Packages**: `Assets/BOXOPHOBIC/` and other asset folders contain vendor assets and utilities.

**Credits & Assets**
- **Source Assets**: Low Poly packs and assets from Poly Haven / Low Poly Village packs (see `Assets/` for exact folders).
- **Third-Party**: Boxophobic packages included in `Assets/BOXOPHOBIC/`.

**Notes & Next Steps**
- Consider adding a small in-VR settings menu for snow density, light intensity, and particle count to let players tune performance.
- If building for Quest 2, verify OpenXR runtime and controller bindings before production builds.

**Contact**
- For questions or to share improvements, open an issue or contact the project owner.

---
Generated from the project's design notes and test results. File: `README.md`.
