# Svax Launcher 1.4.0

A Minecraft: Java Edition launcher for Windows with independent instances, Modrinth mods and modpacks, Litematica schematics (with an online catalogue and a 3D preview), a live game console, a mod collection builder and a 3D skin wardrobe. The interface is a calm, flat dark theme in the spirit of the Modrinth App, with a Lunar-style Play screen.

![Home](Preview.jpg)

**Magyar útmutató** a telepítéshez és a Microsoft-bejelentkezés beállításához: [TELEPITES-ES-BEJELENTKEZES.md](TELEPITES-ES-BEJELENTKEZES.md).

## Start

1. Close any older Svax Launcher window.
2. Extract this entire ZIP into a new folder.
3. Run **Start-SvaxLauncher.bat**. The first run installs the dependencies.

### One file for other players

Run **Build-Windows.bat** on Windows. It produces **`dist\SvaxLauncher.exe`**: a single file that needs no Python and contains no loose source files. Share only that file. The project's Azure application ID is built in (`svax/build_config.py`), so other players only press **Add account**. A private GitHub repository can also build the exe with the included Actions workflow (`.github/workflows/build-windows-exe.yml`).

The source package uses **Python 3.12**. If it is missing, install it with `py install 3.12`, then run the batch file again. Existing data is kept in `%LOCALAPPDATA%\SvaxClient` and is upgraded in place — instances, accounts, servers, builds and skins from 0.8.0 carry over.

`python packaging/build.py --onedir` builds a folder version instead, with Qt as separate files.

## What's new in 1.4.0

**A calmer, hand-made look**

- Flat neutral charcoal theme with one solid accent colour: no gradients, glows, glass panels or aurora backdrop any more. Corners are tighter (8–10 px), labels are in sentence case, and decorative extras (greeting kicker, glowing icon chips, the six quick-action tiles on Home, the light beam under the character) are gone.
- The right panel lists facts as quiet rows instead of tiles; the Home header shows one line of details instead of a row of pills.
- Accent colours are now solid: Green (default), Blue, Violet, Orange, Pink and Mono. Older accent choices are mapped automatically.
- All animations stay: page transitions, card cascades, hover lift, the sliding sidebar selection, toasts and the window intro.

**New logo and loading screen**

- The mark is now a pixel-font **S** built from Minecraft blocks. The loading screen drops the blocks into place one by one, then the name slides in. App icon, `.ico`, SVGs and the exe boot image were regenerated (`packaging/make_icons.py`).

**Schematics: browse online and see them in 3D**

- **Browse online** tab on the Schematics page: search the MineMev catalogue (the one the Litematic Downloader mod uses; its mirror at Choculaterie is used automatically when MineMev is unreachable), sort by newest, popular, most downloaded or oldest, page through results with thumbnails.
- Pick a build to see its author, downloads, game versions, tags, description and **files**. **Download** puts the file into your library; **Download & install** also copies it into the chosen instance. Downloads are checked to be real schematic files; sources that only link to their own website (or require an account) open in the browser instead.
- **3D preview** for every schematic (library, instance-only and online files): orbit with the mouse, zoom with the wheel, pan with right-drag, slice by **layer**, auto-rotate, and a **material list** with block counts. The build rises layer by layer when it opens. Large builds are simplified while you move the camera and drawn in full when you stop.
- Library cards of files without a built-in preview (Sponge, structure, WorldEdit) now show a rendered 3D picture.
- Reads Litematica, Sponge v1–v3, vanilla structure and legacy MCEdit/WorldEdit files.

**Fixes**

- Discover retries automatically the next time you open it after a network error, and sorts by relevance by default, so a typed search shows the best match first.
- Closing the 3D preview while it is still loading no longer leaves anything running.

## 1.3.0

**Schematics (Litematica)**

- A new **Schematics** page (sidebar, `Ctrl+7`) keeps your own library of `.litematic`, `.schem` (Sponge), `.schematic` (WorldEdit) and `.nbt` (structure) files.
- Cards show Litematica's own preview image, name, author, size (W×H×L), block count, file size and where each schematic is installed. Search, filter (library / only in instances) and sort by name, date or size.
- **Install to** any instance with one click: the file is copied into the instance's `schematics` folder, where Litematica loads it. Remove it again from the same card, or copy it to several instances from the right-click menu.
- Schematics that only exist inside an instance (for example ones you saved in game) are listed too and can be **added to the library**.
- **Import** files or `.zip` archives, drop them onto the window, or **Download from link** (a direct `https://` link; the file is checked to be a real schematic, up to 64 MB).
- Shows whether the chosen instance has **Litematica**, and installs Litematica (with its required library) from Modrinth in one click.
- Metadata is read with a streaming, bounded reader that skips block data, so huge schematics still open instantly.

