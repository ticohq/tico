# TECHNICAL STATEMENT: STATIC LINKING OF EMULATOR CORES ON NINTENDO SWITCH PLATFORM

## PURPOSE

This statement addresses the technical implementation of emulator core integration in tiicu's Nintendo Switch builds and responds to allegations regarding licensing compliance. This is provided for transparency and to establish the factual and legal basis for our current implementation approach.

---

## ARCHITECTURAL PHILOSOPHY

**It is neither the purpose nor virtue of tiicu to embed emulator code within our application.**

tiicu is designed as a **frontend application**—a launcher and library management system that interfaces with emulator cores as separate, independent components. We have no interest in, and will never pursue, embedding emulator code directly into our application.

### LibRetro API Architecture

Communication between tiicu and emulator cores is accomplished **exclusively through the LibRetro API**, an industry-standard, open interface specification that provides clean separation between frontend applications and emulator cores. This architecture is used by numerous emulation frontends (RetroArch, EmulationStation, and others).

**Key Technical Facts:**

1. **Standardized Interface**: tiicu communicates with emulator cores through the LibRetro API's defined function calls and callbacks, not through direct code integration
2. **Separation of Concerns**: Clear separation between frontend responsibilities (UI, library management, input handling) and core responsibilities (emulation logic, ROM loading)
3. **Core Independence**: Emulator cores are standalone components that work with any LibRetro-compatible frontend—they are not "part of" tiicu
4. **No Code Modification**: tiicu does not modify, alter, or embed emulator core source code

---

## CURRENT IMPLEMENTATION ACROSS PLATFORMS

### Dynamic Loading (Preferred Architecture)

**tiicu ALREADY FULLY SUPPORTS DYNAMIC LOADING on macOS, Linux, Windows, and Android.**

The tiicu codebase contains complete, functional implementations for dynamically loading LibRetro cores as separate shared libraries:

- **macOS**: Loads cores as .dylib files at runtime
- **Linux**: Loads cores as .so files at runtime  
- **Windows**: Loads cores as .dll files at runtime
- **Android**: Loads cores as shared libraries at runtime

This dynamic loading functionality is already implemented, tested, and fully operational.

### Nintendo Switch: Static Linking (Temporary)

**Static linking is used EXCLUSIVELY on Nintendo Switch alpha builds, and ONLY due to platform limitations.**

As a team new to homebrew development, static linking was our initial approach when bringing tiicu to the Nintendo Switch platform. At the time, we were unaware of alternative architectures available in the homebrew ecosystem.

**Critical Points:**

- **Platform-specific**: Used ONLY on Switch
- **Learning Curve**: Our first approach as newcomers to homebrew development
- **Not a design choice**: We've now discovered better solutions
- **Temporary**: Being replaced with chain-loading architecture
- **Contradicts our implemented architecture**: Our actual codebase uses dynamic loading everywhere else

**Important Distinction: Static Linking ≠ Code Embedding**

Static linking is a compilation and linking methodology, not code embedding:

- Emulator core code remains separate and independent in source form
- Communication occurs through the LibRetro API interface
- Cores are not modified or merged into tiicu's codebase
- Static linking is purely a build-time artifact on Switch

---

## WHY STATIC LINKING WAS USED ON SWITCH

**As newcomers to Nintendo Switch homebrew development, we initially used static linking because:**

1. **Limited Experience**: We were new to the homebrew ecosystem and its capabilities
2. **First Approach**: Static linking was the most straightforward method we understood initially
3. **Platform Constraints**: The Switch homebrew environment does not support dynamic linking in the traditional sense (loading .dll/.so/.dylib files at runtime)

**Recent Discovery:**

We have recently learned that libnx (the Nintendo Switch homebrew library) supports **NRO chain loading**—the ability for one homebrew application to launch another. This discovery changes everything and enables us to eliminate static linking entirely.

---

## EVIDENCE OF GOOD FAITH AND PROPER DESIGN

**The fact that tiicu already implements dynamic loading on all other platforms definitively proves:**

