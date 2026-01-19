
# tiicu

> The first custom emulation frontend for Nintendo Switch - a beautiful, intuitive interface built entirely in pure C++ for native performance and future cross-platform compatibility.

![Status](https://img.shields.io/badge/status-alpha-orange) ![Platform](https://img.shields.io/badge/platform-Switch-red) ![License](https://img.shields.io/badge/license-Closed%20Source-lightgrey)

## What is tiicu?

**tiicu** is a groundbreaking emulation frontend designed specifically for Nintendo Switch homebrew. It transforms how you organize and play retro games with an elegant, controller-first interface that puts your games front and center.

Unlike traditional emulator launchers that force you through endless file browsers and configuration menus, tiicu provides a console-quality experience with automatic game organization, beautiful artwork handling, and embedded emulator cores that just work.

### Screenshots

**Home Intro** ![Home Intro](https://github.com/tiicu/tiicu/blob/main/images/home.jpg?raw=true)

**Homescreen** ![Homescreen](https://github.com/tiicu/tiicu/blob/main/images/homescreen.jpg?raw=true)

**Console Selection** ![Launch Consoles](https://github.com/tiicu/tiicu/blob/main/images/consoles-launch.jpg?raw=true)

**SNES Game Library** ![Launch SNES](https://github.com/tiicu/tiicu/blob/main/images/snes-launch.jpg?raw=true)

**PlayStation Game Library** ![Launch PSX](https://github.com/tiicu/tiicu/blob/main/images/psx-launch.jpg?raw=true)

## Core Features

### Home Screen

Your personalized gaming dashboard with instant access to favorites.

-   **Customizable Grid Layout** - Pin your most-played games for one-button access
-   **Full Shortcut Management** - Edit game information or remove shortcuts as your collection evolves
-   **Visual Excellence** - Every game displays with proper artwork and console-specific presentation

### Launcher Screen

A powerful interface for browsing your entire retro library across multiple systems.

-   **Unified Multi-Console Browser** - Access all your games from Game Boy to PlayStation in one place
-   **Intelligent Caching** - Game lists load instantly thanks to smart background indexing
-   **One-Button Rescan** - Added new ROMs? Refresh your library without rebuilding everything
-   **Direct Home Screen Pinning** - Add any game to your home screen with a single button press
-   **No-Intro and Redump Organization** - Automatic categorization using No-Intro and Redump naming standards

### Embedded Emulator Cores

Zero-configuration retro gaming with everything included out of the box.

-   **No Manual Installation** - All emulator cores are built-in and ready to use
-   **Six Systems at Launch**:
    -   Game Boy
    -   Game Boy Color
    -   Game Boy Advance
    -   Super Nintendo Entertainment System
    -   PlayStation (custom exclusive port optimized for Switch)
    -   PlayStation Portable via PPSSPP (custom exclusive port)
-   **Full Save Support** - Save states work everywhere, SRAM saves function like original hardware
-   **Optimized for Switch** - Custom builds tuned for maximum performance on Switch hardware

### Automatic Artwork System

Professional-looking game cards without Photoshop or manual editing.

-   **Zero Template Hassle** - Drop in raw cover images and tiicu does the rest
-   **Console-Specific Bezels** - Automatically applied frames matching each system's aesthetic
-   **Consistent Library Appearance** - Every game gets polished, uniform presentation
-   **Hero Images Supported** - Full background artwork for featured games

### Organized File Structure

Everything has its place with a logical, hierarchical folder system.

-   **Context-Based Organization** - Separate folders for covers, heroes, saves, and save states
-   **Per-Console Subfolders** - Each system gets dedicated directories preventing file conflicts
-   **Easy Maintenance** - Backup saves or manage artwork without digging through messy folders

## Why tiicu?

### Built for Switch First

While other frontends attempt to be everything for everyone, tiicu is laser-focused on delivering the best possible experience on Nintendo Switch homebrew. Every design decision prioritizes controller navigation, handheld performance, and the unique characteristics of Switch hardware.

### Pure C++ Architecture

tiicu is built from scratch in modern C++ for maximum performance and portability. No heavy frameworks, no interpreted languages - just efficient native code that respects your system's resources while delivering smooth 60fps UI navigation.

### Controller-First Philosophy

Touch controls are an afterthought. tiicu is designed around the assumption that you're using physical buttons. Every menu, every option, every interaction is optimized for controller input.

### Automatic Organization

Stop manually sorting ROMs into folders. tiicu intelligently categorizes games based on No-Intro naming conventions, recognizing regions, versions, and special editions automatically.

## Development Roadmap

### Currently Implemented ✓

-   [x] Core UI framework with grid and list views
-   [x] Home screen with customizable shortcuts
-   [x] Launcher with multi-console support
-   [x] Embedded emulator cores (GB, GBC, GBA, SNES, PS1, PSP)
-   [x] Save state system
-   [x] SRAM save handling
-   [x] Automatic artwork processing
-   [x] Intelligent game caching
-   [x] Organized folder structure

### In Active Development

-   [ ] Enhanced home screen widgets and animations
-   [ ] Media management for screenshots and GIFs
-   [ ] Online asset services for community-curated artwork
-   [ ] Automatic asset downloader
-   [ ] Additional emulator cores

### Planned Features

-   [ ] RetroAchievements integration
-   [ ] Playlist/collection management
-   [ ] Advanced filtering and search

## Repository Purpose

Since tiicu is **closed source**, this repository serves as the central hub for:

-   **Official Releases** - Download stable builds and test versions
-   **Development Updates** - Track progress and upcoming features
-   **Issue Tracking** - Report bugs and request features
-   **Community Discussion** - Share feedback and suggestions

We believe in maintaining development control while fostering an engaged community through transparent communication and active feedback collection.

## Installation

1.  Download the latest release from the [Releases](https://github.com/tiicu/tiicu/releases) page
2.  Extract the archive to your Switch SD card 
3.  Place your ROM files in the appropriate folders (ex.: sdmc:/tiicu/roms/snes)
4.  Launch tiicu from the homebrew menu

## Platform Support

**Current Platform:** Nintendo Switch (homebrew)

**Future Possibilities:** The pure C++ architecture makes tiicu inherently portable. Future platform support will be determined by community demand through polls and feedback. Potential targets include Windows, macOS, Linux, Android, and other gaming devices.

## Community

Join our Discord server for support, updates, and discussion:

[Discord Server](https://discord.gg/ADVaC3SvZE)

## Concept Inspiration

tiicu draws conceptual inspiration from iiSU's design philosophy of clean, minimal interfaces focused on playing games rather than managing files. While iiSU remains closed source, tiicu is our own ground-up implementation bringing similar ideas to the Switch homebrew community.

## About the Developer

Hi, I'm **Dan**, a 31-year-old developer with 16 years of programming experience. My background is primarily web development, but tiicu represents my personal challenge to master C++ and low-level game development.

This project combines my lifelong passion for retro gaming with the technical goal of creating a polished, professional-grade application in C++. Building tiicu has been an incredible learning experience, and I'm excited to share it with the homebrew community.

## Legal Notice

tiicu is distributed with emulator cores but does not include:

-   BIOS files or system files
-   Copyrighted games or ROMs
-   Methods to circumvent copy protection or DRM

Users are responsible for legally obtaining games, required system files, and using emulators in compliance with their local laws. tiicu is intended for use with legally owned game backups and homebrew software only.

## Acknowledgments

-   Concept inspired by iiSU's design philosophy
-   Built for the Nintendo Switch homebrew community
-   Special thanks to all alpha testers and early supporters
-   Gratitude to the emulator development community whose cores make this possible

----------

**Disclaimer:** This project is not affiliated with or endorsed by Nintendo. Nintendo Switch is a trademark of Nintendo Co., Ltd. tiicu is an independent homebrew application.

**Closed Source Notice:** tiicu is proprietary software. Source code is not available for public distribution or modification. This repository exists solely for community engagement, release distribution, and issue tracking.