**Also**

- The developer-only Microsoft/Azure setup was removed from Settings → Accounts; players just add their account.
- The sidebar hides its captions on short windows so all destinations fit (1366×768 laptops).

## 1.2.0

- **One `SvaxLauncher.exe`**: `Build-Windows.bat` now builds a single self-contained file (PyInstaller one-file build with Windows version details and a boot image shown while it unpacks, which hands over seamlessly to the animated loading screen).
- **Built-in sign-in application**: the launcher ships with the project's Azure application (client) ID, so players no longer need their own Azure app.
- **Clearer sign-in errors from the browser step**: an app limited to its own organisation (AADSTS50020), a wrong redirect URI (AADSTS50011), an unknown application ID (AADSTS700016) and a cancelled sign-in are explained with the exact fix.
- `MOJANG-URLAP.md` (Hungarian) helps fill in Mojang's Minecraft API access form; `public-page/` is a source-free README with screenshots for a public project page.

## 1.1.0

**Much faster**

- The interface no longer redraws itself constantly. The 3D character, the Home artwork, list hover effects and page changes were rebuilt to repaint only what changes (the character now renders ~40× cheaper, a page change costs ~20 ms instead of ~100 ms, a full window repaint ~25 ms instead of ~38 ms in the reference renderer).
- **Performance mode** (Settings → Appearance) for slower PCs: plain backdrop, no idle character motion and no light sweep on Play.

**Loading screen**

- An animated start-up screen: the logo draws itself, the wordmark rises in and a progress line follows start-up. The window then slides in and the first page cascades in.

**Right side panel (Modrinth-style)**

- *Playing as*: your account and skin head, account switching, or Sign in.
- *Selected instance*: artwork, loader and version, a big **PLAY** button with an instance switcher, play time, sessions, content and world counts, and quick buttons (folder, settings, add content, log, open).
- *Now playing* with timers and Stop, *Downloads* with live progress, *Your library* totals, *Servers* with live player counts, and launcher/Minecraft version facts.
- Toggle it from the top bar; it hides itself on narrow windows.

**Denser, richer menus**

- Smaller type and spacing everywhere, so every page shows more.
- **Home**: quick-action tiles (New instance, Modpacks, Import, Mod Builder, Wardrobe, Servers), *Jump back in* cards, **Recent worlds** across all instances with one-click Quick Play, compact patch notes, server tiles, popular mods and **Featured modpacks**.
- **Library**: a dense **list view** (loader, files, play time, last played, Play and menu per row) next to the card view, plus totals in the header.
- **Discover**: an image **card view** next to the list.
- Smaller version tiles (three per row), denser content and world rows.

**Sign-in that explains itself**

- Settings → Accounts had a four-step Azure checklist (removed again in 1.3.0; the application ID is now built in).
- Every sign-in failure says what to fix: an unapproved Azure app, a wrong redirect URI/account type, no Xbox profile, a child account, or an account that does not own Java Edition.

## 1.0.0 — the redesign

**A new look**

- **New logo**: an isometric Minecraft block whose edges trace an **S**. It is drawn live in the sidebar, so it follows your colour theme.
- **New colours**: a deep navy base with translucent "glass" surfaces over a softly blurred artwork backdrop, and **two-colour gradient themes** — Svax (mint → sky), Aurora, Ocean, Sunset, Lime and Frost. Older accent choices are mapped to the closest new theme.
- Gradient **PLAY** button with a glow and a periodic light sweep; it fills with progress while an instance installs.

**A new main menu (Home)**

- A full-width, cinematic stage: the artwork fades into the window, a greeting, the instance name in large type, glass detail chips and a **launch dock** — instance switcher, PLAY, folder and settings in one capsule.
- Your 3D character stands on a glowing platform with a name tag; the stage has gentle parallax while scrolling and a slow zoom-in when you arrive.
- Below: **Jump back in** artwork cards, **Quick connect** server tiles with live player counts, **Latest from Minecraft** image cards and popular Modrinth projects for the selected instance.

**Smoother motion**

- Page transitions: the old page lifts away while the new one rises in.
- Lists and grids fade in one card after another; cards lift with a soft shadow on hover.
- The sidebar selection is a glass pill that slides between destinations.
- Dialogs and menus fade and grow in; notifications slide in.

**Cleaner layout**

- Sidebar with icons *and* labels, recent instances and a live download ring.
- **Global search** in the top bar (**Ctrl+K**) searches Modrinth from any page.
- **Library** cards with the instance's release artwork, a floating Play button and the last-played time.
- **Instance** pages open with an artwork banner header.
- Redesigned theme picker, switches, chips, tabs, inputs, combo boxes, server avatars and news cards.

