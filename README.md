# digital-invoice-to-pdf

Convert Italian [FatturaPA](https://www.fatturapa.gov.it/it/lafatturapa/formatofatturapa/) electronic invoice XML files to PDF.

See an [example output](./assets/example.pdf).

## Usage

### As a library

```ts
import { xmlToPDF, xmlToJson, xmlToCompactJson } from "./src/index";

const pdfStream = await xmlToPDF(xmlString);
```

### As a server

The project includes a Fastify server with a file upload endpoint:

```bash
npm run build
npm start
# Server listens on http://localhost:3000

# Convert an XML invoice to PDF
curl -X POST http://localhost:3000/convert \
  -F "file=@invoice.xml" \
  --output invoice.pdf

# Specify language (it or de)
curl -X POST "http://localhost:3000/convert?lang=de" \
  -F "file=@invoice.xml" \
  --output invoice.pdf
```

## Exports

- `xmlToPDF(xml, options?)` -- converts FatturaPA XML to a PDF stream (via [react-pdf](https://react-pdf.org/))
- `xmlToJson(xml, options?)` -- parses XML to typed JSON using [xml2js](https://github.com/Leonidas-from-XIV/node-xml2js) (see `types/DigitalInvoiceJson`)
- `xmlToCompactJson(xml, options?)` -- produces a normalized `DigitalInvoice` object (see `types/DigitalInvoice`)
