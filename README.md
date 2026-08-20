# BillBoard remote configuration

Serves the notice strip and bottom banner shown inside the BillBoard Android app.
The app reads `config.json` from this site on every launch and whenever the user
taps refresh. Nothing here is required for the app to work — if this site is
unreachable, BillBoard falls back to the last configuration it saw.

    https://akifislam.github.io/BillBoard/config.json

## Turning things on and off

Edit `config.json` and commit. That is the whole process — no app update needed.

| Want to…                  | Change                                        |
|---------------------------|-----------------------------------------------|
| Show/hide the notice      | `marquee.enabled` → `true` / `false`          |
| Change the notice wording | `marquee.text`                                |
| Show/hide the banner      | `advertisement.enabled` → `true` / `false`    |
| Swap the banner picture   | upload to `ads/`, update `advertisement.image_url` |
| Change where it links     | `advertisement.click_url`                     |
| Run it for a date range   | `advertisement.start_date` / `end_date`       |

Both switches are independent: the notice can run with no banner, or vice versa.

## Rules the app enforces

- Links must start with `https://`. Anything else is ignored and that element
  simply is not tappable.
- Dates are ISO-8601 with an offset, e.g. `2026-09-01T00:00:00+06:00`. A banner
  outside its window stays hidden even if `enabled` is `true`, and a malformed
  date hides it rather than showing it at the wrong time.
- Unknown fields are ignored, so new settings can be added later without
  breaking copies of the app already installed on phones.

## Banner images

1200 x 300 px (4:1), WebP preferred, under ~150 KB. Displayed at up to 96 dp
tall, scaled to the screen width with proportions preserved — never stretched.

Upload a **new filename** rather than overwriting an existing one. Images are
cached on the device, so reusing a name can leave some users on the old picture.
