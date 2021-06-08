Patches and hacks for Firefox I made, mainly for ESR.
In no particular order.

For autoconfig scripts, need `general.config.sandbox_enabled` = `false`.

Alternative way to patch: [chrome.manifest override](https://github.com/tartpvule/my-firefox-patches/issues/2#issue-481998289)

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

A cleaner approach would be to define a new `run_at` manifest value, say "document_create", for content scripts to run at `content-document-global-created`.

## mod_ExportFunction_esr78.patch

Adds an option, bool `OOT_notCtor`, for `exportFunction` not to pass `JSFUN_CONSTRUCTOR` to `NewFunctionByIdWithReserved`.
This allows creating a function forwarder that throws `TypeError: ... is not a constructor`.

See [CreepJS "lies.js"](https://github.com/abrahamjuliot/creepjs/blob/1554c66098cd814d7462b60981635339bf526e9e/modules/lies.js)
