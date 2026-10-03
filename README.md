<p align="center">
  <img src="assets/splash.png" alt="Frames — Creative Studio" width="100%" />
</p>

<h1 align="center">Frames</h1>
<p align="center"><strong>Frame-based VFX + AI-gen compositor.</strong></p>
<p align="center">
  Drop media on a board. Grade, key, matte and comp it in-app, generate with ComfyUI or cloud models,
  review with your team in ShotGrid — and every output keeps a line back to what made it.
</p>

---

## What Frames is

Frames is a desktop studio for VFX artists: a board you drop media onto, **frames** that hold a shot's work, and native compositing tools that run in the app — plus ComfyUI templates (local or on a RunPod GPU) and cloud generation models when you need AI.

- **Native frames, no node wiring.** Merge, Color, Blur, Keyer, Despill, Transform, Retime, Regrain and Invert run in-app in float, preview live, and bake masters (ProRes / EXR / HEVC).
- **ComfyUI templates as forms.** Templates declare their inputs; Frames builds the settings form. Drop media into slots, hit Run.
- **Cloud generation built in.** Google Vertex (Nano Banana, Veo, Omni), FAL (Seedance, Kling, MiniMax, Wan…), Beeble, Topaz and BytePlus from one widget.
- **Lineage by default.** Every output knows which inputs and settings produced it.
- **Production tie-in.** Track your time, map it to ShotGrid tasks, review versions with frame annotations, and post notes to artists — without leaving the app.

---

## Install

