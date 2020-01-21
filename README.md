# Vertex Shader: Simple Morph

Vertex shader that morphs geometry into primitive shapes.

<p align="center">
  <img align="center" src="example.gif" title="Dungeons & fat Dragons"><br>
  Dragon made by the artist <a href="https://assetstore.unity.com/publishers/23554">Dungeon Mason</a>.
</p>

This use case has been made with Unity. To use the shader just add a material to a mesh renderer and attach the provided C# script to the gameobject.

To morph into a cube the vertices are expanded and clamped to fit the cube dimensions.
```
...

float4 position = v.position;
position.xyz *= _OffsetFactor / length(position.xyz);
position.xyz = clamp(position.xyz, -_Size, _Size);
f.position = UnityObjectToClipPos(lerp(v.position, position, _BlendFactor));

...
```

To morph into a sphere the vertices are expanded but not clamped.
```
...

float4 position = v.position;
position.xyz *= _OffsetFactor / length(position.xyz);
f.position = UnityObjectToClipPos(lerp(v.position, position, _BlendFactor));

...
```
References.
> [Graphic Shaders, Chapter 16](http://web.engr.oregonstate.edu/~mjb/cgeducation/ShadersBookSecond/)
