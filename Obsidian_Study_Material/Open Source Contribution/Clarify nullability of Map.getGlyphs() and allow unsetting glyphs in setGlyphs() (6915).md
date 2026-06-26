In MapLibre (and Mapbox GL), **glyphs** are the raw shapes of text characters (fonts) used to render labels on the map. 

> **Because WebGL cannot render standard HTML text directly,** 

the map needs to download "Signed Distance Field" (SDF) images of every character (A, B, C, etc.) in the specific font you want to use (e.g., "Open Sans Bold").

- These are stored in `.pbf` (Protocol Buffer) files.
- The system downloads them in ranges (e.g., characters 0-255, 256-511) so it only loads the characters it needs (like loading Chinese characters only when viewing China).

### `setGlyphs(glyphsUrl)` and `getGlyphs()`

These methods manage the URL template where the map looks for these font files.

*   `setGlyphs(glyphsUrl: string | null)`: Sets the URL template for loading fonts.
    *   'https://demotiles.maplibre.org/font/{fontstack}/{range}.pbf'.
    *   **null** to this method to _remove_ the glyphs URL entirely. Previously, this might have been restricted or undefined behavior. If set to null, the map will stop trying to load text fonts (likely resulting in no text labels or errors if layers try to use them).
        
*   `getGlyphs()`: Returns the current URL template string, or **null** if none is set.
    *   | null, confirming that "no glyphs set" is a valid and expected state, rather than just returning undefined or an empty string.