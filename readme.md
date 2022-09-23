# Geogebra converter to other formats

Example output from geogebra-analyzer:

This XML excerpt...
```
  <element type="numeric" label="elev">
  	<value val="29"/>
  	<slider min="0" max="90" absoluteScreenLocation="true" width="5" x="54" y="178" fixed="false" horizontal="true" showAlgebra="true"/>
  	<lineStyle thickness="10" type="0" typeHidden="1"/>
  	<show object="true" label="true"/>
  	<objColor r="0" g="0" b="0" alpha="0.10000000149011612"/>
  	<layer val="0"/>
  	<labelMode val="1"/>
  	<animation step="1" speed="1" type="0" playing="false"/>
  </element>
  <command name="Point">
  	<input a0="xAxis"/>
  	<output a0="mirrorBase"/>
  </command>
  <element type="point" label="mirrorBase">
  	<show object="true" label="true" ev="4"/>
  	<objColor r="97" g="97" b="97" alpha="0"/>
  	<layer val="0"/>
  	<labelMode val="0"/>
  	<animation step="0.1" speed="1" type="1" playing="false"/>
  	<pointSize val="9"/>
  	<pointStyle val="0"/>
  	<coords x="16" y="0" z="1"/>
  </element>
  <command name="OrthogonalLine">
  	<input a0="mirrorBase" a1="xOyPlane"/>
  	<output a0="mirrorBoom"/>
  </command>
  <element type="line3d" label="mirrorBoom">
  	<show object="true" label="false" ev="4"/>
  	<objColor r="0" g="0" b="0" alpha="0"/>
  	<layer val="0"/>
  	<labelMode val="0"/>
  	<lineStyle thickness="1" type="15" typeHidden="1"/>
  	<eqnStyle style="parametric" parameter="λ"/>
  	<coords ox="16" oy="0" oz="0" ow="1" vx="0" vy="0" vz="1" vw="0"/>
  </element> 
```

...becomes this list:

```
  elev = Slider(0,90)
  mirrorBase = Point(xAxis) Object
  mirrorBoom = OrthogonalLine(mirrorBase, xOyPlane) Object
```

... which exploded contains:

```
  elev: {…}
    formulaStr: "Slider(0,90)"
    functionName: "Slider"
    parameters: (2) […]
      0: "0"
      1: "90"
      length: 2


mirrorBase: {…}
  formulaStr: "Point(xAxis)"
  functionName: "Point"
  parameters: (1) […]
    0: "xAxis"
    length: 1



mirrorBoom: {…}
  formulaStr: "OrthogonalLine(mirrorBase, xOyPlane)"
  functionName: "OrthogonalLine"
  parameters: (2) […]
    0: "mirrorBase"
    1: "xOyPlane"
    length: 2
```
  
Final objective would be to replace each parameter by its definition, to have a single string defining each object.
