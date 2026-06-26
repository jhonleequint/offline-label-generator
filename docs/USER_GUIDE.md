# Label Designer — User Guide and Technical Notes

Languages: **English** · [Português (pt-BR)](USER_GUIDE.pt-BR.md) · [简体中文](USER_GUIDE.zh-CN.md)

Author: Jhon Lee Quint

## 1. Purpose

An offline, standalone "engineering studio" for rapid prototyping and on-demand
printing of industrial labels. It lets you build layouts, test barcodes (MAC,
SN, EAN) and verify them directly on Zebra thermal printers, without complex
setup or an internet connection.

## 2. User guide

- **Label size:** set the real dimensions (millimeters) in the top fields
  (for example 100 x 150) and click **Apply**.
- **Add elements:** use **+ Text**, **+ Shape** and **+ Logo / Image** to compose
  the layout.
- **Barcodes:** select the symbology in the dropdown. For alphanumeric values
  (for example MAC addresses containing letters) use **CODE-128** exclusively.
  EAN and UPC accept digits only.
- **QR code:** click **+ QR Code** and enter the data.
- **Export (.Lab):** saves the current project for later use or as a layout
  backup.
- **Print (network):** the **Standard Printer** button rasterizes the label and
  opens the operating system print dialog (suited to networked A4/inkjet
  printers).
- **Print (Zebra/WebUSB):** sends a direct ZPL (Zebra Programming Language)
  conversion over USB to Zebra thermal printers.

## 3. Limitations and scope

As a client-side application running offline in the browser:

- **No batch serialization:** not designed to integrate with a database or
  ERP/MES for automatic sequential printing (for example 1,000 sequential MAC
  addresses). Operation is based on single, WYSIWYG designs.
- **Volatile storage:** there is no auto-save to the cloud or local disk. If the
  tab is closed or refreshed before the project is exported (.Lab), the on-screen
  data is lost.
- **ZPL conversion (dithering):** for WebUSB thermal printing, color images and
  gradients go through Floyd-Steinberg halftoning. Very low-contrast images may
  degrade in 1-bit thermal output.
- **WebUSB compatibility:** direct USB communication requires a Chromium-based
  browser (Google Chrome, Microsoft Edge). Firefox (Gecko) and legacy WebKit do
  not support this hardware API.

## 4. Architecture and libraries

Pure client-side architecture (single page, single file), with no back-end
dependency, which keeps the tool portable and usable on isolated (air-gapped)
industrial networks.

- **Core languages:** HTML5, CSS3 and vanilla JavaScript (ES6+).
- **Canvas engine:** Fabric.js 5.3.0 — vector manipulation, drag and drop, and
  rendering at the exact physical scale of 203 DPI.
- **Barcode generation:** JsBarcode 3.11.5 — CODE-128, EAN, UPC and others.
- **QR code generation:** qrcode 1.5.1 — QR codes with built-in error correction.
- **Physical communication:** native browser WebUSB API — routes the ZPL/GFA
  bytes from the browser directly to the printer's USB endpoint (Zebra vendor
  ID `0x0A5F`).