1. **Architectural Intent**: Our design philosophy prioritizes separation and dynamic loading
2. **Good Faith Compliance**: We implemented proper architecture on all platforms where we understood how
3. **Learning and Adaptation**: As we learn more about Switch homebrew, we're adapting our approach
4. **Technical Competence**: We have the knowledge and capability to implement proper separation
5. **Licensing Respect**: Our implementation demonstrates respect for component independence

**Any allegation that we are "trying to embed emulator code" or "avoid licensing through static linking" is contradicted by:**

- Dynamic loading already works on four major platforms
- Our immediate pivot to chain-loading upon learning it's possible
- Our status as newcomers learning the homebrew ecosystem
- Our investment in community infrastructure (detailed below)

---

## TRANSITION TO CHAIN-LOADING ARCHITECTURE

**Now that we've discovered libnx supports NRO chain loading, we are actively transitioning to this architecture.**

### What Chain-Loading Enables

- Launch emulator cores as separate, independent homebrew applications (.nro files)
- Eliminate static linking completely on Switch
- Maintain LibRetro API communication between separate processes
- Bring Switch implementation in line with our existing dynamic loading architecture
- Provide perfect separation between frontend and emulator components

### Implementation Status

This transition is already underway and will be implemented in upcoming Switch releases. Chain-loading will allow tiicu to launch cores as standalone homebrew applications, achieving the same separation we already have on other platforms.

---

## COMMUNITY CONTRIBUTION: THE LIBRETRO-NX INITIATIVE

**tiicu is the first custom LibRetro frontend for Nintendo Switch**, and we're committed to improving the entire ecosystem beyond our own project.

### Purpose of libretro-nx

