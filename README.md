Patches and hacks for Firefox I made, mainly for ESR.
In no particular order.

For autoconfig scripts, need `general.config.sandbox_enabled` = `false`.

Alternative way to patch: [chrome.manifest override](https://github.com/tartpvule/my-firefox-patches/issues/2#issue-481998289)

## remove_normandy_esr68.patch

A patch for ESR68 to remove the Normandy component.

## Bug1421725_WebRequest_esr60.patch

A patch for ESR60 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
Non-blocking listeners are not affected.

## monkey_Bug1421725_WebRequest_esr60.cfg

An autoconfig script for ESR60 to monkey-patch Bug 1421725.

## Bug1421725_WebRequest_esr68_with_308ef98e6e4b.patch

A patch for ESR68.1 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
This patch also refactors the code into a new class: `ListenerRunner`.
Non-blocking listeners are not affected.

This patch is intended to be applied after applying [this changeset](https://hg.mozilla.org/mozilla-central/rev/308ef98e6e4b),
for [Bug 1450965](https://bugzilla.mozilla.org/show_bug.cgi?id=1450965).

## monkey_Bug1421725_WebRequest_esr68.cfg

An autoconfig script for ESR68 to monkey-patch Bug 1421725.

## ubo1250_issue909.patch

A patch for gorhill's uBlock Origin 1.25.0 to fix Issue 909 "CNAME first-party resources detected as third-party".
This patch makes uBO not resolve CNAME if a request is of exactly the same host as the origin.

In version 1.25.0, first-party same-host requests are filtered twice; first as a normal first-party request, then again as a third-party request under CNAME-uncloaked host. This makes it impossible to write rules that affect the CNAME-uncloaked host while leaving first-party requests alone.

## Bug1424176_poc_esr78.patch

Proof-of-Concept only. Not intended to be "ready for production". Trusts content scripts.

[Bug 1424176](https://bugzilla.mozilla.org/show_bug.cgi?id=1424176) nullifies the security of *any* WebExtensions that hook Web APIs; a potentially hostile page script can always get a reference to an untouched by any WebExtension content scripts by accessing a newly-created iframe's `contentWindow` at `readyState === "uninitialized"`.
This patch "fixes" that by utilizing an `nsIObserverService` observer for `content-document-global-created`, and execute code registered by content scripts on the new windows.

Credit: [Rob Wu's comment in Bug 1486036](https://bugzilla.mozilla.org/show_bug.cgi?id=1486036#c0)

Will probably also "fix" Bugs [1486036](https://bugzilla.mozilla.org/show_bug.cgi?id=1486036) and [1415539](https://bugzilla.mozilla.org/show_bug.cgi?id=1415539), but I have not explicitly tested.

A cleaner approach: define a new `run_at` manifest value, say "document_create", for content scripts to run at `content-document-global-created`.
