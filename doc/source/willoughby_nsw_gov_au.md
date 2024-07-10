# Willoughby City Council (NSW)

Support for schedules provided by [Willoughby City Council Waste and street sweeping services](https://www.willoughby.nsw.gov.au/Residents/Waste-and-recycling/Household-bin-services/Waste-and-street-sweeping-services).

## Configuration via configuration.yaml

```yaml
waste_collection_schedule:
  sources:
    - name: willoughby_nsw_gov_au
      args:
        post_code: POST_CODE
        suburb: SUBURB
        street_name: STREET_NAME
        street_number: STREET_NUMBER
```

### Configuration Variables

**post_code**  
*(string) (required)*

**suburb**  
*(string) (required)*

**street_name**  
*(string) (required)*

**street_number**  
*(string) (required)*

## Example

```yaml
waste_collection_schedule:
  sources:
    - name: willoughby_nsw_gov_au
      args:
        post_code: 2068
        suburb: North Willoughby
        street_name: Penshurst St
        street_number: 315
```

## How to get the source arguments

Visit the [Willoughby City Council Waste and street sweeping services](https://www.willoughby.nsw.gov.au/Residents/Waste-and-recycling/Household-bin-services/Waste-and-street-sweeping-services) page, and search for your address. The street address arguments used to configure hacs_waste_collection_schedule should exactly match the street address shown in the autocomplete result.

## How this integration uses Blacktown Council's APIs

Two API calls are currently needed to retrieve waste collection schedule results from Blacktown Council:
1. The address search API at https://www.willoughby.nsw.gov.au/api/v1/myarea/search
2. The waste services API at https://www.willoughby.nsw.gov.au/ocapi/Public/myarea/wasteservices

This integration does the following:
1. Calls the address search API to retrieve the "location ID" for the given location. Eg. https://www.willoughby.nsw.gov.au/api/v1/myarea/search?keywords=315+Penshurst+St+North+Willoughby+NSW+2068
2. Retrieves waste/collection info from the waste services API using the "location ID" retrieved in step #1. Eg. https://www.willoughby.nsw.gov.au/ocapi/Public/myarea/wasteservices?geolocationid=1b456d32-33d4-40f7-8331-459a38c6b606&ocsvclang=en-AU
3. Parses the HTML returned by the waste services API in step #2 to extract the data


# Similarities with other sources

For future work it's good to note that Blacktown City Council and Campbelltown City Council uses the same APIs as Willoughby City Council, to the point I was able to copy and paste their files with minimal modification.
 