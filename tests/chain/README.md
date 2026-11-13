# Test catalog for the signing chain

A minimal catalog repository used only by the dry run in `.github/workflows/checks.yml`. Its
values are made up for the test and say so here: the CLI entry names version 0.0.1 with a hash of
zeros, which no real file has. Nothing here is ever published.

The dry run assembles this catalog, signs `keys.json` and the catalog with keys generated in the
run and thrown away afterwards, and verifies both. Before that it must see `verify` refuse a
tampered catalog and a wrong root key, so a check that always passes cannot go unnoticed (R-20).
