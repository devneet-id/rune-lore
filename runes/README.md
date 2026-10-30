# Runes

> The ten origin runes. Read the [Acts](../README.md) to learn them step by step; come here to look things up.

Every rune is a folder of five files: **Ether** (constants), **Essence** (globals), **Entity** (functions — the logic), **Manifest** (the static class your runite calls) and **Phantasm** (the contract you are reading here).

| Rune | Purpose | Introduced in | Version | Mark | Nodes |
|---|---|---|---|---|---|
| [Aether](aether.md) | Represents the foundational flow that permeates all components | Act 0 · The Void | `1.18` | `VOID` | 51 |
| [Whisper](whisper.md) | Handles user-facing output through styled messages, prompts, and echoes | Act 0 · The Void | `1.13` | `VOID` | 34 |
| [Weaver](weaver.md) | Built for advanced string manipulation, data binding, and template weaving | Act 0 · The Void | `1.7` | `VOID` | 27 |
| [Chanter](chanter.md) | Encapsulates processes and CLI-style operations to maintain immutability | Act 0 · The Void | `1.14` | `VOID` | 33 |
| [Forger](forger.md) | Built for structured file and directory operations such as tracing, scanning, fixing, moving, and cloning | Act 1 · First Resonance | `1.14` | `VOID` | 29 |
| [Cipher](cipher.md) | Keeps secrets and identities of the system | Act 1 · First Resonance | `1.6` | `VOID` | 15 |
| [Keeper](keeper.md) | Handles persistent message tracking, data logging, and structured memory management | Act 1 · First Resonance | `1.13` | `VOID` | 36 |
| [Crafter](crafter.md) | Focused on dynamic creation and composition | Act 2 · Understanding Its Flow | `1.13` | `VOID` | 36 |
| [Specter](specter.md) | Enables out-of-process operations through soul-like abstractions | Act 3 · Liberation of Forte | `1.9` | `VOID` | 30 |
| [Minister](minister.md) | Speaks with a familiar (an AI spirit) on behalf of the runite | Act 3 · Liberation of Forte | `0.3` | `DEVELOPMENT` | 9 |

**Version=** in the footer of every cast: the major of `AETHER_VERSION`, then its minor plus the sum of the rune majors, then the sum of the rune minors — all whole numbers (`1.20.110` today). See [Versioning](../acts/4-the-beyond/versioning.md).
