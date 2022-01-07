# EVA / Page Builder

## Installation

```
git clone git@github.com:EVA-3D/contrib-extras.git
git submodule update --init --recursive
```

#### I have a proper Python environment

Note that I do not intend to support Windows, Docker is your best bet if you are using Windows.

```
poetry install
poetry shell
```

#### I'll use Docker

```
docker-compose build
```

## Developemnt instance

To run a local copy of the document use the following

```
mkdocs serve
```
or
```
docker-compose run --rm page
```

## Onshape downloader

To use this you must specify the Onshape metadata key on your page, like this:

```yaml
---
title: My page
onshape: 
    uid: EVA / My project / Mosquito
    cad_url: https://cad.onshape.com/documents/1765b04fac582f6c1c470bd3/w/1cc31596374d6ce51cd23fa9/e/f36b4d773104fcd6926a6641
---
```

> `cad_url` needs to point to an Onshape assembly

> check the `docs/sub_page` directoy for an example

Then you can invoke a script that will pull a thumbnail image, BOM and STL files from Onshape:

```
eva-3d page download
```
or
```
docker-compose run --rm page eva-3d page download
```

It will ask you for your Onshape Access and Secret key, you can get those from https://dev-portal.onshape.com/, the key only need the "Application can read your documents" permission.

You can also specify a specific page to be downloaded by using it's `uid` or path, i.e. given the following `docs` structure 
```
docs
├── category
│   ├── thing_1
│   │   └── index.md  # uid = thing-1
│   └── thing_2
│       └── index.md  # uid = thing-2
└──  index.md  # uid = thing-3
```

you can invoke:

```
eva-3d page download --page-uid "thing-1"  # will only download thing-1
eva-3d page download --path category/thing_1  # will only download thing-1
eva-3d page download --path category/  # will download thing-1 and thing-2
eva-3d page download # will download all three
```

Upon success the script will create the following structure in the page directory:

```
sub_page
├── assets
│   └── thumbnail.png
├── stls
│   ├── first.stl
│   └── second.stl
└── index.md
```

> Running the script with remove the stls directory and create it a new in the process - this is to ensure there are no danging STLs.

### Determining which files get downloaded as STL

Python Onshape Downloader pulls the BOM for an assembly first, from that BOM it looks for parts marked with one of the following materials:

- PETG
- ABS
- ASA
- PLA

If a part does not have one of those materials assigned then the part is basically treated like a screw, marked as not printable and thus not downloaded.


## Deployment

TBD but you need to change the licence to CC BY-SA - this repository is code so it's under GPLv3. Also this README should be rewritten to reflect that your repository is about.

I will add automation for the page to deployitself on merge to main.
