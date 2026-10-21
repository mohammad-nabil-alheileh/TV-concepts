# Image Memory on Low-RAM TVs

The size of an image file on disk or over the network is **not** what it costs in memory. Once an image is displayed, the device decodes it into raw pixels, and that decoded bitmap is what fills RAM. The cost depends on the pixel dimensions, not the file size.

```
decoded size = width × height × 4 bytes
```

## Example Decoded Sizes

Each pixel takes 4 bytes, so the decoded size grows with the dimensions:

| Image dimensions | Decoded size | Notes |
|---|---|---|
| 1920 × 1080 (1080p) | about 8.3 MB | Typical full-screen TV size |
| 3840 × 2160 (4K) | about 33.2 MB | Four times the 1080p cost |
| 1000 × 1500 (poster) | about 6.0 MB | Typical poster artwork |

A file that is only a few hundred kilobytes on disk can still take several megabytes once decoded.

## Why It Matters on TV

- Low-end TVs and streaming sticks often have 1 to 2 GB of RAM shared with the system, and the OS kills apps that go over their budget.
- TV screens show lots of large artwork at once.
- The crash often only shows up after a long browsing session, which makes it hard to reproduce.

## Fixes

| Fix | What to do | Why it helps |
|---|---|---|
| 1. Request right-sized images | Ask the server for about 1x to 2x the display size, not 4x | The screen is usually 1080p, so extra pixels are never shown |
| 2. Use an image library with caching | Use a library that manages a memory cache with limits | Old entries are evicted automatically |
| 3. Set explicit dimensions | Always give network images explicit width and height | The image is decoded at the size it is shown, not at its full size |
| 4. Load only what is visible | Release images for unmounted items | Memory is freed as the user scrolls away |
| 4a. Prefetch carefully | Prefetch only the next few items in the direction of travel | Avoids loading the whole catalogue |
