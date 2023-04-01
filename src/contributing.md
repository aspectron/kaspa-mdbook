# Contributing

This [mdbook](https://rust-lang.github.io/mdBook/) for Kaspa is available at [https://github.com/aspectron/kaspa-mdbook/](https://github.com/aspectron/kaspa-mdbook).

If you would like to contribute to the content:
```bash
cargo install mdbook
git clone https://github.com/aspectron/kaspa-mdbook
cd kaspa-mdbook
mdbook serve
```
Once started, you can navigate to [http://localhost:3000](http://localhost:3000)

For Visual Studio Code, in the command palette, you can search for *Simple Browser*. This will allow for the book preview while it is being edited.

`mdbook` works like a wiki - it scans for links and creates corresponding markdown files if missing. To create new pages, just create links to destination files.

When you've made changes, please PR!
