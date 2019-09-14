Patches and hacks for Firefox I made, mainly for ESR.
In no particular order.

For autoconfig scripts, need `general.config.sandbox_enabled` = `false`.

## remove-normandy.patch

A patch to remove Normandy component, to be applied to source files.
Tested on ESR60.

## Bug1421725_WebRequest_esr60.patch

A source patch for ESR60 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
Non-blocking listeners are run not affected.

## monkey_Bug1421725_WebRequest_esr60.cfg

An autoconfig script for ESR60 to monkey-patch the changes in Bug1421725_WebRequest.patch.

## Bug1421725_WebRequest_esr68_with_308ef98e6e4b.patch

A source patch for ESR68.1 to make WebRequest.jsm run and apply changes from blocking listeners sequentially.
This patch also refactors the code into a new class: `ListenerRunner`.
Non-blocking listeners are run not affected.

This patch is intended to be applied after applying [this changeset](https://hg.mozilla.org/mozilla-central/rev/308ef98e6e4b),
for [Bug 1450965](https://bugzilla.mozilla.org/show_bug.cgi?id=1450965).

## monkey_Bug1421725_WebRequest_esr68.cfg

Currently untested.
An autoconfig script for ESR68 to monkey-patch Bug 1421725.