We are establishing the **libretro-nx organization** (https://github.com/libretro-nx) to engage the community around ports, patches, and maintenance of LibRetro cores exclusively for Nintendo Switch.

**Goals:**

1. **Centralized Development**: Dedicated organization for Switch-specific LibRetro core development
2. **Community Collaboration**: Enable contributions for ports, patches, optimizations, and bug fixes
3. **Regular Updates**: Keep cores up-to-date with upstream LibRetro development
4. **Open Development**: Maintain all cores as open-source with public repositories
5. **Quality Assurance**: Establish testing, documentation, and quality standards

### Problems in the Current Switch LibRetro Ecosystem

The libretro-nx initiative addresses serious issues:

**1. Minimal Maintenance:**
- Switch cores maintained by only a handful of developers
- Many cores not updated in months or years
- Bug fixes from upstream rarely ported to Switch
- Limited resources mean slow response to issues

**2. Infrequent Updates:**
- Cores lag significantly behind upstream
- Performance improvements and new features delayed or never implemented
- Users stuck with outdated, buggy versions

**3. Patreon Paywall Distribution:**
- Some developers distribute Switch cores through Patreon paywalls
- Users must pay monthly subscriptions for cores that should be freely available
- Highly problematic for GPL-licensed cores requiring free distribution
- Creates artificial scarcity and fragments the community
- May constitute GPL license violations

### Our Commitment to Open Development

By establishing libretro-nx, we demonstrate commitment to:

- **Free and open distribution** of all cores
- **Transparent development** with public repositories
- **Community collaboration** rather than gatekeeping
- **Licensing compliance** with proper open-source practices
- **Ecosystem health** for all Switch homebrew users

**This benefits the entire Switch homebrew community**, not just tiicu users. Cores developed through libretro-nx will work with any LibRetro-compatible frontend.

---

## CORE MODIFICATIONS AND SOURCE CODE AVAILABILITY

**tiicu does not modify emulator core source code.** We utilize cores as-provided through their LibRetro API implementation.

**If modifications become necessary** for Switch-specific compatibility, bug fixes, ABI updates, JIT settings, or performance improvements, **all such modifications will be developed and maintained through the libretro-nx organization**, not as part of tiicu.

### Principles for Any Core Modifications

1. **Separation of Concerns**: Modifications developed independently through libretro-nx, not integrated into tiicu
2. **Full Source Code Disclosure**: All modified core source code published in public libretro-nx repositories
3. **Community Benefit**: All modifications available to the entire Switch homebrew community
4. **Patch Documentation**: Clear documentation of modifications and rationale
5. **Upstream Contribution**: Patches submitted upstream when appropriate
6. **GPL Compliance**: Full compliance with GPL and other open-source licenses
7. **Multi-Frontend Support**: Modified cores remain compatible with any LibRetro frontend

**We will not keep any core modifications private or proprietary.**

### Relationship to tiicu's Architecture

The libretro-nx initiative further demonstrates our commitment to proper separation:

- **Independent Core Development**: Cores developed through libretro-nx are completely independent of tiicu
- **Multi-Frontend Support**: All cores work with any LibRetro frontend
- **Chain-Loading Ready**: Cores can be packaged as standalone .nro applications
- **Open Source Compliance**: Public repositories ensure transparency
- **Community Ownership**: Designed for community contribution, not proprietary control

**This is the opposite of embedding cores—we are investing in an independent, open ecosystem.**

---

## LEGAL POSITION AND GPL COMPLIANCE

### Good Faith and Architectural Integrity

We are acting in complete good faith to maintain proper separation. The evidence:

- Dynamic loading already implemented on macOS, Linux, Windows, and Android
- Static linking on Switch was our initial approach as newcomers to homebrew
- Now transitioning to chain-loading after discovering it's possible
- Investing in community infrastructure (libretro-nx) that benefits everyone
- Any necessary core modifications handled independently through libretro-nx

### LibRetro API Compliance

Our use of the LibRetro API is consistent with its intended purpose across all platforms. The API's separation between frontend and cores is maintained universally—only the linking methodology differs temporarily on Switch.

### No Code Embedding or Modification

We do not embed, modify, merge, or integrate emulator core source code into tiicu on any platform. Static linking on Switch is purely a build-time artifact of platform limitations and our initial understanding, not a design decision.

### GPL Compliance Commitment

For cores licensed under GPL or other open-source licenses, we are committed to:

1. **Proper Separation**: Cores are separate components, not integrated into tiicu
2. **Clean API Boundaries**: LibRetro API maintained across all platforms
3. **No Modification Within tiicu**: Any modifications handled through libretro-nx
4. **Source Code Availability**: GPL-licensed components available from original developers or libretro-nx
5. **Chain-Loading Architecture**: Eliminates static linking concerns entirely
6. **Public Disclosure**: Any modifications transparently disclosed through libretro-nx repositories

### What We Will Not Do

We will not open-source tiicu's codebase in response to demands from individuals who lack legal standing.

**Key Legal Principle:** The GPL, if applicable to specific LibRetro cores, requires disclosure of modified GPL code—not the entire project's proprietary frontend code.

Since we:
- Do not modify core code within tiicu
- Only interface through the LibRetro API
- Already use dynamic loading on four major platforms
- Use static linking on Switch only due to initial platform understanding (now being replaced)
- Support independent core development through libretro-nx
- Will handle any core modifications through libretro-nx, not within tiicu

Our obligations would be limited to:
- Providing source for specific cores (available from original developers or libretro-nx)
- Publicly disclosing any core modifications through libretro-nx repositories
- Potentially providing build scripts for linking cores on Switch (during transition period)
- NOT providing tiicu's frontend source code, which is separate and independent

### Third-Party Standing

Individuals who are not copyright holders or developers of LibRetro emulator cores lack legal standing to assert licensing claims. Licensing matters are between tiicu developers and actual emulator core developers—not third parties.

Our investment in libretro-nx demonstrates our willingness to work directly with core developers and the community to ensure proper practices and licensing compliance.

---

## TECHNICAL ROADMAP

### Current Status
- Dynamic loading fully implemented on macOS, Linux, Windows, Android
- Static linking used on Switch alpha builds (initial approach as newcomers)
- Chain-loading architecture discovered and transition underway
- Communication through LibRetro API maintained across all platforms
- No core modifications within tiicu codebase
- libretro-nx organization being established

### Short-term (Switch Alpha → Beta)
- Implementation of chain-loading architecture on Switch
- Complete elimination of static linking on Switch
- Emulator cores run as separate .nro applications
- LibRetro API communication between separate processes
- Launch of libretro-nx with initial core ports

### Medium-term (Community Development)
- Active development and maintenance through libretro-nx
- Community contributions to core ports and optimizations
- Regular updates to sync Switch cores with upstream LibRetro
- Elimination of Patreon paywall distribution through free alternatives
- Transparent disclosure of all modifications through libretro-nx

### Future (All Platforms)
- Fully modular architecture across all platforms
- Maximum separation and independence universally
- Consistent LibRetro API implementation
- Thriving community ecosystem for Switch core development

---

## ARCHITECTURAL COMMITMENT

**We categorically state:**

1. tiicu will **never embed emulator code** within the application
2. All communication with cores occurs **through the LibRetro API** on every platform
3. **Dynamic loading is already implemented** on macOS, Linux, Windows, and Android
4. Static linking on Switch was **our initial approach as newcomers to homebrew development**
5. We are **actively eliminating static linking** through chain-loading (now that we know it's possible)
6. Our design philosophy **prioritizes separation**, not integration
7. We are **investing in independent community infrastructure** (libretro-nx)
8. We **oppose proprietary gatekeeping** practices like Patreon paywalls
9. tiicu **does not modify emulator cores**; any necessary modifications handled through libretro-nx
10. tiicu is **the first custom LibRetro frontend for Nintendo Switch**

**Our existing implementation on four platforms, combined with our immediate pivot to chain-loading upon discovering it's possible, and our investment in libretro-nx, is irrefutable proof of our good faith and commitment to open-source principles.**

---

## CONTACT FOR EMULATOR DEVELOPERS

LibRetro emulator core developers with questions or concerns are encouraged to contact us directly:

**ticolauncher@proton.me**

We are committed to working cooperatively with all rights holders to ensure proper licensing compliance and architectural integrity.

**We invite core developers to participate in the libretro-nx initiative** to ensure their cores are properly maintained, updated, and distributed for Nintendo Switch.

**Third parties who are not rights holders should refrain from making licensing demands, particularly when:**
- Those demands ignore our existing proper implementation on four platforms
- Those demands ignore our status as newcomers learning homebrew development
- Those demands ignore our investment in community infrastructure
- Those demands ignore that any core modifications are handled through libretro-nx
- Those demands are based on misunderstanding of temporary platform-specific constraints

---

## CONCLUSION

**The facts are clear:**

- tiicu already fully supports dynamic loading on macOS, Linux, Windows, and Android
- Static linking on Switch was our initial approach as newcomers to homebrew development
- We recently discovered libnx supports NRO chain loading
- We are immediately transitioning to chain-loading to eliminate static linking
- tiicu is the first custom LibRetro frontend for Nintendo Switch
- We are investing in libretro-nx to improve the entire Switch LibRetro ecosystem
- tiicu does not modify cores; any necessary modifications handled through libretro-nx
- We oppose problematic practices like Patreon paywall distribution

tiicu's architecture is fundamentally based on the LibRetro API, providing clean separation between frontend and cores across all platforms. This separation is maintained regardless of linking methodology and is already properly implemented through dynamic loading on every platform we initially understood.

**Our immediate pivot to chain-loading upon learning it's possible, combined with our investment in community infrastructure, demonstrates our commitment to proper separation, open-source principles, and ecosystem health.**

We remain committed to full licensing compliance with all legitimately applicable requirements across all platforms.

---

**Last Updated:** 02/02/2026
**Architecture:** LibRetro API-based Frontend  
**Dynamic Loading Status:** Fully implemented on macOS, Linux, Windows, Android  
**Switch Status:** Alpha (static linking) → Transitioning to chain-loading (NRO chain loading)  
**Community Initiative:** libretro-nx organization - https://github.com/libretro-nx  
**Contact:** ticolauncher@proton.me
