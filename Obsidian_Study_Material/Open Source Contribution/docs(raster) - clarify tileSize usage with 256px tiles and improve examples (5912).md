A raster tile layer is ==a basemap or operational layer composed of pre-rendered, static image tiles (PNG, JPG) arranged in a grid, commonly used for rapid display in web and mobile maps==. It serves as a fast-loading, cached image source for geographic context, such as imagery, terrain, or topographic maps.

Improves the raster tile source documentation by:
- Adding a clear note about the default `tileSize` of 512.
- Highlighting the importance of setting `tileSize: 256` when using providers like OpenStreetMap, Stadia Maps, or WMS that serve 256px tiles.
- Enhancing usage examples with inline comments for clarity.

