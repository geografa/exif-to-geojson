# Exif To GeoJSON

This takes a directory full of images and makes a GeoJSON file with all of the found GPS points. This is adapted from https://github.com/hallahan/exif-to-geojson but uses [GL JS](https://www.mapbox.com/mapbox-gl-js/api/) for the map rendering library.

1. Put the images you want to create a corresponding GeoJSON file with in the img directory.
2. `node exif-to-geojson.js`
3. The output will be written to exif.geojson

Demo: [http://hallahan.github.io/exif-to-geojson](http://hallahan.github.io/exif-to-geojson)

After you run the script, you can see the geojson with pop-ups that link to the corresponding images
in `index.html`.

## Notes

1. The decoder does not seem to correctly decode the MakerNote and UserComment
fields in the exif object, so I just delete them so that we do not
have a bunch of un-decoded bytes wasting space in the JSON.

2. The GPSTimeStamp array is important, because this is the time
stamp of the moment the phone got the actual GPS coordinate that is
associated with the image. This is often not the same point in time
that the picture itself was taken. This is particularly true with
my phone which does not have a very reliable GPS unit.

3. The test directory is not unit tests, however, it does create json that
you can look at to see if you find reasonable results. This should be refactored
to produce unit tests.

4. The demo should be improved so that we can see multiple images where the GPS coordinates
are at the same point. This is particularly a problem with images from my phone, because
the GPS unit fails often and will tag many images with the same coordinates.