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

#Multi-Material
You may want to keep one subMesh for each mesh you used CSG on. This library allows you to do so :

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

	// Set up a MultiMaterial
	var multiMat = new BABYLON.MultiMaterial("multiMat", scene);
	var mat0 = new BABYLON.StandardMaterial("mat0", scene);
	var mat1 = new BABYLON.StandardMaterial("mat1", scene);

	mat0.diffuseColor.copyFromFloats(0.8, 0.2, 0.2);
	mat1.diffuseColor.copyFromFloats(0.2, 0.8, 0.2);    

	// Submeshes are built in order : mat0 will be for the first cube, and mat1 for the second
	multiMat.subMaterials.push(mat0, mat1);

	// Last parameter to true means you want to build 1 subMesh for each mesh involved
	subCSG.toMesh("csg", multiMat, scene, true);

![](http://f.cl.ly/items/3G2A3B002C2k0P162A0D/Capture.PNG)
