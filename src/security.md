# Security Considerations

WASM SDK binaries are built directly from the Rust project codebase.  WASM SDK provides all necessary primitives to interop with Kaspa from NodeJs or a browser environments.

## Using WASM SDK

# TODO: INTEGRITY EXAMPLE FOR LOADING WASM SDK INTO HTML USING `<script>` TAG

To load WASM SDK, you can use “kaspa” or “kaspa-wasm” NPM modules, however for security-critical applications, you should either build WASM SDK from the Rust source code or obtain prebuilt binaries and embed them into your project.

## NPM versioning 

For security-centric applications, any 3rd-party JavaScript node module dependencies should be considered not secure due to a multitude of attack vectors, such as code injection vulnerabilities.

If you have no choice and you absolutely need to use something from NPM, review all dependencies manually, make sure to set the full version of the dependency, including the patch number. This helps prevent potential dependency code updates when new versions of dependencies are published on NPM.

Manual review of all dependencies and direct embedding of said dependencies into your project or a library your project relies on is another great option to reduce exposure to dependency changes.

## Serving

It is generally desirable to serve WASM libraries, as well as other cryptocurrency application components, from the server controlled by you. Serving 


## Usging *subresource integrity*

When loading WASM or your own scripts via the `<script>` tag, you can specify an `integrity` hash of the target resources.

```html
<script
  src="https://example.com/example-framework.js"
  integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
  crossorigin="anonymous"></script>
```

https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity#subresource_integrity_with_the_script_element

