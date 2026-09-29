# ScanWise

ScanWise is a small, responsive packaged-food label reader. It can look up a product by barcode, show available ingredients, declared allergens and nutrition, and keep optional preferences and package-specific dates on the device.

## Run locally

This project has no build step or package dependencies. Serve this folder over HTTP (camera access requires a secure context, such as `localhost`):

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>. You can also deploy the static files to any HTTPS static host.

## Product data

Lookups use the public [Open Food Facts API](https://world.openfoodfacts.org/data). No API key is required. Barcode searches are sent to Open Food Facts; personal preferences are kept in browser local storage and are not sent. Product coverage and completeness vary. This app displays only returned facts, with missing fields called out. It currently uses the worldwide product endpoint. No credentials or environment variables are required.

## Languages

The interface supports English and Hindi (हिन्दी), and defaults to Hindi when the browser language is Hindi. The selected language is stored on the device. Package wording remains in the source language where provided. Nutrition is displayed per 100 g/ml based on Open Food Facts fields.

## Dates and privacy

A barcode identifies a product type and does not supply the date on an individual package. Users may enter and label a best-before or use-by date for a product. These dates are stored locally and are not represented as database data or a food safety determination. The app stores preferences, recent lookups, saved products and package dates in local storage. Settings lets users clear them.

## Limitations

- Camera scanning uses the browser `BarcodeDetector` API and works only in supporting browsers on HTTPS or localhost. Manual barcode entry is the fallback.
- Product-name search, package photo/OCR, and shared/cloud accounts are not implemented.
- Allergen declarations can be absent or incomplete. ScanWise does not diagnose illness or determine whether food is safe for a person with an allergy; check the current package.
- Open Food Facts may be unavailable or have no record for a barcode. A missing record is never filled with invented facts.
- Preferences are simple local text matches against returned ingredient wording, not medical screening or certification.
