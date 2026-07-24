# Development Plan — SOG Launcher

This document details the phases and tasks required to configure the auto-updating launcher utilizing Packwiz.

---

## 🎯 Workflow Rules
- [ ] **Ignored Filters**: Protect local configuration and saves of the player (`options.txt`, `saves/`, `xaerowaypoints/`) using the `ignore` section in `pack.toml`.
- [ ] **Automatic Indexing**: Always execute `.\packwiz.exe refresh` after modifying or adding local files (private mods, configs, quests) to update `index.toml`.

---

## 📋 Phased Roadmap

### Phase 1: Distribution & Auto-Updating Instance (Packwiz) (Pending)
- [ ] **Configuration and Deployment of the Synchronized Instance**:
  - [ ] **Step 1a**: Create the dedicated Git repository for the modpack (`sog-experience-launcher`) to host the Packwiz metadata (`pack.toml` and `index.toml`).
  - [ ] **Step 1b**: Generate TOMLs for external mods (Cobblemon, FTB, Xaero) and index the internal mod `cobbleadditions-0.9.1.jar` under `/custom/`.
  - [ ] **Step 1c**: Configure exclusion filters (`ignore` and `untracked`) to protect local player preferences, volume settings, controls, and shaders.
  - [ ] **Step 1d**: Sync the global server waypoints file `normal.txt` and package the instance with the pre-launch command in Prism Launcher.
