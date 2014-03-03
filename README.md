BabylonCSG
==========

Constructive Solid Geometry in BABYLON.js, based on csg.js

![](http://evanw.github.com/csg.js/image.png)

Constructive Solid Geometry (CSG) is a modeling technique that uses Boolean operations like union and intersection to combine 3D solids. This library implements CSG operations on meshes elegantly and concisely using BSP trees, and is meant to serve as an easily understandable implementation of the algorithm. All edge cases involving overlapping coplanar polygons in both solids are correctly handled.

This library is an adaptation for BABYLON.js meshes, original documentation on csg.js can be found here :
https://github.com/evanw/csg.js/

#Example

	var a = BABYLON.Mesh.CreateBox("box", 500, scene);
	var b = BABYLON.Mesh.CreateBox("box", 500, scene);

	a.position.y += 500;
	b.position.y += 250;
	b.rotation.y += Math.PI/8;

	var aCSG = BABYLON.CSG.FromMesh(a);
	var bCSG = BABYLON.CSG.FromMesh(b);

	var subCSG = bCSG.subtract(aCSG);

	// Disposing original meshes since we don't want to see them on the scene
	a.dispose();
	b.dispose();

	subCSG.toMesh("csg", new BABYLON.StandardMaterial("mat", scene), scene);

![](http://f.cl.ly/items/1f1v2Y2O1Y1e1I3f2j2I/Capture.PNG)
