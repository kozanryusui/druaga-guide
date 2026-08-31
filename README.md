# Druaga Online guide and databases

The input databases are in `data/`. The generated item icons are in `item-icons/`. The generated quest minimaps are in `minimaps/`.

This repository contains the generated website. Open `index.html` in a web browser to use it.

The source data and generators are in the sibling [druagatools](https://github.com/kozanryusui/druagatools) repository. The source game files are in its `work/resources/1.60/` directory. The decompiled quest scripts and the main controller area database are in `work/analysis/scpt/`. The complete extracted minimap set is in `work/analysis/minimaps/`.

Clone this repository as `druaga-guide` at the root of the `druagatools` checkout. Run these commands from the `druagatools` root.

```sh
cargo run -p druaga-utils --bin tower-source-builder -- \
  work/resources/1.60/tower/item/lottery.dat \
  work/resources/1.60/tower/item/present.dat \
  druaga-guide/data/tower_sources.json

cargo run -p druaga-utils --bin sol-source-builder -- \
  work/analysis/scpt/decompiled \
  work/analysis/scpt/mainctrl-quest-areas.json \
  work/resources/1.60/station/map/mapname.dat \
  work/analysis/minimaps \
  druaga-guide/data/items.json \
  druaga-guide/data/chests.json \
  druaga-guide/data/quest_sources.json \
  druaga-guide/minimaps

cargo run -p druaga-utils --bin site-builder -- \
  druaga-guide/data/items.json \
  druaga-guide/data/alchemy.json \
  druaga-guide/data/chests.json \
  druaga-guide/data/enemies.json \
  druaga-guide/data/quest_sources.json \
  druaga-guide/data/tower_sources.json \
  druaga-guide
```

Before you run `sol-source-builder`, extract each Station `map/*.gsm` file with `gsm2-extract`. Use the GSM base name for the PNG base name.
