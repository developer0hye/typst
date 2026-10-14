# Downstream typst-library 0.15.1

This maintenance branch packages the published `typst-library` crate with registry dependencies so it remains compatible with the other Typst 0.15.1 crates used by office2pdf. Other compiler crates remain in the checkout as upstream source; the root Cargo manifest builds only `typst-library`.

The branch adds `Clone` to resolved cell-grid data. Consumers can use `Arc::make_mut` to update a copied grid while preserving cached models, merged entries, and header/footer state. Paragraph content, fonts, and images keep their shared storage. Typst layout and painting are unchanged.

The focused regression checks copy-on-write fill independence and retained grid structure. Run:

```sh
CARGO_BUILD_JOBS=2 cargo test --locked --lib -- --test-threads=2
cargo fmt --all --check
```

This is an AI-assisted downstream change. Upstream code PRs are not submitted under Typst's contribution policy; the API request is tracked at [typst/typst#8955](https://github.com/typst/typst/issues/8955). The policy in `CONTRIBUTING.md` describes contributions to the upstream project. AI-assisted maintenance on this downstream branch is authorized by its owner.

Based on Typst 0.15.1, commit `9dfd3a08500b7896045f907433cf7b4b02434fad`, under the original Apache-2.0 license. Return to an official compatible release when it includes the required copy-on-write API.
