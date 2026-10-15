# Domely

Domely is an add-on and companion app for Home Assistant. It lets you share a simple, premium app
with the people you live with, without them ever seeing the Home Assistant interface, and without
port forwarding.

This repository is how you install it. It holds no source: the code lives in a private repository
and ships as images on GHCR.

## Home Assistant OS, as an add-on

Settings, Add-ons, Add-on store, the three-dot menu, Repositories, and paste this repository's URL.
Domely then appears in the store.

### Edge, for a test house only

`domely-edge/` is a second add-on, "Domely (edge)", built from the main branch before it is
released. It has its own data and is not promised to coexist with the stable add-on. Leave it alone
unless you are testing Domely itself.

## Home Assistant in Docker, as a container

`standalone/compose.yml` runs the same three components beside your existing Home Assistant, with a
long-lived access token instead of the supervisor. `standalone/README.md` has the steps.

That path is permanent rather than a fallback: a large part of the Home Assistant community runs
Home Assistant in Docker and cannot install add-ons at all.

## Licence

Apache-2.0, in `LICENSE`. The Domely Cloud service that the app pairs with is a separate,
proprietary component and is not part of this repository.
