# Image Style Sample for Wpf

### Description
As you probably already know, using the Map Suite API, you can easily display a point-based feature as an image. But how do you do the same thing for a line or a polygon-based feature? In this WPF project, we show you how to create custom Image Styles for both line and polygon features. With the new ImageAreaStyle, you can display a polygon feature that uses an image as its fill. You can see how an image for forest and water is used in the sample project. And with the new ImageLineStyle, you can do the same thing with line features. You'll see how an image of a pavement texture is used to represent streets.

Please refer to [Wiki](http://wiki.thinkgeo.com/wiki/thinkgeo_desktop_for_wpf) for the details.

![Screenshot](https://github.com/ThinkGeo/ImageStyleSample-ForWpf.NETCore/blob/master/Screenshot.png)

### Requirements

This sample makes use of the following NuGet Packages

[MapSuite 12.0.0](https://www.nuget.org/packages?q=ThinkGeo)

### About the Code
```csharp
[Serializable]
class ImageAreaStyle : Style
{
    private GeoImage geoImage = null;

    public ImageAreaStyle(GeoImage geoImage)
    {
        this.geoImage = geoImage;
    }

    protected override void DrawCore(IEnumerable<Feature> features, GeoCanvas canvas, Collection<SimpleCandidate> labelsInThisLayer, Collection<SimpleCandidate> labelsInAllLayers)
    {
        // Loop through all of the features being passed in to draw.
        foreach (Feature feature in features)
        {
            WellKnownType shapeWellKnownType = feature.GetWellKnownType();
            if (shapeWellKnownType == WellKnownType.Polygon)
            {
                PolygonShape polygonShape = new PolygonShape(feature.GetWellKnownBinary());
                canvas.DrawArea(polygonShape, new GeoTextureBrush(geoImage), DrawingLevel.LevelOne);
            }
            else if (shapeWellKnownType == WellKnownType.Multipolygon)
            {
                MultipolygonShape multiPolygonShape = new MultipolygonShape(feature.GetWellKnownBinary());
                canvas.DrawArea(multiPolygonShape, new GeoTextureBrush(geoImage), DrawingLevel.LevelOne);
            }
        }
    }
}
```
### Getting Help

[Map Suite Desktop for Wpf Wiki Resources](http://wiki.thinkgeo.com/wiki/thinkgeo_desktop_for_wpf)

[Map Suite Desktop for Wpf Product Description](https://thinkgeo.com/ui-controls#desktop-platforms)

[ThinkGeo Community Site](http://community.thinkgeo.com/)

[ThinkGeo Web Site](http://www.thinkgeo.com)

### Key APIs
This example makes use of the following APIs:

- [ThinkGeo.Core.Style](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.style)
- [ThinkGeo.Core.GeoImage](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.geoimage)
- [ThinkGeo.Core.GeoCanvas](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.geocanvas)
- [ThinkGeo.Core.SimpleCandidate](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.simplecandidate)
- [ThinkGeo.Core.Feature](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.feature)
- [ThinkGeo.Core.WellKnownType](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.wellknowntype)
- [ThinkGeo.Core.PolygonShape](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.polygonshape)
- [ThinkGeo.Core.DrawingLevel](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.drawinglevel)
- [ThinkGeo.Core.MultipolygonShape](http://wiki.thinkgeo.com/wiki/12.0/apis/thinkgeo.core.multipolygonshape)

### About Map Suite
Map Suite is a set of powerful development components and services for the .Net Core.

### About ThinkGeo
ThinkGeo is a GIS (Geographic Information Systems) company founded in 2004 and located in Frisco, TX. Our clients are in more than 40 industries including agriculture, energy, transportation, government, engineering, software development, and defense.
