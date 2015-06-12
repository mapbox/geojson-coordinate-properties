# geojson-coordinateProperties

A [GeoJSON](http://geojson.org/) extension proposal that adds an encoding
for time & heart rate data along a `LineString` geometry.

## Requirements Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC2119].

## Definitions

JavaScript Object Notation (JSON), and the terms object, name, value, array, number, true, false, and null are to be interpreted as defined in [RFC7159].

Inside this document the term "geometry type" refers to the seven case-sensitive strings: "Point", "MultiPoint", "LineString", "MultiLineString", "Polygon", "MultiPolygon", and "GeometryCollection".

As another shorthand notation, the term "GeoJSON types" refers to the nine case-sensitive strings "Feature", "FeatureCollection" and the geometry types listed above.

## Example

A GeoJSON feature collection with `coordinateProperties`:

```json
{
    "type": "FeatureCollection",
    "features": [{
        "type": "Feature",
        "geometry": {
            "type": "LineString",
            "coordinates": [
                [102.0, 0.0],
                [103.0, 1.0],
                [104.0, 0.0],
                [105.0, 1.0]
            ]
        },
        "properties": {
            "prop0": "value0",
            "prop1": 0.0,
            "coordinateProperties": {
                "times": [
                    1434126869275,
                    1434136869275,
                    1434146869275,
                    1434166869275
                ]
            }
        }
    }]
}
```

## coordinateProperties

`coordinateProperties` is a special property that MAY be included in the `properties`
member of a `Feature` object. A `Feature` object with `coordinateProperties` defined
in its `properties` MUST contain a geometry object of type `LineString`.

`coordinateProperties` MAY contain one or more members, which each MUST have a value
of type Array. Each Array value MUST have have the same length
as the `coordinates` member of the LineString geometry of that Feature.
Members can have any name, but semantics of two names are defined:

### times

A `times` member of the `coordinateProperties` MUST contain values that are either

* A Number corresponding to a Unix timestamp in uniseconds since 1 January 1970 00:00:00 UTC.
* A String formatted as ISO 8601
* `null`, indicating no data for this coordinate

### heart

A `heart` member of the `coordinateProperties` MUST contain values that are either

* A Number indicating heart-beats per minute
* `null`, indicating no data for this coordinate

## see also

* [Mailing list discussion about values along lines](http://lists.geojson.org/htdig.cgi/geojson-geojson.org/2013-August/thread.html#3660)
