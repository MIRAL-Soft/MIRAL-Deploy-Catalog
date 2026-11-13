# MIRAL-Deploy-Catalog

The package catalog of MIRAL Deploy, a package manager for Windows PCs by MIRAL Soft. This
repository holds data only: which programs MIRAL Deploy knows, where their installers come from,
how a successful installation is recognised, and which general profiles and bloatware entries
exist. The programs themselves are not part of this repository.

## How the catalog reaches a PC

1. Every change arrives as a pull request. CI checks it: the format, the rules of the catalog,
   HTTPS and the allowed domains of each package, and, for the packages the pull request changes,
   that every installer can be downloaded and matches its SHA-256.
2. After a merge, the publishing workflow assembles all files into one `catalog.json`. A
   maintainer approves the signing step by hand; only that step holds the signing key.
3. The signed catalog is published at `https://catalog.miralsoft.com/`:
   `keys.json`, `keys.json.sig`, `catalog.json`, `catalog.json.sig`.
4. MIRAL Deploy verifies `keys.json` against root keys built into the program, then the catalog
   against a key listed in `keys.json`. It refuses an unsigned catalog, a wrong signature, and a
   catalog older than the newest one it has already accepted. Every installer is checked against
   the SHA-256 in the signed catalog on exactly the file that is then run.

## Layout

| Path | Content |
|---|---|
| `packages/<id>.json` | One package: names, detection, the one approved version and its installers |
| `profiles/<id>.json` | A general profile such as a standard set of programs |
| `bloatware/<id>.json` | A program or Store app that may be removed, never by default |
| `settings.json` | `mirrorBase`, the address of the MIRAL Soft mirror |
| `programs/cli.json` | The current MIRAL Deploy CLI release (version, URL, SHA-256) |
| `keys/` | `keys.json` with its root signature, and the public root keys |

Every file carries `schemaVersion` and is written in one normal form: the fields in a fixed
order, two spaces of indentation, LF line ends, a final line end, UTF-8 without a byte-order mark.
IDs are short and use lowercase letters, digits and hyphens only (`firefox`, `7zip`).

## What this catalog does not do

- It contains no scripts. Actions after an installation come from a fixed, declarative list
  (remove a shortcut, set a registry value, disable a scheduled task or a service).
- It contains no licence keys and licenses nothing. Commercial software is installed unlicensed.
- It contains no customer data and no customer-specific profiles.
- It collects nothing. Fetching the catalog is a plain download of static files.
- It removes nothing on its own. Uninstalls and bloatware removal are always visible and must be
  chosen; a profile may preselect them, and every preselection can be undone before a run.
- Installers are mirrored only where the vendor's terms permit redistribution; otherwise the
  vendor's own address is used.

## Contributing

Pull requests are welcome. Maintainers usually work with the MIRAL Deploy Catalog Editor, which
writes the normal form and checks a change before proposing it. When editing by hand, keep the
normal form and run the CatalogTool's `check --repo .` before opening the pull request. A
maintainer reviews every pull request; installers for the mirror are uploaded by maintainers only.

## Trademarks

Program and company names in this catalog are trademarks of their respective owners. MIRAL Soft
is not affiliated with, endorsed or sponsored by any of them. A program listed here is offered
under its vendor's own licence terms, which this repository does not change.

## Licence

The catalog data and workflows in this repository are licensed under the MIT License, see
[LICENSE](LICENSE). The licence covers this repository only, not the programs it describes.
