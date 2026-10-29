# Changelog

What the update dialog in Home Assistant shows. The repository root's `VERSION` is the single
source of the number and [`../../CHANGELOG.md`](../../CHANGELOG.md) is the whole release note;
this file is the add-on's half of it, in the same [Keep a
Changelog](https://keepachangelog.com/en/1.1.0/) shape. `test.sh` fails the build when the two top
entries and `config.yaml` disagree.

## Unreleased

## [0.1.47] - 2026-10-29

### Changed

- The API layer's Laravel framework is updated to 13.38.

## [0.1.46] - 2026-10-28

### Changed

- The battery plan no longer sells a full battery on a sunny midday: energy left at the end of
  the plan is valued at the lowest positive import price (#533).
- The tunnel is updated to cloudflared 2026.10.3, and the add-on's Home Assistant base image to
  its latest 3.24 build.

## [0.1.45] - 2026-10-25

### Changed

- A saved Home layout may hold the expected cost widget, so the expected electricity cost can be
  removed from Home and added back (#1055).

## [0.1.44] - 2026-10-23

### Changed

- The plan screen is answered for the next 24 hours rather than up to midnight, so tomorrow's
  prices and plan show once they are in (#1037).

## [0.1.43] - 2026-10-21

### Security

- Runs on PHP 8.5.12, which fixes a CVE in PHP itself. 0.1.42 still shipped 8.5.11 (#1030).

## [0.1.42] - 2026-10-21

### Security

- Meant to move to PHP 8.5.12 and did not: this version still runs PHP 8.5.11. Update to 0.1.43.

## [0.1.41] - 2026-10-21

### Added

- Today's plan for the app's plan screen: the price per quarter hour, each appliance's planned
  run and the battery's plan when one is steered (#538).
- Pausing steering for the rest of the day: every steered device goes back to its normal mode
  until midnight in the house's time zone (#538).

## [0.1.40] - 2026-10-21

### Added

- A notification in the evening when tomorrow's solar forecast is at least 5 kWh more than the
  house is expected to use, so the washing can wait for the afternoon (#684).

## [0.1.39] - 2026-10-21

### Added

- The energy steering setup proposes an appliance's run time and deadline from its own past runs
  in Home Assistant's history, and says so. An appliance without enough runs keeps 120 minutes,
  ready by 07:00 (#1003).

## [0.1.38] - 2026-10-21

### Added

- The Agent switches the appliances chosen in the energy steering setup at their planned quarter
  hour, gives way to a person switching one by hand, and hands every device back when the prices
  run out. No battery is steered yet (#535).
- A weather entity can be tagged as the house's weather forecast (#665).

## [0.1.37] - 2026-10-20

### Added

- The Agent keeps what the administrator chose Domely may steer, and how long each appliance runs,
  for the new energy steering setup in the app (#537).

## [0.1.36] - 2026-10-20

### Added

- Home shows what electricity is expected to cost today and tomorrow, and the cheapest two hours,
  for a house with a dynamic contract (#531, #664).

## [0.1.35] - 2026-10-20

### Added

- An energy flow widget for Home, for a house with solar, a battery or an EV charger (#778).

## [0.1.34] - 2026-10-20

### Added

- The house's solar forecast can be chosen as an energy role, "Zonneprognose" (#530).

### Changed

- The add-on links to its public distribution (#946).

## [0.1.33] - 2026-10-19

### Changed

- The tunnel is updated to cloudflared 2026.10.1.
- The API's Laravel framework and JWT library, and the adapter's WebSocket libraries (ws and
  home-assistant-js-websocket), are updated.
- The adapter is built with TypeScript 7.

## [0.1.32] - 2026-10-18

### Security

- The internal channel only runs the Home Assistant services Domely issues (#872).
- Event streams are limited per user and end when the token or the session does (#871).
- A push subscription cannot be moved to another user and is capped per user (#874).
- The adapter's log cannot be forged, the cloud address must be https and on one origin, and the
  database file is private to the add-on (#873).
- The API and the tunnel no longer inherit the supervisor token (#875).
- The API logs less of what an unauthenticated caller sends, and its answers carry `nosniff` and
  `no-store` (#870, #886).
- A vulnerable HTTP library in the API is updated (#869), and the images' base layers are pinned
  and carry provenance and an SBOM (#889).

## [0.1.31] - 2026-10-18

### Fixed

- A state change right at start-up, or a first sync that fails, no longer leaves the mirror behind
  (#808).
- A Home Assistant restart no longer removes devices from Domely or switches automations off while
  its integrations are still loading (#809).
- Notifications are only sent to real push services (#803).
- An empty state from Home Assistant is kept as it is, and two admin changes can no longer half
  apply (#811).
- The remote-access tunnel restarts less often, stops cleanly, and an interrupted first start no
  longer stops the add-on from starting again (#812).

## [0.1.30] - 2026-10-17

### Added

- The house keeps the notifications it sent for a week, so the app can list them on the
  notifications screen (#793).

## [0.1.29] - 2026-10-16

### Added

- An administrator can publish a Home Assistant `number` or `select` entity, such as a battery's
  charge power setpoint or its mode. The household sees it read-only; the administrator and
  automations can set it (#526).

## [0.1.28] - 2026-10-16

### Added

- The house accepts the "Goed moment" block on its home screen, which says whether now is a good
  moment to use power (#657).

## [0.1.27] - 2026-10-16

### Added

- A `contact` type for a door or window sensor, and a notification when one stays open longer
  than the administrator set (10 minutes by default). It reaches only those who may see the
  device (#686).

## [0.1.26] - 2026-10-16

### Added

- A notification when an appliance has finished: an energy meter the administrator marks "notify
  when finished" counts a run above 10 W for five minutes, and idle below 5 W for three minutes.
  It reaches only those who may see the device (#689).

## [0.1.25] - 2026-10-15

### Added

- A morning notification when the house used noticeably more at night than its median of the last
  14 nights, read from Home Assistant's statistics for the grid import meter (#685).
- The administrator is notified when an automation failed (#692) and when Home Assistant has been
  unreachable for ten minutes (#691).
- A grant can end on a date, and the house treats an ended grant as no grant (#654).

### Changed

- The quiet window between notifications is kept per kind, so one kind no longer silences another
  (#685).

### Fixed

- Renaming a room that holds a published device triggers a Google Home sync (#730).
- The adapter exits when its first connect to Home Assistant fails on a database that is not
  migrated yet, instead of lingering (#736).

## [0.1.24] - 2026-10-13

### Added

- Each device has a "Niet naar Google Home" switch. A device with it set is left out of what the
  house reports for Google Home (#706).

### Changed

- Publishing refuses a type that does not fit the entity's domain. A light and a switch may each
  be the other, a cover is only ever a cover. Devices published earlier keep their type until it is
  changed (#706).

## [0.1.23] - 2026-10-12

### Added

- The house tells Domely Cloud when its published devices change, so Google Home picks them up
  without linking again, and reports each device's type and abilities alongside its state, which
  Google Home needs to show it (#318).
- A cover's class is read from Home Assistant when it is published, so blinds, curtains, shutters
  and awnings can reach Google Home. Covers published earlier get it the next time they are saved
  (#463).

## [0.1.22] - 2026-10-11

### Added

- Each member can switch off the notifications this house sends, per kind, from the Notifications
  screen in the app. The house keeps the choice and nothing about it reaches Domely Cloud (#679).

## [0.1.21] - 2026-10-11

### Added

- Home can be several dashboards, each shown to everyone or to the accounts you chose. The number a
  house may have arrives from Domely Cloud (#669).

## [0.1.20] - 2026-10-09

### Fixed

- The adapter no longer writes "Skipping the smoke test" to the status page on every start. The
  line is meant for development and is now logged at `debug` (#649).

## [0.1.19] - 2026-10-08

### Added

- The add-on tells Domely that it is the add-on, so the app's update notice can say where in Home
  Assistant to update it (#639).

## [0.1.18] - 2026-10-08

### Added

- A phone or browser that was signed out of Domely, or whose account changed its password, can no
  longer reach the house with what it still held, instead of until its access ran out up to two
  weeks later (#626).

## [0.1.17] - 2026-10-05

### Added

- Someone who accepts an invitation sees the house at once, and someone who is removed loses access
  at once, instead of within five minutes (#609).

## [0.1.16] - 2026-10-05

### Added

- The house can tell Domely support what it holds of who may use it, and a short log of how its
  connections to Home Assistant and Domely Cloud went, without device states or names (#605).

## [0.1.15] - 2026-10-02

### Security

- The API layer's Laravel and Markdown libraries are updated for three published advisories.

## [0.1.14] - 2026-10-01

### Added

- Media players can be published in Domely: play and pause, volume and the source, each only
  when the player supports it.

## [0.1.13] - 2026-09-29

### Added

- The Domely page in the sidebar can unpair the add-on: type `ONTKOPPEL` as a Home Assistant
  administrator. Rooms and devices are kept. When Domely Cloud no longer knows this house, the page
  says so instead of linking to it.
- New devices in Home Assistant are remembered, so "Nieuw gevonden" in Domely's Beheer shows what
  appeared since you last looked. Ignored ones can be brought back.

### Changed

- A quick action switches every device it can, at once, even when one of them fails.

## [0.1.12] - 2026-09-29

### Added

- An `unpair` option: put in the home ID from the log and restart, and the add-on asks for a new
  pairing code. It only unpairs the home it names, so it is safe to leave filled in.

### Fixed

- With the energy insights on, a power meter now sends its peak power per hour, also beside a
  kilowatt-hour meter for the same thing and for the P1 meter's net power.

### Security

- The sidebar page shows the pairing code only to a Home Assistant administrator. Anyone else is
  pointed at the add-on's log, which only an administrator can read.

## [0.1.11] - 2026-09-28

### Changed

- The add-on's image is now published under `ghcr.io/domely-app`. Nothing in it changed since
  0.1.10.

## [0.1.10] - 2026-09-27

### Added

- Scenes can be composed in Domely from published devices, and the add-on switches them step by
  step.
- Covers: open, close and set a position.
- A notification from the house also reaches a page with Domely open, without push permission.

### Changed

- Starting the house over also deletes the scenes composed in Domely.

## [0.1.9] - 2026-09-26

### Added

- Home can hold an empty block, to leave a place open.
- Starting the house over from its settings deletes every device, room and automation Domely kept,
  so setting it up again starts from Home Assistant alone.
- Automations can be switched off for the whole house: none of them runs until they are switched on
  again, and each comes back as it was.

### Fixed

- Device state now reaches Google Home. Every report the add-on made had been refused since it
  started reporting, and nothing said so outside the log.

## [0.1.8] - 2026-09-25

### Added

- A device can be set to "Alleen zien": your housemates see it and cannot switch it, you still can.
- Home can hold small blocks, a quarter of the width, and a block for one room.

## [0.1.7] - 2026-09-24

### Fixed

- A thermostat is refused a mode it does not have before the command reaches Home Assistant.
- Unpairing while the add-on is syncing with Domely Cloud no longer logs an error, and no longer
  leaves the old home's access behind.
- Notifications reach only the phones of people who still have access to the home.

## [0.1.6] - 2026-09-23

### Added

- A house whose grid is one signed P1 number now also gets the notification that it is giving
  power away.

### Changed

- A room you rename in Home Assistant, or a device you move to another one, reaches Domely within
  the second. Until now it waited for the next time Home Assistant restarted, and nothing said so.
- The house tells you which modes a climate device actually has, so a room's card no longer offers
  one it does not, such as "Ontvochtigen" on an air conditioner that cannot dry. A device published
  before this ships keeps offering the full list until you republish it.
- A room or a device can no longer be given a name shaped like a Home Assistant entity id, and
  neither can a room the one-tap setup creates. Nothing already named that way is touched.
- `domely:channel-check` tells an adapter address that does not resolve apart from one that has not
  started yet, instead of one line that reads as a wait either way.

### Fixed

- A lamp or a socket that your energy dashboard happens to name is offered as a lamp or a socket
  when you publish it, instead of as an energy meter.
- When a command cannot reach the part of Domely that talks to Home Assistant, the add-on log says
  what went wrong and which address it tried, instead of one sentence that fits every cause.
- A counter and a power sensor carrying the same energy role, such as a P1's import counter and its
  own import power sensor, are no longer added together in what the house reports for insights.
- The automation engine advances its minute counter only after the work that depends on it, closing
  a narrow window where a failure between two reads in the same tick could fire an automation
  twice.
- Beheer, open in your browser, now hears when you rename a room or move a device in Home
  Assistant, instead of only catching up the next time you reload the page.

## [0.1.5] - 2026-09-23

### Added

- The home screen is yours to compose. The house keeps the layout, everybody in it sees what you
  put there, and each of them only the devices they may reach. It also knows the new blocks: what
  needs attention, what is on, and today.
- A P1 that reports the grid as one number, negative while you give back, can be published as the
  grid. Home Assistant's own grid power sensor is suggested as that, and so is the P1's live power
  when the energy dashboard only knows its counters.
- The house tells the app which of its devices are one physical thing, so an air conditioner's
  display light and jet mode are shown with the air conditioner.

### Changed

- Domely's own logo, in the add-on list and on its page, instead of the placeholder square and the
  word spelled out in pixels.

## [0.1.4] - 2026-09-18

### Added

- This house tells Domely which version of each of its three parts it is running, on the calls it
  already makes. It is what makes "which version are you on" answerable without asking you to go
  and look. Nothing about your house or the people in it travels with it.

## [0.1.3] - 2026-09-18

### Added

- Lamps that can change colour can be asked to. Tick "Kleur veranderen" when you share the lamp, or
  press Aanzetten on the line that says the lamp can do more than it was shared with, and a colour
  picker appears on its card in the app. A lamp that only runs warm to cold white is not offered
  one, because there is no colour in it to pick.

## [0.1.2] - 2026-09-17

### Added

- Domely can ask this house to send a test notification, so somebody can watch one arrive instead
  of waiting for the sun. It goes to every phone and browser in the household that turned
  notifications on, and it does not use up the one notification a day about spare power.

### Changed

- The Domely Cloud address is filled in for you. Leave it as it is unless you run a Domely Cloud
  of your own.

## [0.1.1] - 2026-09-17

### Added

- The sidebar's pairing page shows the code large enough to read from across the room, says how
  long it is still good for, and its button opens the app with the code already in the field.
- The house Home Assistant already knows, offered in one pass: rooms and the devices in them, each
  with a sensible suggestion of what your housemates may do with it, published in one confirmation
  instead of built up by hand.
- "Alle lampen uit" as a quick action on the home screen, which switches off every lamp you shared.
- Automations that run in this house rather than in the cloud. Domely stores them here, and the
  engine that runs them reaches only the devices you published, and only the things those devices
  can really do. What they did is kept here as well and is readable in the app.
- One notification, sent by the house itself and never by Domely Cloud: when your roof has been
  giving power away long enough to be worth doing something about, your phone is told, with
  something to do attached. It reads what Domely has already mirrored, so it costs Home Assistant
  nothing.

## [0.1.0] - 2026-08-31

The first release. Add [domely-app/sidecar](https://github.com/domely-app/sidecar) as a
repository in the add-on store and Domely appears there.

### Added

- Domely as a Home Assistant add-on: the adapter, the API layer and the Cloudflare tunnel in one
  container under s6-overlay, talking to the Home Assistant it is installed in through the
  supervisor's own proxy. No long-lived token, and no port forwarding.
- A sidebar entry, which opens this home's administrator screens in the Domely app.
- Everything durable under `/data`, so a Home Assistant backup carries the publish configuration
  and a restore brings back the same device identities the household's shares point at.