## Also new since 0.8.0 (0.9.0)

**A rebuilt interface**

- New layout: an icon sidebar with your most recent instances (with live "running" and "installing" dots), a top bar with Back/Forward, breadcrumbs, the running game and download progress, and your account with its skin head.
- **Home** is a Lunar-style stage: wide artwork, the selected instance, a large **Play** button with an instance switcher, and your 3D character next to it. Below: *Jump back in*, *Quick connect* servers, *Minecraft news* and popular mods for the selected instance.
- Modrinth-style **Library**, **Instance** pages, **Discover** with category filters, and full **project pages** (description, gallery, versions, links, compatibility).
- Bundled **Inter** typeface, a refined dark palette, smooth hover/selection animations, sliding tab indicators, skeleton loading, toast notifications instead of pop-up boxes, and a dark native title bar on Windows.
- **Accent themes** (Settings → Appearance). Drag & drop `.mrpack`, backup `.zip`, mod `.jar`, resource pack `.zip` or skin `.png` files anywhere on the window.

**The launcher stays usable while Minecraft runs**

- Previously the whole window was locked until the game closed. Now games run in the background: browse, install, or start a *different* instance at the same time.
- **Stop** a game from Home, the instance page or the top bar. **Live game log** with colour-coded warnings/errors, filtering, copy and crash-report viewer.
- Crashes are detected and reported with a shortcut to the log or crash report. Launch failures (sign-in, downloads) appear as notifications.
- Choose what the launcher does when a game starts: keep open, minimize, or hide until the game closes.
- Downloads and installs run in a background queue with a progress ring in the sidebar and a task list.

**More Minecraft**

- **Every Minecraft release** is available (not only 1.21.11+), plus optional **snapshots**.
- New mod loaders: **NeoForge** and **Quilt** next to Fabric, Forge and Vanilla. Quilt instances also accept Fabric mods.
- **Modrinth modpacks**: browse and install them from Discover, or import any `.mrpack`. Export any instance as a `.mrpack`.
- **Restore backups** as a new instance (previously manual).
- **Delete instances** (with confirmation).

**Better content management**

- Files you dropped into `mods`, `resourcepacks` or `shaderpacks` by hand are now shown, and **Identify local files** matches them to Modrinth by hash.
- **Check for updates** compares installed files with Modrinth in one request; update one project or **Update all**. Install a specific version from a project's Versions tab.
- Filters for enabled, disabled, local files and updates; per-type counts.

**Worlds, screenshots and servers**

- **Worlds** tab: every singleplayer world with name, game mode, version and last played time, one-click **Play** (Minecraft 1.20+), back up, open or remove.
- **Screenshots** tab: a thumbnail gallery with a full-size viewer (←/→, copy, save copy, delete).
- **Servers** show the coloured server description (MOTD), players, ping and version. **Import** servers from an instance's own multiplayer list. Choose which instance joins.

**Per-instance settings**

- Name, icon, colour, pin; memory; Java executable; extra JVM arguments; game window size and fullscreen; loader version selection and **Repair installation**.
- Global defaults: memory slider with a recommendation based on your PC's RAM, Java, JVM arguments and window size.

## Play and instances

Create an instance with **+** in the sidebar, **New instance** in the Library, or **Ctrl+N**. Pick a loader (Vanilla, Fabric, Quilt, Forge, NeoForge), a game version, a name, colour and optionally an icon and memory. Loader availability is checked before the instance is created. The **Import** tab takes a `.mrpack` modpack or a Svax backup.

Press **Play** on Home, a library card (hover it for the round Play button), the instance page, or press **Ctrl+Enter**. Missing game files, the loader and the correct Java runtime are downloaded automatically on the first launch. The Microsoft session is refreshed before every launch.

Each instance has its own mods, worlds, screenshots, options and logs. Game libraries and Java runtimes are shared between instances.

## Discover and modpacks

Discover lists **Modpacks**, **Mods**, **Resource packs** and **Shaders** from Modrinth. Mods are filtered for the chosen instance's game version and loader; categories, sort order and paging work like the Modrinth website. Click a result to open its project page, or press **Install**. Required dependencies are resolved automatically. Downloads must come from Modrinth's CDN and are verified by size and SHA-512.

Installing a **modpack** downloads its `.mrpack`, creates a new instance with the exact Minecraft and loader version, downloads every file (only from `cdn.modrinth.com`, `github.com`, `raw.githubusercontent.com` or `gitlab.com`, verified by SHA-512), and copies the pack's configuration overrides. Paths in a pack can never write outside the new instance.

