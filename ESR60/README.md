ESR60 Patches

For autoconfig scripts, need `general.config.sandbox_enabled` = `false`.

Alternative way to patch: [chrome.manifest override](https://github.com/tartpvule/my-firefox-patches/issues/2#issue-481998289)

## Bug1421725_WebRequest_esr60.patch

A patch for ESR60 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
Non-blocking listeners are not affected.

## monkey_Bug1421725_WebRequest_esr60.cfg

An autoconfig script for ESR60 to monkey-patch Bug 1421725.