> Frames is currently in **closed beta**. Activation requires approval — see [Activate](#activate).

### Windows

Download the latest `Frames-Setup-X.Y.Z.exe` from the [Releases page](https://github.com/richservo/frames-releases/releases/latest) and run it.

- Installs per-user under `%LOCALAPPDATA%\Programs\Frames` (folder can be changed). No admin rights needed.
- The installer is small (~120 MB). The Python runtime that powers the local AI tools is set up on **first launch** (see below), not during install.
- The installer is not code-signed yet — Windows SmartScreen will warn on first run. Click **More info → Run anyway**.

### First launch: runtime setup

After activation, the **Setting up Frames** screen installs the Python runtime once (several GB):

1. **Location** — default `%LOCALAPPDATA%\Frames\runtime`, or pick another drive with **Change…** (handy to keep large files off C:).
2. **Hardware** — **NVIDIA GPU (CUDA)** or **CPU only**. The detected option is marked.
3. **Install** — progress streams live. Later app updates only download what changed.

Model weights download separately the first time you use each feature. The runtime can be moved later from **Settings → Python runtime**.

### macOS

Coming soon.

---

## Activate

First launch shows the activation screen.

### Request access (closed beta)

1. Enter your full name, email and mailing address, then **Request access**.
2. The screen shows "Request submitted" and checks for approval every few seconds. You can close the app — the next launch picks up where it left off.
3. Once approved, the license applies automatically and the app opens.

Your details are encrypted in transit and used only to issue and support your license.

### Already have a .rslicense file

Click **I have a .rslicense file already → Choose .rslicense file…**. It's verified and stored in your user data.

The **Machine ID** at the bottom of the screen (with a copy button) is what support may ask for.

---

## Quick start

1. **Open Studio** — click **Studio** in the left nav. The canvas is the big empty space.
2. **Drop media** — drag videos, images or image sequences from your desktop onto the canvas.
3. **Add a frame** — press **Tab** for the widget palette, or use the Alt shortcuts (e.g. **Alt+C** Color, **Alt+K** Keyer, **Alt+F** a ComfyUI Frame around your selection).
4. **Wire it** — drag a media card into the frame's input; tweak it live in the frame's viewer.
5. **Run output** — bakes a master to the library (and to the board's output folder if set).

To run ComfyUI templates, add a connection first (see [Connection](#connection)) — local ComfyUI or a RunPod pod.

---

## Feature reference

### Studio — boards and canvas

An infinite pan/zoom board (middle-mouse / two-finger drag to pan, wheel to zoom).

- **Boards and projects** — the board switcher shows a project tree (Show → Scene → …, any depth). Boards without a project are *Unfiled*. Search by name or content.
- **Board history** — the live board plus five rolling backups, restorable (and the restore is undoable).
- **Board Settings** — per board:
  - **Project** placement in the tree.
  - **Allowed credential profiles** — lock a board to a client's accounts; other profiles are hidden and refused at run time.
  - **Output folder** — where **Run output** delivers masters (the library proxy stays in place).
  - **Output frame rate** and **output colorspace** for rendered masters (Auto follows the source).
  - **GCS bucket** — required for Google's Generative Media Pro models.
  - **ShotGrid time logs** — which ShotGrid task this board's tracked time goes to.
- **Media cards** — images, video and image sequences with trim (in/out marks), retime, resize, and audio.
- **Lineage** — outputs keep a dashed line back to their inputs.

#### Native frames (run in-app, no ComfyUI needed)

| Frame | Shortcut | What it does |
|---|---|---|
| **Merge** | Alt+M | Layer stack compositing (over, screen, multiply…). |
| **Color** | Alt+C | Float grade: exposure, white balance, lift/gamma/gain wheels, contrast, ASC-CDL, saturation, curves, scopes, .cube LUTs. |
| **Blur** | Alt+B | Gaussian, box, disc and bokeh defocus with lens presets; optional mask. |
| **Invert** | Alt+I | Invert a clip or matte. |
| **Transform** | Alt+T | Move / scale / rotate with a gizmo, keyframeable, optional mask. |
| **Despill** | Alt+D | Remove green/blue spill with spill replacement and cast correction. |
| **Keyer** | Alt+K | Chroma key with screen balance, clip black/white and built-in despill. |
| **Regrain** | Alt+G | Re-apply the plate's grain to a comp, per-channel. |
| **Retime** | Alt+R | Keyable speed curve; renders in-betweens with RIFE. |
| **Frame** | Alt+F | ComfyUI template container: pick a template, fill its slots, Run. |

Every native frame previews live and has **Run output** to bake a master (ProRes / EXR / HEVC).

#### Widgets

| Widget | What it does |
|---|---|
| **Generate Media** | Cloud image/video generation. Google Vertex (Nano Banana Pro / 2, Veo 3 / 3.1, Gemini Omni, Generative Media Pro models), FAL (Seedance, Kling, MiniMax H3, Wan, GPT Image, Seedream, depth, upscale…), Beeble SwitchX, Topaz (upscale / interpolation), BytePlus Seedance. Reference bin, history rail, @mentions. |
| **Inpaint** | Paint a mask and regenerate just that area as a toggleable layer, with any image model you have credentials for — Google Vertex (Nano Banana Pro / 2) or FAL (Nano Banana, GPT Image, Seedream…). Clone stamp, video timeline, layer groups. |
| **Local Generate Media** | Wan VACE video generation, locally or on a pod; pod models include Wan 2.2 VACE, ID-V2V, SCAIL-2 and MiniMax H3 (ref-to-video, masked, ControlNet, first/last frame). |
| **SAM3 Mask** | Click points to mask a subject; propagates through video. Runs locally. |
| **MatAnyone** | Mask-guided video alpha matting (feed it a SAM3 mask). |
| **ViTMatte** | Turn a rough mask into a clean alpha edge (hair, fur, props). |
| **Rotoscope** | Animatable bezier shapes with feather; Ctrl+drag snaps points to edges. |
| **3D Camera** | Turn a still + depth into a mesh you can move to find a new camera angle. |
| **Tile Outpaint** | Split a larger canvas into overlapping tiles, generate each, stitch with blending. |
| **LoRA Trainer** | Train Wan 2.2 character / style / object LoRAs on a connected pod, with live loss and samples. |
| **Prompt Enhancer** | Rewrite prompts with Ollama, a RunPod serverless endpoint or Claude; positive / negative outputs wire into template slots. |
| **LatLong Rotate** | Rotate 360° equirectangular images, with exposure / HDR range. |
| **Solid** | Solid-color image or video plate. |
| **Note** | Sticky note. |

### Time

A passive time tracker: it records what you worked on each day — runs, generations, bakes, imports, edits and time active in the app, per board — with no timers to remember.

- **Range** — Today by default; Yesterday, This week, Last week, This month, or any date range. Past days are rebuilt from your history, so it works retroactively.
- **Project filter** — one project and everything nested under it, for per-client reports.
- **Manual tasks** — Start / Stop named tasks (e.g. "R&D: depth model"), edit times afterwards, add notes.
- **Views** — totals per board and per task, a per-day timeline, and a detailed log of every block.
- **Export** — **PDF** report, **detailed CSV**, or a **ShotGrid CSV** (decimal hours).
- **Push to ShotGrid** — send time logs straight to the mapped ShotGrid tasks, with a preview first. Pushing a day again updates the same time logs instead of duplicating them.

### ShotGrid

Appears in the nav once a ShotGrid site is added in Credentials. A badge shows tasks with unread notes.

- **Modes** — My tasks (all projects), Project tasks, All shots, and Playlists. Sortable columns, text search, filters for task, task status and shot status, **Hide final**, **New notes only**. Filters are remembered per project.
- **Multi-select** — click, Ctrl+click, Shift+click.
- **Task / shot detail** — thumbnail, description, cut range, statuses, dates, bid vs logged, notes with replies and attachments, and every version with playback.
- **New-note alerts** — tasks with notes you haven't read are highlighted and announced, following ShotGrid's own read state.
- **Log time / Start timer / New note** from any task.
- **Upload from the canvas** — right-click a media card → **Upload to ShotGrid…** creates a Version on the task (review copy or master), auto-named as the next version, with your description. Progress shows in the Transfers dock.

#### Playlists and review

- **ShotGrid playlists** — open any project playlist; create new ones; **+ Playlist** on any version.
- **Local playlists** — right-click shots → **Add to local playlist**. Kept in Frames; each shot plays its latest video unless you pin a version; save to ShotGrid any time.
- **Quick playlists** — **Whole sequence** or **Prev / current / next** for any shot, in cut order, skipping omitted shots, using each shot's latest video.
- **Review player** — plays continuously (the next clip loads ahead), thumbnail strip that follows playback, hover a tile to pick another version, × to drop a clip, **Solo** to loop one clip.
- **Frame annotations** — pause, draw (pen with colors, arrow, circle, square, text), and post: the artist gets a ShotGrid note with the exact frames attached, numbered in ShotGrid's frame range. Annotated frames show as diamonds on the playbar; jump between them with **[** / **]**. Text annotations prefill the note.
- **Viewer color** — exposure, gamma, contrast and saturation per clip (view only).

| Review key | Action |
|---|---|
| Space | Play / pause |
| ← / → (or , / .) | Step one frame |
| J / K / L | Reverse / pause / forward (press again for 2×, 4×); hold K + J/L to step |
| ↑ / ↓ | Previous / next clip |
| [ / ] | Previous / next annotated frame |
| S | Solo (loop this clip) |
| Ctrl+Z | Undo annotation |

### Connection

Saved endpoints, stored encrypted:

- **Local ComfyUI** on this machine (install path + port).
- **Remote** pods — paste an SSH line, or the new-pod wizard for RunPod.

Several can be connected at once; the one you click is *focused* and gets Runs, Files, Resources and the ComfyUI view. Others stay connected so their in-flight runs keep streaming progress.

### Run flow

- **Run** submits to the focused ComfyUI. Runs queue per endpoint, one at a time, and survive an app restart (the app rebinds to prompts still running).
- **Sampling dock** (right rail) streams per-endpoint progress; **Completions** lists recent results — click to find them on the canvas.

### Other panels

- **Status** — live status and a full health check (pull server, SSH, tunnel, file round-trip).
- **Actions** — free memory, restart the local Python worker, kill / interrupt ComfyUI, start / stop Ollama.
- **ComfyUI** — the focused endpoint's ComfyUI, embedded, for authoring templates.
- **Files** — browse the focused endpoint, bookmarks, drag files onto the canvas.
- **Logs** — live log tail.
- **Resources** — GPU / VRAM / CPU / RAM / disks, history charts and processes.
- **Terminal** — a shell on the focused endpoint.
- **Storage** — reclaim disk space: automatic cleanup of rebuildable files, a review list with a 7-day trash, and model sizes.

### Credentials

One encrypted store (your OS keychain) for every service: **Google Vertex** (service account), **FAL**, **Beeble**, **Topaz**, **BytePlus**, **RunPod Serverless**, **Anthropic (Claude)** and **ShotGrid** (sign in inside the app — works with Autodesk single sign-on — or legacy login / script key).

Credentials are grouped by **profile** (e.g. a client name); boards can be locked to a profile. Open from **Settings → Credentials** or any widget that needs a key.

### Settings

- **Updates** — version, check now, download progress, release notes, **Restart to update**.
- **Python runtime** — location, **Move…** to another drive.
- **Credentials** — opens the credentials manager.
- **Data folder** — where the library, proxies, thumbnails and boards live (point it at a project drive); restart to apply.

---

## Keyboard shortcuts (Studio)

| Shortcut | Action |
|---|---|
| Tab | Widget / frame palette |
| Alt + F / M / C / B / I / T / D / K / G / R | Add Frame / Merge / Color / Blur / Invert / Transform / Despill / Keyer / Regrain / Retime |
| Ctrl/⌘ + A | Select all |
| Ctrl/⌘ + C / X / V | Copy / cut / paste (at the cursor) |
| Ctrl/⌘ + Z / Ctrl/⌘ + Shift + Z | Undo / redo |
| Delete / Backspace | Remove selection |
| R / G / B / A | View a single channel on every viewer (Esc clears) |
| P | Pause / resume board playback |

With a video card selected:

| Shortcut | Action |
|---|---|
| Space | Play / pause |
| ← / → | Step one frame |
| Home / End | Jump to in / out (or clip start / end) |
| J / K / L | Reverse / stop / forward (repeat for up to 8×) |
| I / O | Mark in / out |
| X (or Shift+I / Shift+O) | Clear in / out |

---

## Running without a pod

- **In-app** (no ComfyUI): all native frames, Rotoscope, 3D Camera, LatLong, Solid, Notes, plus SAM3 / MatAnyone / ViTMatte on your own GPU (after the runtime setup).
- **Local ComfyUI**: template Frames against ComfyUI on your machine.
- **Local Generate Media**: Wan 2.1 VACE runs locally; the larger models need a pod.
- **Cloud**: Generate Media, Inpaint and Prompt Enhancer (Claude / RunPod) need internet and a key, not a pod.
- **Pod only**: LoRA Trainer and the larger Local Generate Media models.

---

## Updates + support

Frames checks for updates at launch and every few hours from [`frames-releases`](https://github.com/richservo/frames-releases), downloads only what changed, and installs on quit — or right away from **Settings → Updates → Restart to update**.

Support, bugs and feedback: **gentle.fury@gmail.com**. Include your Machine ID (activation screen) and, if relevant, a log snippet or a copied error from the Errors dock.

---

## Not in this build yet

- macOS installer (Windows only for now).
- Code signing on Windows (SmartScreen will warn on first run).

---

<p align="center">
  <sub>© 2026 richservo · Frames Creative Studio</sub>
</p>
