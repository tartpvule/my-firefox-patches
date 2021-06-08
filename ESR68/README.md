ESR68 Patches

For autoconfig scripts, need `general.config.sandbox_enabled` = `false`.

Alternative way to patch: [chrome.manifest override](https://github.com/tartpvule/my-firefox-patches/issues/2#issue-481998289)

## remove_normandy_esr68.patch

A patch for ESR68 to remove the Normandy component.

## Bug1421725_WebRequest_esr68_with_308ef98e6e4b.patch

A patch for ESR68.1 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
This patch also refactors the code into a new class: `ListenerRunner`.
Non-blocking listeners are not affected.

This patch is intended to be applied after applying [this changeset](https://hg.mozilla.org/mozilla-central/rev/308ef98e6e4b),
for [Bug 1450965](https://bugzilla.mozilla.org/show_bug.cgi?id=1450965).

## monkey_Bug1421725_WebRequest_esr68.cfg

An autoconfig script for ESR68 to monkey-patch Bug 1421725.
