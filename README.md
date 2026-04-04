# pe-calc

A minimal, zero-dependency justified P/E calculator. Single HTML file with embedded CSS and JS.

## Features

- Justified P/E calculation based on growth rate, required return, and terminal value
- Target price and buy price (−20% margin of safety)
- English / Swedish with auto-detection
- Light / Dark / System theme
- Preferences persisted in localStorage

## Run locally

Open `index.html` in a browser — no build step required.

## Docker

```sh
docker build -t pe-calc .
docker run -p 8080:80 pe-calc
```

Or with Docker Compose:

```sh
docker compose up -d
```

## License

GPL v3 — see [LICENSE](LICENSE).
