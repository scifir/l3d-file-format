# L3D file format
**Version:** 1.0.0-beta
**Author:** [Ismael Correa Castro](https://iarfen.github.io) (ORCID 0009-0007-3815-7053)
**Last updated:** 2023-07-31

**L3D** is an XML file format that allows to create very lightweight 3d models. The way it works is by describing geometric figures in 3d, instead of describing them by triangles. With it, it's possible to have a high amount of files of 3d models without consuming a lot of space inside the hard disk. Then, it's possible to download 3d software without taking high amounts of time.

An example of an L3D file is the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<l3d>
	<cylinder p="1 m,2 m,1 m;20º,10º" r="5 dm" h="1 m" c="123,234,123,240" s1="(1 m,1 m,1 m),(5 dm,3 dm,1 m);(3 m,2 m,5 dm)" />
	<sphere p="1 m,1 m,1 m;0º,0º" r="1 m" t="death_star.svg">
		<sphere p="1 m,1 m,2 m:0º,0º" r="3 dm" o="sub" />
	</sphere>
</l3d>
```

The previous XML specifies a cylinder with position (1 m,2 m,1 m) and rotation (20º,10º), of radius 5 dm and height 1 m. The color of the cylinder is specified in rgba as (123,234,123,240). The cylinder has a Bezier surface whose control points are the ones specified inside the attribute s, that's, the control points (1 m,1 m,1 m) and (5 dm,3 dm,1 m) for the coordinate u and the control point (3 m,2 m,5 dm) for the coordinate v. Also, it specifies an sphere of position (1 m,1 m,1 m), rotation (0º,0º) and radius 1 m. The texture of the sphere is the file death_star.svg.

### Advantages

- **Extremely light** 3d file format compared to common 3d formats that instead of specifying geometric figures specify triangles.
- **Controlled VRAM consumption**, the 3d figures can be drawn with more or less triangles depending on the needs of the software and the level of zoom on them. Common 3d formats just draw all the triangles.
- All positions and lengths are specified using **units of measurement**, instead of decimal numbers without units.
- By using it instead of a common 3d file format, a videogame and any other software that uses 3d **reduces the size** of its 3d assets from what's usually GB to just MB.

### Author

The DNA file format has been created by [Ismael Correa Castro](https://iarfen.github.io), an industrial civil engineer and scientist of 32 years old. You can email him if you find bugs, you want to request new features, or have any other need, at ismael.correa.castro@gmail.com. His ORCID is 0009-0007-3815-7053, if you want to reference this work inside any publication.

### Funding

The **Scifir Foundation** is looking for **funding**, in order to do some digital marketing and pay some other needs of his projects. If you want to support his technologies, and **science will thank you** for that, you can donate in this [sponsors page](https://github.com/sponsors/iarfen).

## XML elements

The XML elements for l3d files are the following:

| XML element | Use | Description
| -------- | ---------| ----------------------------|
| \<l3d\> | Required, top level | Top-level element to create 3d figures inside |
| \<sphere\> | Optional, any number | Creates a new sphere |
| \<ellipsoid\> | Optional, any number | Creates a new ellipsoid |
| \<cylinder\> | Optional, any number | Creates a new cylinder |
| \<cube\> | Optional, any number | Creates a new cube |
| \<cuboid\> | Optional, any number | Creates a new cuboid |
| \<cone\> | Optional, any number | Creates a new cone |
| \<pyramid\> | Optional, any number | Creates a new pyramid |
| \<prism\> | Optional, any number | Creates a new prism |
| \<torus\> | Optional, any number | Creates a new torus |

### \<l3d\>

A l3d element is the top element of l3d files.

### Common attributes

All l3d elements have the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| p | Required | Position of the 3d figure |
| c | Optional | Color of the 3d figure. Required if there's no texture |
| t | Optional | Texture of the 3d figure. Required if there's no color |
| s{n} | Optional | Surfaces of the 3d figure. Depending on the 3d figure, the n represents one of his surfaces or another |
| o | Required for inner elements | It specifies if the element adds or substracts to the parent element, with a value of "add" for additions and "sub" for substractions |

### Faces

The faces of some XML elements, like the pyramid and the prism, are specified as polygons. They have to specify the position of each vertex that conforms the polygon, by writing the position on the x and y axis of each point. The positions are specified in units of lengths because, in this file format, as is the point of view of the author of it, the space, real or virtual, always exist as space and, then, there doesn't exist positions without units, as some textbooks of geometry say. Inside this file format, all spaces, real and virtual, have units of length, there doesn't exist an space without units of measurement for it.

To specify a polygon it's written each point that conforms it, and then the next. An example is the following snippet of code:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<prism p="0 m,0 m,0 m" f="(0 m,5 dm),(1 m,2 dm),(2 m,3 dm)" h="3 m" c="100,100,100,255" />
```

In the previous example, the face corresponds to a polygon, which is a triangle, as can be easily seen given the fact that it has 3 points.

### Axis of symmetry

The axis of symmetry of some XML elements, like the prism, the pyramid and the cylinder, can be curved to give the 3d figure the shape wanted. The curve is specified using Bezier curves, which are similar to the Bezier surfaces used to alter the surfaces. Bezier curves use control points to specify the level of curvature.

An example of an axis of symmetry is the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cone p="0 m,0 m,0 m" h="4 m" c="150,200,55,255" m="(2 m,0 m,1 m)" />
```

In the previous example, a control point in the position (2 m,0 m) is established.

### \<sphere\>

A sphere element creates an sphere. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| r | Required | Radius of the sphere |

### \<ellipsoid\>

An ellipsoid element creates an ellipsoid. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| x | Required | Length of the x-axis of the ellipsoid |
| y | Required | Length of the y-axis of the ellipsoid |
| z | Required | Length of the z-axis of the ellipsoid |

### \<cylinder\>

A cylinder element creates a cylinder. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| r | Required | Radius of the cylinder |
| h | Required | Height of the cylinder |

### \<cube\>

A cube element creates a cube. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| a | Required | Length of the cube |

### \<cuboid\>

A cuboid element creates a cuboid. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| a | Required | Length of the x-axis of the cuboid |
| b | Required | Length of the y-axis of the cuboid |
| c | Required | Length of the z-axis of the cuboid |

### \<cone\>

A cone element creates a cone. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| r | Required | Radius of the cone |
| h | Required | Height of the cone |

### \<pyramid\>

A pyramid element creates a pyramid. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| h | Required | Height of the pyramid |
| f | Required | Face of the pyramid |

### \<prism\>

A prism element creates a prism. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| h | Required | Height of the prism |
| f | Required | Face of the prism |

### \<torus\>

A torus element creates a torus. It has the following attributes:

| Attribute | Required | Description
| -------- | --------- | ----------------------------|
| R | Required | Radius from the center of the tube to the center of the torus |
| r | Required | Radius of the tube |

## History

L3D has been created in **2007** by [Ismael Correa Castro](https://iarfen.github.io), when he was building a game engine and a 3d format to use for virtual worlds. Then, this file format is a result of years of work developing videogames, among other 3d software. It's merit, for that reason, of that kind of game developers, who work passionately to ammeliorate videogames and the informatics, and it's a proof that passionate work on videogames and informatics gives good results. There are a good amount of open source projects focused on ammeliorating videogames, and this file format is expected to be one of those projects.

Un 2007, L3D has been created as part of the game engine in that year called **Yggdrassil**, a very flexible game engine created by [Ismael Correa Castro](https://iarfen.github.io). In those times, and still at the present, there wasn't a good solution for 3d files, there was instead a very high consumption of hard disk and VRAM with all 3d technologies, and it was important to have then a 3d technology with a lower consumption of resources. For that purpose, L3D has born, and since then it has been part of the central scientific technologies of Scifir, used in all cases where a description of 3d figures is needed, as happens not only in videogames, but in nanotechnology and scientific machines in general. L3D is published open source, and can be used by anyone who needs it for creating videogames, 3d software or any scientific tool, cause it's very good in accomplishing his purpose of providing a 3d system easy to use and with very low consumption of resources compared to the other 3d technologies.
