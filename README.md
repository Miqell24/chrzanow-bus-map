# Chrzanów area — interactive bus map

Interactive, poster-grade map of the buses of the **Chrzanów commune union**
(Związek Komunalny „Komunikacja Międzygminna" w Chrzanowie, ZKKM): **26 lines
/ 1 357 km** across Chrzanów, Trzebinia, Libiąż, Alwernia, Babice and Płaza,
drawn along the real street geometry.

## Live

**https://miqell24.github.io/chrzanow-bus-map/** — GitHub Pages from `main:/docs`. Local build on port 8187 (`npm run serve`).

| what | detail |
|---|---|
| feed | `data.odt.org.pl/gtfs/zkkm-gtfs.zip` — ODT's copy, **the one with shapes** |
| lines | 3, 8, 9, 10, 15, 17a, 17b, 25, 29, 30, 31, 31B, 32a, 32b, 33, 35, 38, 41, 42, A, B, La, Lb, Lc, P and the night N |
| stops | 438 poles |
| graph | OSM roadways, cut from the Geofabrik małopolskie and śląskie extracts |

**Two copies of this feed exist and they are not the same.** The operator's own
file (`zkkm.pl/files/pl/gtfs/google-transit-3.zip`) is the kiedyPrzyjedzie
export and ships NO shapes; odt.org.pl republishes it WITH shapes — 32 545
points over the same 26 routes and 1 636 trips. This map reads the ODT copy,
and that alone took the mean matching error from 7.3 m down to **1.1 m**:
the corridors are the publisher's geometry instead of a reconstruction from
the stop sequence. Neither copy carries direction_id, so the headsign stays
the direction key.

The night line **N** (two departures, both at 02:15) prints black and sorts
last, the family rule.

## Pipeline

`npm run download` fetches the feed, cuts the OSM and vendors MapLibre GL.
`npm run build` map-matches every line (HMM/Viterbi on the OSM graph) and
writes GeoJSON to `data/out/`; `npm run lines` adds the line-by-line view.
`npm run serve` hosts the map at http://localhost:8187.

Data: GTFS ZKKM Chrzanów · base map © OpenFreeMap / OpenMapTiles /
OpenStreetMap contributors.
