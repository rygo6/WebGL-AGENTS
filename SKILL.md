---
name: webgl
description: Use local specifications, conformance tests, examples, and ANGLE source to answer questions and develop, debug, or test WebGL 1 and 2 code. Use for WebGL APIs, shaders, rendering state, extensions, context loss, and browser or backend issues affecting WebGL.
---

# WebGL Local Reference Skill

Search the relevant local sources before answering technical questions. Paths below are relative to this skill directory; read only the sources needed for the request.

```text
references/WebGL/                   ← Khronos WebGL 1/2 specifications, extensions, and CTS
references/WebGLSamples/            ← Classic runnable WebGL examples
references/WebGL2Samples/           ← Focused WebGL 2 examples
references/WebGLFundamentals/       ← Conceptual lessons and focused examples
references/ANGLE/                   ← Browser-facing OpenGL ES implementation and tests
```

WebGL is the browser API. Use the separate `opengl` skill for native OpenGL and OpenGL ES questions, and use `webxr` when WebGL is used through WebXR-specific bindings.

## Choose the authoritative source

| Topic | Primary source |
|---|---|
| WebGL 1/2 API behavior and validation | `references/WebGL/specs/latest/` |
| WebGL extensions | `references/WebGL/extensions/` |
| Web IDL and API surface | `references/WebGL/specs/latest/*/*.idl` and the matching spec |
| Conformance requirements and regressions | `references/WebGL/sdk/tests/` and `conformance-suites/` |
| WebGL 1 implementation examples | `references/WebGLSamples/` |
| WebGL 2 implementation examples | `references/WebGL2Samples/` |
| Concepts, math, and teaching examples | `references/WebGLFundamentals/webgl/` |
| ANGLE translation, backends, and implementation tests | `references/ANGLE/src/`, `extensions/`, and `samples/` |

Treat the Khronos specification as normative. Treat samples and tutorials as illustrative. Treat ANGLE as one important implementation, not a browser-independent definition of WebGL.

## Answer API and extension questions

1. Determine whether the request targets WebGL 1, WebGL 2, or an extension.
2. Search the corresponding file under `references/WebGL/specs/latest/` or `references/WebGL/extensions/` for the method, enum, interface, or algorithm.
3. Read the surrounding validation rules, errors, state changes, and referenced OpenGL ES behavior.
4. Search `references/WebGL/sdk/tests/` for executable edge cases and expected errors.
5. State which behavior is normative, which comes from tests, and which is implementation-specific.

## Implement and debug WebGL code

1. Work from the user's code or reproduction. Use a matching example in `WebGLSamples`, `WebGL2Samples`, or `WebGLFundamentals` when it clarifies the implementation.
2. Verify the API behavior and constraints the answer depends on against the WebGL specification; native OpenGL examples may rely on behavior WebGL does not permit.
3. For shader failures, check the required GLSL ES version, precision declarations, interface matching, compiler log, and WebGL-specific restrictions.
4. For black frames or incomplete rendering, inspect context creation, viewport, program link status, vertex input, texture completeness, framebuffer completeness, depth/blend/cull state, and GL errors.
5. For browser/backend-specific behavior, search ANGLE source and tests, then identify the backend and browser assumptions explicitly.

## Work with conformance tests

1. Search `references/WebGL/sdk/tests/` for the API, extension, or failure signature.
2. Follow shared helpers and generated test inputs before interpreting an assertion.
3. Use `references/WebGL/conformance-suites/` to identify released suite manifests and versions.
4. Distinguish a WebGL CTS expectation from ANGLE's native GL/ES tests.

## Answering strategy

- Cite the source files and relevant sections used. Make local file links resolvable from the user's workspace.
- Separate WebGL 1, WebGL 2, extension, and browser-specific behavior.
- Do not infer current browser support from a specification, test, or sample; verify support when it matters.

## Reference availability and versions

- Local checkouts are snapshots. Match the sources to the user's target version; verify current claims against official upstream sources when freshness matters. Do not silently update existing checkouts.
- If a needed submodule is missing, initialize only that reference with `git submodule update --init -- references/<repo>` from this skill directory. Omit `--recursive`; nested build dependencies are unnecessary for source lookup.
- If a source remains unavailable, state the limitation and use an official upstream source when accessible. Do not present an unverified recollection as a source-backed conclusion.
