# Label Designer

Offline, single-file label design tool for industrial labels. Compose a layout
with text, shapes, images, barcodes and QR codes, then export it as PNG or
`.lab` project, print it on a regular printer, or send it straight to a Zebra
thermal printer over USB (ZPL via WebUSB).

Author: Jhon Lee Quint

The interface is available in Brazilian Portuguese (default), English and
Simplified Chinese; use the language selector in the top-right corner.

## Usage

No installation, server or internet connection is required. Open `index.html`
in a Chromium-based browser (Google Chrome or Microsoft Edge).

1. Set the label size in millimeters and click **Apply** (default 100 x 150).
2. Add elements: text, shape, logo/image, barcode, QR code.
3. Export (**PNG** or **.Lab**) or print (**standard printer** or
   **Zebra (WebUSB)**).

Barcodes: choose the symbology in the dropdown. For alphanumeric values (for
example MAC addresses or serial numbers) use **CODE-128**; EAN and UPC accept
digits only.

See [`docs/USER_GUIDE.md`](docs/USER_GUIDE.md) for the full guide
(translations: [pt-BR](docs/USER_GUIDE.pt-BR.md), [zh-CN](docs/USER_GUIDE.zh-CN.md)).

## Project layout

| Path | Responsibility |
|---|---|
| `index.html` | The application (markup, styles and logic in a single file) |
| `vendor/` | Third-party libraries, bundled for offline use |
| `docs/` | User guide and technical notes |

## Limitations

- No batch serialization or database/ERP integration; the tool is built for
  one-off layouts (WYSIWYG).
- No auto-save. Export the project (`.lab`) before closing or refreshing the
  tab, or the layout is lost.
- Thermal printing converts the canvas to 1-bit with Floyd-Steinberg dithering;
  very low-contrast images may degrade.
- Direct USB printing requires the WebUSB API (Chromium-based browsers only;
  not available in Firefox or Safari).

## Third-party libraries

Bundled unmodified in `vendor/`:

| Library | Version | License |
|---|---|---|
| [Fabric.js](https://github.com/fabricjs/fabric.js) | 5.3.0 | MIT |
| [JsBarcode](https://github.com/lindell/JsBarcode) | 3.11.5 | MIT |
| [qrcode](https://github.com/soldair/node-qrcode) | 1.5.1 | MIT |

Full notices: [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

## License

Released under the [MIT License](LICENSE).