## Mod Builder

1. Choose a Minecraft version and Fabric, Quilt, Forge or NeoForge.
2. Search compatible mods and add them, or begin with a starter set (Performance, Shaders, Everyday essentials, Map & HUD).
3. **Save** the collection, **Build instance**, or **Export** it as a Svax recipe (`.json`) or a Modrinth pack (`.mrpack`).

A build keeps mods as separate files; it does not merge JARs or include Lunar Client's proprietary modules.

## Schematics

**Browse online** searches the MineMev catalogue (www.minemev.com, with the api.choculaterie.com mirror as fallback; the same public API the open-source [Litematic Downloader](https://github.com/Choculaterie/LitematicDownloader) mod uses). Downloaded files land in your library. **3D preview** (on cards, in the details panel, in the right-click menu and for online files) shows the build with layers and a material list; online files are previewed from a temporary copy in `cache\schematic-preview` and only added to the library when you press Download.

The library lives in `%LOCALAPPDATA%\SvaxClient\schematics`. Installing copies a file into `<instance>\schematics` (Litematica's folder); removing it from an instance moves that copy to the instance's `removed` folder, and removing it from the library moves it to `SvaxClient\removed\schematics`. In game, open Litematica's menu (default key **M**) → *Load Schematics*.

## Skins

- The left panel always shows a large 3D preview. Click any skin to **try it on** without changing your account.
- **Discover** browses the MineSkin community catalogue (search, quick tags, paging). **Wardrobe** shows your saved skins.
- **Use this skin** uploads it to your Minecraft account. **Save**, **PNG** download, Classic/Slim model, **From username** and **Import PNG** (64×64 or 64×32, up to 1 MB) are available.

## Servers

Saved servers show icon, description, players, ping and version; status is queried directly with bounded timeouts. **Import** reads the selected instance's `servers.dat`. The first three servers also appear on Home. Joining uses Minecraft's Quick Play with the instance selected at the top of the page.

## Settings and shortcuts

Settings are saved automatically: Appearance (accent colour, animations, performance mode, Home background), Game & Java, Launcher (window behaviour when a game starts, snapshots), Accounts, Storage (data folder, disk usage, clear cache) and About.

| Shortcut | Action |
| --- | --- |
| Ctrl+N | New instance |
| Ctrl+K | Search Modrinth from anywhere |
| Ctrl+F | Search on the current page |
| Ctrl+Enter | Play the selected instance |
| Ctrl+1 … Ctrl+8 | Home, Library, Discover, Skins, Servers, Builder, Schematics, Versions |
| Alt+← / Alt+→ | Back / Forward |
| F5 | Refresh the current page |
| Ctrl+, | Settings |
| Space / Delete | Toggle / remove the selected content file |

The minimum window size is 1000×660; pages reflow and the Discover filters collapse on narrow windows.

## Microsoft setup — before online play or skin upload

The launcher never borrows another launcher's application ID. The project's own application ID is built in (`svax/build_config.py`); players simply press **Add account**. The one-time setup below is for whoever owns that application (in Hungarian: `TELEPITES-ES-BEJELENTKEZES.md`):

- Register a public-client application with Microsoft whose supported account types include **personal Microsoft accounts** (not “Only your own organization”).
- Configure the desktop/mobile redirect URI **http://localhost:8976/callback**.
- Request Minecraft API access for that application; registration alone may not be sufficient.
- Put its Application (client) ID into `svax/build_config.py` before building (a `client_id` in `settings.json` overrides it), then **Add Microsoft account**.
- The sign-in listener binds to `127.0.0.1:8976` and expires after three minutes.

Login uses PKCE and OAuth state validation. Refresh tokens are kept in Windows Credential Manager through keyring, separately for each application/account pair, never in the settings file. An unapproved application may fail with `AzureAppNotPermitted`.

Reference: https://minecraft-launcher-lib.readthedocs.io/en/latest/tutorial/microsoft_login.html

## Data and validation

Data remains in `%LOCALAPPDATA%\SvaxClient`: settings, instances, builds, skins, shared runtime, backups and caches. Removed content and worlds go to the instance's `removed` folder first. The source archive contains no account tokens, personal instances, downloaded mods or saved skins. The preview images were rendered from temporary demonstration data.

See **VALIDATION.md** for what was tested and what still needs a Windows/Minecraft account test, **RESEARCH.md** for design references and **THIRD-PARTY.md** for credits and licences.

Not an official Minecraft product. Not approved by or associated with Mojang or Microsoft. Modrinth and Lunar Client are not affiliated with Svax Launcher.
