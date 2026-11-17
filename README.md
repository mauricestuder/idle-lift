# Idle Lift

An idle ski resort on a 3D mountain, for phone and PC, running in the browser.

The resort runs itself: guests arrive, queue, ride the lifts, ski down and pay
for every ride. You spend the money with six big buttons.

## Play

No build step and nothing to install. Serve the folder with any web server and
open it:

```bash
npx --yes http-server -p 8080 -c-1
```

Then open `http://localhost:8080/`. Opening `index.html` straight from the disk
does not work, because browsers block JavaScript modules on `file://`.

Over https the game installs as an app (Add to Home Screen) and loads without a
connection after the first visit.

## The game

- Income per second is worked out from your lifts, guests and prices, and stays
  the same until you buy something.
- **New lift** opens the next of six lifts with its piste. **Upgrade lift** turns
  a lift into a chairlift, then a gondola.
- **Lift speed**, **More guests**, **Ticket price** and **Ski hut** raise the income.
- **Jump park** builds kickers; now and then a skier takes one for a trick bonus.
- **Snow guns**, **Ski school**, **Night skiing** and **Restaurant** unlock as you play.
- **Rush hour** is a 30 second boost with a 2 minute recharge.
- 26 quests pay bonuses. Three are open at a time; finishing one unlocks the next.
  When every lift is a gondola you move to the next of three mountains
  (Sonnenhang, Gamshorn, Wetterspitz) and all income doubles.
- **Events** every few minutes: Powder day (income x2), Storm (a lift stops until
  you secure it, for a bonus) and Celebrity visit (tap the skier in gold).
- While the game is closed the resort earns half its income for up to 8 hours.
  The **Lodge** board raises both.
- Pistes wind down the mountain in snake curves, with tunnels, wooden bridges,
  mogul fields, a race section with gates and a fun park with rails, a box and a
  halfpipe.
- Guests arrive by car and coach on the valley road, park in a big car park
  (110 bays) and climb out; when they are done they walk back, climb in and
  drive off. Guests without a car take the coach home. Skiers and snowboarders
  share the pistes. All prices are whole dollars.
- The **P** button sets the parking price, from Free to Rip-off: cheap parking
  brings more guests, dear parking pays more per guest. The sheet shows what
  each price earns.
- Cozy look: warm golden light, soft peach skies and lavender shade on the snow,
  plump round trees, glowing windows and chimney smoke in the village, guests in
  knitted beanies, wide pistes, and a rounded, friendly font on soft wooden boards.
- The valley has a village of painted chalets and a church; hot-air balloons,
  paragliders and skaters on the frozen lakes keep it lively.

## Controls

- Hold a board to keep buying. Keys 1 to 6 press the first six boards, Space starts rush hour.
- **Touch:** one finger moves the camera, two fingers zoom.
- **Mouse:** drag moves, wheel zooms.

Progress saves in the browser (`localStorage`, key `firstchair.idle`).

## Layout

```
index.html            markup and styling
manifest.webmanifest  app name and icons
sw.js                 service worker for offline play
icons/                app icons
vendor/               three.js r160 (MIT licence, see vendor/three-LICENSE)
js/tuning.js          every balance number: fares, prices, growth, caps
js/maps.js            the three mountains
js/terrain.js         heights, slopes, forest              (no rendering)
js/network.js         shapes of lifts and pistes           (no rendering)
js/layout.js          where the six lifts go on a mountain (no rendering)
js/idle.js            the rules: guests, income, buying, milestones, saving (no rendering)
js/view/              three.js scene, camera, lifts, pistes, buildings, guests, extras
js/view/cars.js       the valley road, car park, cars and coaches
js/view/deco.js       village, balloons, paragliders, skaters
js/ui.js              money sign, upgrade boards, quest list, pop-ups, notices
js/audio.js           synthesised sound
js/main.js            boot and game loop
```

The modules marked "no rendering" import nothing from three.js or the page, so
the rules can be run in plain Node to test balance changes.
