# manang-plugin-template

A starter repository for a [Manang](https://github.com/Fundaments-Work/Manang)
plugin written in Rust and compiled to a WebAssembly component. Use it with
"Use this template" on GitHub (once the repository is public and marked as a
template) or by copying the files.

## Status

**Pre-release.** The plugin interface (`manang:plugin@0.2.0`) is 0.x and
unstable. The `cargo-manang` command line tool, which is meant to replace the
manual steps below, **does not exist yet**. Until it does, building needs the
`manang-sdk` repository's `scripts/build-plugin.sh` and its `componentize` tool.
The template has no workflows and no release automation yet.

## What is in here

| Path | What it is |
| :--- | :--- |
| `Cargo.toml` | a `cdylib` crate for `wasm32-unknown-unknown` (standalone workspace) |
| `manifest.toml` | the plugin's identity, permissions and commands |
| `src/lib.rs` | one command, `my-plugin.hello`, and a pass-through hook |
| `wit/plugin.wit` | a copy of the `manang:plugin@0.2.0` interface from `manang-sdk` |

Everything named `my-plugin` or marked `PLACEHOLDER` is yours to rename.

## Build it today, step by step

You need Rust with the `wasm32-unknown-unknown` target and a checkout of the
`manang-sdk` repository (private for now, so you need access to it).

```sh
rustup target add wasm32-unknown-unknown
git clone https://github.com/Fundaments-Work/manang-sdk.git
git clone https://github.com/Fundaments-Work/manang-plugin-template.git my-plugin
cd my-plugin

# edit name in Cargo.toml and manifest.toml, command ids and src/lib.rs, then:
../manang-sdk/scripts/build-plugin.sh .
# -> ./dist/<name>/{manifest.toml,plugin.wasm}

cp -r dist/<name> ~/.config/manang/plugins/      # Linux; Manang hot-reloads it
```

The first build of the `componentize` tool is slow (it compiles `wit-component`);
later builds reuse it. These steps are the same ones Manang's own repository used
before the SDK was split out; they have not yet been re-run from these two
repositories.

Keep `wit/plugin.wit` identical to `manang-sdk/wit/plugin.wit`: a component built
against another version of the interface is rejected by the host. See the SDK's
`docs/plugin-guide.md` (being restructured) for the manifest, permissions, limits
and the stateless-per-call model.

## Related repositories

All under the `Fundaments-Work` organisation, all private for now.

* `Manang`: the application
* `manang-sdk`: the interface, the componentize tool, the example and the guide
* `manang-plugin-template`: this repository
* `manang-plugins-registry`: the list of published plugins and the signed-index tooling

## Licence

0BSD: do whatever you like with the template; no attribution required.
