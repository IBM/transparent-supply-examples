Welcome to the IBM Blockchain Transparent Supply&trade; Examples!

# Trace API examples
The code in this repository is intended to be a collection of code examples that exemplify the capabilities of the IBM Blockchain Transparent Supply API.  Currently this is focused only on the Trace APIs, defined here: http://developer.transparentsupply.ibm.com/ift/api/outbound/api-docs/ *.  These examples show how to access your entitled data in Blockchain Transparent Supply to solve real world problems.

*\* All references to URLs containing developer.transparentsupply.ibm.com require signing up for a trial to the Transparent Supply Developer Playground to get access, but can be replaced with the base domain for any existing IBM Food Trust or Blockchain Transparent Supply customers (e.g. food.ibm.com)*

## harvested-epcs
This returns a list of EPCs that were harvested from a particular location within a particular timeframe, for a set of GTINs (product IDs).  This leverages the 'events' endpoint.

## impacted-epcs
This returns a list of EPCs that contain ingredients harvested from a particular location within a particular timeframe, for a set of GTINs.  This leverages the 'events' endpoint and assumes that the harvested EPCs were transformed directly into other EPCs (or were never transformed), and does not attempt to handle multiple layers of transformation, or aggregations into transformations.

## impacted-transactions
This returns a list of transaction identifiers (purchase order IDs and despatch advice IDs) that contain ingredients that were harvested from a particular location within a particular timeframe, for a set of GTINs.  This again uses the 'events' endpoint and assumes that the harvested EPCs were transformed directly into other EPCs (or were never transformed), and does not attempt to handle multiple layers of transformation, or aggregations into transformations.  It also assumes that the impacted EPCs are shipped to a partner as a child of an aggregation event and that the transaction IDs are referenced on that event.

## ingredient-sources
This returns a list of products with their final locations alongside their ingredients and the source locations for each of the ingredients.  This will make assumptions about the overall flow of products (it will assume a `STORE` is a more likely final location than a `FARM`, and the reverse for source locations).  In CSV format, it will also limit the final/source locations to a single location each, sorted by timestamp and by the assumption described previously.  This uses a variety of endpoints including the 'trace' endpoint.

## product-destinations
This endpoint will provide a list of ingredients and the source locations alongside the most downstream product they produce (same formatting as `/ingredient-sources`).  This will make assumptions about the overall flow of products (it will assume a `STORE` is a more likely final location than a `FARM`, and the reverse for source locations).  In CSV format, it will also limit the final/source locations to a single location each, sorted by timestamp and by the assumption described previously.

# Usage
1) Clone the code locally
2) Nagigate to the top level, and execute:
   - `npm install`
   - `npm run build`
   - `npm run start`
3) From your browser, open http://localhost:5474/api-samples/recall-assistant/v1/swagger/

There is also the option to use our command line interface
1) Clone the code locally
2) Nagigate to the top level, and execute:
   - `npm install`
   - `npm run build`
3) Run either of the following commands to see the parameters available parameters
   - `npm run cli -- -h`
   - `node bin/assistant-cli.js -h`

### Product and facility IDs
This application requires entering product and facility identifiers as inputs. The [products page](https://developer.transparentsupply.ibm.com/manage-data/products) and [facilities page](https://developer.transparentsupply.ibm.com/manage-data/facilities) shows the products available if you choose "All" from the Organization selector. Please note that products and facility identifiers will show in a truncated format if they leverage an [IBM solution identifier](https://developer.transparentsupply.ibm.com/ift/help/reference/solution-identifiers), so *urn:ibm:ift:product:class:* may need to be prepended to a product ID or *urn:ibm:ift:location:loc:* to a facility ID if values are copied from those pages.
