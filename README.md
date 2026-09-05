# WebGL-AGENTS

An agent skill that answers WebGL questions using local specifications, examples, and ANGLE source.
It works with coding agents that support skills.

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

The reference repositories are Git submodules. Initialize them without nested dependencies for
source lookup:

```bash
git clone git@github.com:rygo6/WebGL-AGENTS.git ~/.agents/skills/webgl
cd ~/.agents/skills/webgl
git submodule update --init
```

Do not pass `--recursive` or clone with `--recurse-submodules` for source lookup. ANGLE's nested
dependencies can require large downloads and access to private Chromium repositories. They are
unnecessary for this skill's reference workflow.

The commands above use the recorded reference revisions. To deliberately refresh existing
references, review local changes first, then run `git submodule update --remote` and inspect the result.

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

Once installed, request the `webgl` skill by name or use your agent’s skill picker or invocation syntax.

## Related skills

Use `opengl` for native OpenGL and OpenGL ES, `metal` for Apple Metal, `vulkan` for Vulkan and
MoltenVK, and `webxr` when WebGL is used through WebXR-specific bindings.
