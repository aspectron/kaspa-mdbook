# Security Considerations

The WASM SDK binaries are built directly from the Rust project codebase. The WASM SDK provides all the necessary primitives to interact with Kaspa from NodeJs or browser environments.

## Using WASM SDK

To load the WASM SDK, you can use the “kaspa” or “kaspa-wasm” NPM modules. However, for security-critical applications, it is recommended to either build the WASM SDK from the Rust source code yourself or obtain prebuilt binaries and embed them directly into your project.

## NPM Versioning

For security-focused applications, any third-party JavaScript Node.js module dependencies should be treated as potentially insecure due to a variety of attack vectors, such as code injection vulnerabilities.

If you must use NPM dependencies, it is crucial to manually review all dependencies and set a fixed version of the dependency, including the patch number. This approach helps prevent unexpected updates when new versions of dependencies are published on NPM.

Manually reviewing and embedding dependencies directly into your project or into a library your project relies on is another excellent option to reduce the risks associated with dependency updates.

## Serving

It is highly advisable to serve WASM libraries, as well as other cryptocurrency application components, from a server controlled by you. Serving WASM libraries from a CDN or third-party servers can expose your application to potential attacks, such as code injection.

## Using *Subresource Integrity*

When loading WASM or your own scripts via the `<script>` tag, you can specify an `integrity` hash for the target resources to ensure that the resource hasn't been tampered with.

```html
<script
  src="https://example.com/example-framework.js"
  integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
  crossorigin="anonymous"></script>
```
Using Subresource Integrity (SRI) helps protect your application by verifying that resources loaded from third parties match the expected content.

Source: [Subresource integrity at Mozilla Developer](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity#subresource_integrity_with_the_script_element)


