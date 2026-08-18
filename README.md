# WebGL-AGENTS

An agent skill that answers WebGL questions by referencing locally cloned official repositories,
rather than relying solely on training data. It is agent-agnostic and works with any coding agent
that supports skills (Claude Code, Codex, etc.).

### Reference repos included

| Repo | Purpose |
|------|---------|
| `references/WebGL` | Khronos WebGL 1/2 specifications, extensions, and conformance suite |
| `references/WebGLSamples` | Classic runnable WebGL examples |
| `references/WebGL2Samples` | Focused WebGL 2 examples |
| `references/WebGLFundamentals` | Conceptual lessons and focused examples |
| `references/ANGLE` | Browser-facing OpenGL ES implementation and tests |

## Installation

Install once into the shared agent skills directory, then symlink it into each agent's skills folder.

The reference repos are git submodules. Initialize them one level deep only — they are read-only
references that are never built, so nested build dependencies are pure overhead:

```bash
git clone git@github.com:rygo6/WebGL-AGENTS.git ~/.agents/skills/webgl
cd ~/.agents/skills/webgl
git submodule update --init
git submodule update --remote
```

Do not pass `--recursive` or clone with `--recurse-submodules`. ANGLE's own nested submodules pull
roughly 12 GB of Chromium build dependencies that this skill never references, and they fail outright
on `chrome-internal.googlesource.com`, which is not publicly reachable. If you have already recursed
into ANGLE and want the space back:

```bash
git -C references/ANGLE submodule deinit --all -f
rm -rf .git/modules/references/ANGLE/modules
```

Then link it into the agents you use:

```bash
mkdir -p ~/.claude/skills ~/.codex/skills
ln -s ~/.agents/skills/webgl ~/.claude/skills/webgl
ln -s ~/.agents/skills/webgl ~/.codex/skills/webgl
```

On Windows, use `mklink /J` to create a junction instead (run in `cmd`, no admin rights needed):

```bat
mklink /J "%USERPROFILE%\.claude\skills\webgl" "%USERPROFILE%\.agents\skills\webgl"
mklink /J "%USERPROFILE%\.codex\skills\webgl"  "%USERPROFILE%\.agents\skills\webgl"
```

## Usage

Once installed, invoke `/webgl` from any agent that supports skills.

## Related skills

Use `opengl` for native OpenGL and OpenGL ES, `metal` for Apple Metal, `vulkan` for Vulkan and
MoltenVK, and `webxr` when WebGL is used through WebXR-specific bindings.
