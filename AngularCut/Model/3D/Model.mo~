'# MWS Version: Version 2021.1 - Nov 10 2020 - ACIS 30.0.1 -

'# length = mm
'# frequency = GHz
'# time = ns
'# frequency range: fmin = 40 fmax = 45
'# created = '[VERSION]2021.1|30.0.1|20201110[/VERSION]


'@ use template: Antenna - Planar_3.cfg

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
'set the units
With Units
    .Geometry "mm"
    .Frequency "GHz"
    .Voltage "V"
    .Resistance "Ohm"
    .Inductance "H"
    .TemperatureUnit  "Kelvin"
    .Time "ns"
    .Current "A"
    .Conductance "Siemens"
    .Capacitance "F"
End With

'----------------------------------------------------------------------------

Plot.DrawBox True

With Background
     .Type "Normal"
     .Epsilon "1.0"
     .Mu "1.0"
     .XminSpace "0.0"
     .XmaxSpace "0.0"
     .YminSpace "0.0"
     .YmaxSpace "0.0"
     .ZminSpace "0.0"
     .ZmaxSpace "0.0"
End With

With Boundary
     .Xmin "expanded open"
     .Xmax "expanded open"
     .Ymin "expanded open"
     .Ymax "expanded open"
     .Zmin "expanded open"
     .Zmax "expanded open"
     .Xsymmetry "none"
     .Ysymmetry "none"
     .Zsymmetry "none"
End With

' optimize mesh settings for planar structures

With Mesh
     .MergeThinPECLayerFixpoints "True"
     .RatioLimit "20"
     .AutomeshRefineAtPecLines "True", "6"
     .FPBAAvoidNonRegUnite "True"
     .ConsiderSpaceForLowerMeshLimit "False"
     .MinimumStepNumber "5"
     .AnisotropicCurvatureRefinement "True"
     .AnisotropicCurvatureRefinementFSM "True"
End With

With MeshSettings
     .SetMeshType "Hex"
     .Set "RatioLimitGeometry", "20"
     .Set "EdgeRefinementOn", "1"
     .Set "EdgeRefinementRatio", "6"
End With

With MeshSettings
     .SetMeshType "HexTLM"
     .Set "RatioLimitGeometry", "20"
End With

With MeshSettings
     .SetMeshType "Tet"
     .Set "VolMeshGradation", "1.5"
     .Set "SrfMeshGradation", "1.5"
End With

' change mesh adaption scheme to energy
' 		(planar structures tend to store high energy
'     	 locally at edges rather than globally in volume)

MeshAdaption3D.SetAdaptionStrategy "Energy"

' switch on FD-TET setting for accurate farfields

FDSolver.ExtrudeOpenBC "True"

PostProcess1D.ActivateOperation "vswr", "true"
PostProcess1D.ActivateOperation "yz-matrices", "true"

With FarfieldPlot
	.ClearCuts ' lateral=phi, polar=theta
	.AddCut "lateral", "0", "1"
	.AddCut "lateral", "90", "1"
	.AddCut "polar", "90", "1"
End With

'----------------------------------------------------------------------------

With MeshSettings
     .SetMeshType "Hex"
     .Set "Version", 1%
End With

With Mesh
     .MeshType "PBA"
End With

'set the solver type
ChangeSolverType("HF Time Domain")

'----------------------------------------------------------------------------

'@ define material: Copper (annealed)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Material
     .Reset
     .Name "Copper (annealed)"
     .Folder ""
     .FrqType "static"
     .Type "Normal"
     .SetMaterialUnit "Hz", "mm"
     .Epsilon "1"
     .Mu "1.0"
     .Kappa "5.8e+007"
     .TanD "0.0"
     .TanDFreq "0.0"
     .TanDGiven "False"
     .TanDModel "ConstTanD"
     .KappaM "0"
     .TanDM "0.0"
     .TanDMFreq "0.0"
     .TanDMGiven "False"
     .TanDMModel "ConstTanD"
     .DispModelEps "None"
     .DispModelMu "None"
     .DispersiveFittingSchemeEps "Nth Order"
     .DispersiveFittingSchemeMu "Nth Order"
     .UseGeneralDispersionEps "False"
     .UseGeneralDispersionMu "False"
     .FrqType "all"
     .Type "Lossy metal"
     .SetMaterialUnit "GHz", "mm"
     .Mu "1.0"
     .Kappa "5.8e+007"
     .Rho "8930.0"
     .ThermalType "Normal"
     .ThermalConductivity "401.0"
     .SpecificHeat "390", "J/K/kg"
     .MetabolicRate "0"
     .BloodFlow "0"
     .VoxelConvection "0"
     .MechanicsType "Isotropic"
     .YoungsModulus "120"
     .PoissonsRatio "0.33"
     .ThermalExpansionRate "17"
     .Colour "1", "1", "0"
     .Wireframe "False"
     .Reflection "False"
     .Allowoutline "True"
     .Transparentoutline "False"
     .Transparency "0"
     .Create
End With

'@ new component: component1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Component.New "component1"

'@ define brick: component1:Ground

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Ground" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-6", "6" 
     .Yrange "-6", "6" 
     .Zrange "0", "-0.05" 
     .Create
End With

'@ define material: FR-4 (lossy)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Material
     .Reset
     .Name "FR-4 (lossy)"
     .Folder ""
     .FrqType "all"
     .Type "Normal"
     .SetMaterialUnit "GHz", "mm"
     .Epsilon "4.3"
     .Mu "1.0"
     .Kappa "0.0"
     .TanD "0.025"
     .TanDFreq "10.0"
     .TanDGiven "True"
     .TanDModel "ConstTanD"
     .KappaM "0.0"
     .TanDM "0.0"
     .TanDMFreq "0.0"
     .TanDMGiven "False"
     .TanDMModel "ConstKappa"
     .DispModelEps "None"
     .DispModelMu "None"
     .DispersiveFittingSchemeEps "General 1st"
     .DispersiveFittingSchemeMu "General 1st"
     .UseGeneralDispersionEps "False"
     .UseGeneralDispersionMu "False"
     .Rho "0.0"
     .ThermalType "Normal"
     .ThermalConductivity "0.3"
     .SetActiveMaterial "all"
     .Colour "0.94", "0.82", "0.76"
     .Wireframe "False"
     .Transparency "0"
     .Create
End With

'@ define brick: component1:Substrate

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Substrate" 
     .Component "component1" 
     .Material "FR-4 (lossy)" 
     .Xrange "-6", "6" 
     .Yrange "-6", "6" 
     .Zrange "0.51", "0" 
     .Create
End With

'@ activate local coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "local"

'@ move wcs

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.MoveWCS "local", "0.0", "0.0", "0.51"

'@ define brick: component1:Patch

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Patch" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-1.6", "1.6" 
     .Yrange "-1.6", "1.6" 
     .Zrange "0", "0.05" 
     .Create
End With

'@ define brick: component1:Diagonal

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Diagonal" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-0.5", "0.5" 
     .Yrange "-0.1", "0.1" 
     .Zrange "0", "0.05" 
     .Create
End With

'@ transform: rotate component1:Diagonal

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:Diagonal" 
     .Origin "Free" 
     .Center "0", "0", "0" 
     .Angle "0", "0", "45" 
     .MultipleObjects "False" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Transform "Shape", "Rotate" 
End With

'@ boolean subtract shapes: component1:Patch, component1:Diagonal

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:Diagonal"

'@ define brick: component1:Feed

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Feed" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-0.4", "0.4" 
     .Yrange "-0.5", "0.5" 
     .Zrange "0", "0.05" 
     .Create
End With

'@ transform: translate component1:Feed

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:Feed" 
     .Vector "0", "-2.1", "0" 
     .UsePickedPoints "False" 
     .InvertPickedPoints "False" 
     .MultipleObjects "False" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Transform "Shape", "Translate" 
End With

'@ boolean add shapes: component1:Patch, component1:Feed

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Add "component1:Patch", "component1:Feed"

'@ define brick: component1:Feedcut

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "Feedcut" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-0.3", "0.3" 
     .Yrange "-0.1", "0.1" 
     .Zrange "0", "0.05" 
     .Create
End With

'@ transform: translate component1:Feedcut

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:Feedcut" 
     .Vector "0", "-1.7", "0" 
     .UsePickedPoints "False" 
     .InvertPickedPoints "False" 
     .MultipleObjects "False" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Transform "Shape", "Translate" 
End With

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "-0.4", "-1.6" 
     .LineTo "-0.3", "-1.6" 
     .LineTo "-0.3", "-1.8" 
     .LineTo "-0.4", "-1.8" 
     .LineTo "-0.4", "-1.6" 
     .Create 
End With

'@ boolean subtract shapes: component1:Patch, component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:solid1"

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "0.4", "-1.6" 
     .LineTo "0.3", "-1.6" 
     .LineTo "0.3", "-1.8" 
     .LineTo "0.4", "-1.8" 
     .LineTo "0.4", "-1.6" 
     .Create 
End With

'@ boolean subtract shapes: component1:Patch, component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:solid1"

'@ activate global coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "global"

'@ activate local coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "local"

'@ move wcs

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.MoveWCS "local", "0.0", "0.0", "-0.51"

'@ activate global coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "global"

'@ define cylinder: component1:Axilegr

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Cylinder 
     .Reset 
     .Name "Axilegr" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .OuterRadius "0.10" 
     .InnerRadius "0" 
     .Axis "z" 
     .Zrange "0", "-0.05" 
     .Xcenter "0" 
     .Ycenter "-2.2" 
     .Segments "0" 
     .Create 
End With

'@ boolean subtract shapes: component1:Ground, component1:Axilegr

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Ground", "component1:Axilegr"

'@ boolean add shapes: component1:Patch, component1:Feedcut

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Add "component1:Patch", "component1:Feedcut"

'@ define cylinder: component1:Axilesub

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Cylinder 
     .Reset 
     .Name "Axilesub" 
     .Component "component1" 
     .Material "FR-4 (lossy)" 
     .OuterRadius "0.045" 
     .InnerRadius "0.0" 
     .Axis "z" 
     .Zrange "0.51", "0" 
     .Xcenter "0" 
     .Ycenter "-2.2" 
     .Segments "0" 
     .Create 
End With

'@ boolean subtract shapes: component1:Substrate, component1:Axilesub

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Substrate", "component1:Axilesub"

'@ define cylinder: component1:Axileouter

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Cylinder 
     .Reset 
     .Name "Axileouter" 
     .Component "component1" 
     .Material "PEC" 
     .OuterRadius "0.10" 
     .InnerRadius "0.08" 
     .Axis "z" 
     .Zrange "0", "-0.5" 
     .Xcenter "0" 
     .Ycenter "-2.2" 
     .Segments "0" 
     .Create 
End With

'@ define material: Air

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Material
     .Reset
     .Name "Air"
     .Folder ""
     .FrqType "all"
     .Type "Normal"
     .SetMaterialUnit "Hz", "mm"
     .Epsilon "1.00059"
     .Mu "1.0"
     .Kappa "0"
     .TanD "0.0"
     .TanDFreq "0.0"
     .TanDGiven "False"
     .TanDModel "ConstKappa"
     .KappaM "0"
     .TanDM "0.0"
     .TanDMFreq "0.0"
     .TanDMGiven "False"
     .TanDMModel "ConstKappa"
     .DispModelEps "None"
     .DispModelMu "None"
     .DispersiveFittingSchemeEps "General 1st"
     .DispersiveFittingSchemeMu "General 1st"
     .UseGeneralDispersionEps "False"
     .UseGeneralDispersionMu "False"
     .Rho "1.204"
     .ThermalType "Normal"
     .ThermalConductivity "0.026"
     .SpecificHeat "1005", "J/K/kg"
     .SetActiveMaterial "all"
     .Colour "0.682353", "0.717647", "1"
     .Wireframe "False"
     .Transparency "0"
     .Create
End With

'@ define cylinder: component1:Axileair

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Cylinder 
     .Reset 
     .Name "Axileair" 
     .Component "component1" 
     .Material "Air" 
     .OuterRadius "0.08" 
     .InnerRadius "0.045" 
     .Axis "z" 
     .Zrange "0", "-0.5" 
     .Xcenter "0" 
     .Ycenter "-2.2" 
     .Segments "0" 
     .Create 
End With

'@ define cylinder: component1:Axileinn

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Cylinder 
     .Reset 
     .Name "Axileinn" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .OuterRadius "0.045" 
     .InnerRadius "0.0" 
     .Axis "z" 
     .Zrange "0.51", "-0.5" 
     .Xcenter "0" 
     .Ycenter "-2.2" 
     .Segments "0" 
     .Create 
End With

'@ boolean add shapes: component1:Patch, component1:Axileinn

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Add "component1:Patch", "component1:Axileinn"

'@ pick edge

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Pick.PickEdgeFromId "component1:Axileouter", "1", "1"

'@ define port: 1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Port 
     .Reset 
     .PortNumber "1" 
     .Label ""
     .Folder ""
     .NumberOfModes "1"
     .AdjustPolarization "False"
     .PolarizationAngle "0.0"
     .ReferencePlaneDistance "0"
     .TextSize "50"
     .TextMaxLimit "0"
     .Coordinates "Picks"
     .Orientation "positive"
     .PortOnBound "True"
     .ClipPickedPortToBound "False"
     .Xrange "-0.1", "0.1"
     .Yrange "-2.3", "-2.1"
     .Zrange "-0.5", "-0.5"
     .XrangeAdd "0.0", "0.0"
     .YrangeAdd "0.0", "0.0"
     .ZrangeAdd "0.0", "0.0"
     .SingleEnded "False"
     .WaveguideMonitor "False"
     .Create 
End With

'@ define frequency range

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solver.FrequencyRange "24", "32"

'@ define time domain solver parameters

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Mesh.SetCreator "High Frequency" 

With Solver 
     .Method "Hexahedral"
     .CalculationType "TD-S"
     .StimulationPort "All"
     .StimulationMode "All"
     .SteadyStateLimit "-40"
     .MeshAdaption "False"
     .AutoNormImpedance "False"
     .NormingImpedance "50"
     .CalculateModesOnly "False"
     .SParaSymmetry "False"
     .StoreTDResultsInCache  "False"
     .FullDeembedding "False"
     .SuperimposePLWExcitation "False"
     .UseSensitivityAnalysis "False"
End With

'@ set PBA version

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Discretizer.PBAVersion "2020111021"

'@ define monitor: e-field (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "28" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: surface-current (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "surface-current (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Surfacecurrent" 
     .MonitorValue "28" 
     .Create 
End With

'@ define monitor: h-field (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "28" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=28)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "28" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ define monitor: power (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "power (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Powerflow" 
     .MonitorValue "28" 
     .Create 
End With

'@ define monitor: h-energy (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-energy (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Henergy" 
     .MonitorValue "28" 
     .Create 
End With

'@ farfield plot options

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With FarfieldPlot 
     .Plottype "3D" 
     .Vary "angle1" 
     .Theta "90" 
     .Phi "90" 
     .Step "5" 
     .Step2 "5" 
     .SetLockSteps "True" 
     .SetPlotRangeOnly "False" 
     .SetThetaStart "0" 
     .SetThetaEnd "180" 
     .SetPhiStart "0" 
     .SetPhiEnd "360" 
     .SetTheta360 "False" 
     .SymmetricRange "False" 
     .SetTimeDomainFF "False" 
     .SetFrequency "-1" 
     .SetTime "0" 
     .SetColorByValue "True" 
     .DrawStepLines "False" 
     .DrawIsoLongitudeLatitudeLines "False" 
     .ShowStructure "True" 
     .ShowStructureProfile "True" 
     .SetStructureTransparent "False" 
     .SetFarfieldTransparent "False" 
     .AspectRatio "Free" 
     .ShowGridlines "True" 
     .SetSpecials "enablepolarextralines" 
     .SetPlotMode "Directivity" 
     .Distance "1" 
     .UseFarfieldApproximation "True" 
     .IncludeUnitCellSidewalls "True" 
     .SetScaleLinear "False" 
     .SetLogRange "40" 
     .SetLogNorm "0" 
     .DBUnit "0" 
     .SetMaxReferenceMode "abs" 
     .EnableFixPlotMaximum "False" 
     .SetFixPlotMaximumValue "1" 
     .SetInverseAxialRatio "False" 
     .SetAxesType "user" 
     .SetAntennaType "unknown" 
     .Phistart "1.000000e+00", "0.000000e+00", "0.000000e+00" 
     .Thetastart "0.000000e+00", "0.000000e+00", "1.000000e+00" 
     .PolarizationVector "0.000000e+00", "1.000000e+00", "0.000000e+00" 
     .SetCoordinateSystemType "spherical" 
     .SetAutomaticCoordinateSystem "True" 
     .SetPolarizationType "Linear" 
     .SlantAngle 0.000000e+00 
     .Origin "bbox" 
     .Userorigin "0.000000e+00", "0.000000e+00", "0.000000e+00" 
     .SetUserDecouplingPlane "False" 
     .UseDecouplingPlane "False" 
     .DecouplingPlaneAxis "X" 
     .DecouplingPlanePosition "0.000000e+00" 
     .LossyGround "False" 
     .GroundEpsilon "1" 
     .GroundKappa "0" 
     .EnablePhaseCenterCalculation "False" 
     .SetPhaseCenterAngularLimit "3.000000e+01" 
     .SetPhaseCenterComponent "boresight" 
     .SetPhaseCenterPlane "both" 
     .ShowPhaseCenter "True" 
     .ClearCuts 
     .AddCut "lateral", "0", "1"  
     .AddCut "lateral", "90", "1"  
     .AddCut "polar", "90", "1"  

     .StoreSettings
End With

'@ activate local coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "local"

'@ move wcs

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.MoveWCS "local", "0.0", "0.0", "0.51"

'@ define extrude: component1:Truncut22

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "Truncut22" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "0.3", "-1.6" 
     .LineTo "1.6", "-0.3" 
     .LineTo "1.6", "-1.6" 
     .LineTo "0.3", "-1.6" 
     .Create 
End With

'@ transform: mirror component1:Truncut22

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:Truncut22" 
     .Origin "Free" 
     .Center "0", "0", "0" 
     .PlaneNormal "0", "-0.5", "0" 
     .MultipleObjects "True" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Destination "" 
     .Material "" 
     .Transform "Shape", "Mirror" 
End With

'@ transform: mirror component1:Truncut22_1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:Truncut22_1" 
     .Origin "Free" 
     .Center "0", "0", "0" 
     .PlaneNormal "-0.5", "0", "0" 
     .MultipleObjects "False" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Transform "Shape", "Mirror" 
End With

'@ boolean subtract shapes: component1:Patch, component1:Truncut22

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:Truncut22"

'@ boolean subtract shapes: component1:Patch, component1:Truncut22_1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:Truncut22_1"

'@ define brick: component1:CUTTT

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Brick
     .Reset 
     .Name "CUTTT" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Xrange "-0.25", "0.25" 
     .Yrange "-0.25", "0.25" 
     .Zrange "0", "0.05" 
     .Create
End With

'@ transform: translate component1:CUTTT

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:CUTTT" 
     .Vector "-1.35", "-1.35", "0" 
     .UsePickedPoints "False" 
     .InvertPickedPoints "False" 
     .MultipleObjects "True" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Destination "" 
     .Material "" 
     .Transform "Shape", "Translate" 
End With

'@ transform: translate component1:CUTTT

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Transform 
     .Reset 
     .Name "component1:CUTTT" 
     .Vector "1.35", "1.35", "0" 
     .UsePickedPoints "False" 
     .InvertPickedPoints "False" 
     .MultipleObjects "False" 
     .GroupObjects "False" 
     .Repetitions "1" 
     .MultipleSelection "False" 
     .Transform "Shape", "Translate" 
End With

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "1.1", "1.6" 
     .LineTo "1.6", "1.1" 
     .LineTo "1.6", "1.6" 
     .LineTo "1.1", "1.6" 
     .Create 
End With

'@ delete shape: component1:CUTTT

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Delete "component1:CUTTT"

'@ boolean subtract shapes: component1:Patch, component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:solid1"

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "-1.1", "-1.6" 
     .LineTo "-1.6", "-1.1" 
     .LineTo "-1.6", "-1.6" 
     .LineTo "-1.1", "-1.6" 
     .Create 
End With

'@ delete shape: component1:CUTTT_1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Delete "component1:CUTTT_1"

'@ boolean subtract shapes: component1:Patch, component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:solid1"

'@ define monitor: e-field (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "28" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: h-field (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=28)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "28" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=28)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=28)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "28" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ activate global coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "global"

'@ define monitor: e-field (f=26)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=26)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "26" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: h-field (f=26)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=26)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "26" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=26)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=26)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "26" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ define monitor: e-field (f=26.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=26.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "26.2" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: h-field (f=26.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=26.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "26.2" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=26.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=26.2)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "26.2" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ define monitor: surface-current (f=26.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "surface-current (f=26.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Surfacecurrent" 
     .MonitorValue "26.2" 
     .Create 
End With

'@ farfield plot options

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With FarfieldPlot 
     .Plottype "Polar" 
     .Vary "angle1" 
     .Theta "90" 
     .Phi "90" 
     .Step "1" 
     .Step2 "1" 
     .SetLockSteps "True" 
     .SetPlotRangeOnly "False" 
     .SetThetaStart "0" 
     .SetThetaEnd "180" 
     .SetPhiStart "0" 
     .SetPhiEnd "360" 
     .SetTheta360 "False" 
     .SymmetricRange "False" 
     .SetTimeDomainFF "False" 
     .SetFrequency "-1" 
     .SetTime "0" 
     .SetColorByValue "True" 
     .DrawStepLines "False" 
     .DrawIsoLongitudeLatitudeLines "False" 
     .ShowStructure "True" 
     .ShowStructureProfile "True" 
     .SetStructureTransparent "False" 
     .SetFarfieldTransparent "True" 
     .AspectRatio "Free" 
     .ShowGridlines "True" 
     .SetSpecials "enablepolarextralines" 
     .SetPlotMode "Directivity" 
     .Distance "1" 
     .UseFarfieldApproximation "True" 
     .IncludeUnitCellSidewalls "True" 
     .SetScaleLinear "False" 
     .SetLogRange "40" 
     .SetLogNorm "0" 
     .DBUnit "0" 
     .SetMaxReferenceMode "abs" 
     .EnableFixPlotMaximum "False" 
     .SetFixPlotMaximumValue "1" 
     .SetInverseAxialRatio "False" 
     .SetAxesType "user" 
     .SetAntennaType "unknown" 
     .Phistart "1.000000e+00", "0.000000e+00", "0.000000e+00" 
     .Thetastart "0.000000e+00", "0.000000e+00", "1.000000e+00" 
     .PolarizationVector "0.000000e+00", "1.000000e+00", "0.000000e+00" 
     .SetCoordinateSystemType "spherical" 
     .SetAutomaticCoordinateSystem "True" 
     .SetPolarizationType "Linear" 
     .SlantAngle 0.000000e+00 
     .Origin "bbox" 
     .Userorigin "0.000000e+00", "0.000000e+00", "0.000000e+00" 
     .SetUserDecouplingPlane "False" 
     .UseDecouplingPlane "False" 
     .DecouplingPlaneAxis "X" 
     .DecouplingPlanePosition "0.000000e+00" 
     .LossyGround "False" 
     .GroundEpsilon "1" 
     .GroundKappa "0" 
     .EnablePhaseCenterCalculation "False" 
     .SetPhaseCenterAngularLimit "3.000000e+01" 
     .SetPhaseCenterComponent "boresight" 
     .SetPhaseCenterPlane "both" 
     .ShowPhaseCenter "True" 
     .ClearCuts 
     .AddCut "lateral", "0", "1"  
     .AddCut "lateral", "90", "1"  
     .AddCut "polar", "90", "1"  

     .StoreSettings
End With

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "-1.2", "0" 
     .LineTo "-0", "1.2" 
     .LineTo "1", "1.2" 
     .LineTo "1.4", "0.8" 
     .LineTo "1.4", "-0.2" 
     .LineTo "0.2", "-1.4" 
     .LineTo "-0.8", "-1.4" 
     .LineTo "-1.2", "-1" 
     .LineTo "-1.2", "0" 
     .Create 
End With

'@ activate local coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "local"

'@ delete shape: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Delete "component1:solid1"

'@ define extrude: component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Extrude 
     .Reset 
     .Name "solid1" 
     .Component "component1" 
     .Material "Copper (annealed)" 
     .Mode "Pointlist" 
     .Height "0.05" 
     .Twist "0.0" 
     .Taper "0.0" 
     .Origin "0.0", "0.0", "0.0" 
     .Uvector "1.0", "0.0", "0.0" 
     .Vvector "0.0", "1.0", "0.0" 
     .Point "-1.4", "0.2" 
     .LineTo "-0.2", "1.4" 
     .LineTo "1", "1.4" 
     .LineTo "1.4", "1" 
     .LineTo "1.4", "-0.2" 
     .LineTo "0.2", "-1.4" 
     .LineTo "-1", "-1.4" 
     .LineTo "-1.4", "-1" 
     .LineTo "-1.4", "0.2" 
     .Create 
End With

'@ boolean subtract shapes: component1:Patch, component1:solid1

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solid.Subtract "component1:Patch", "component1:solid1"

'@ define frequency range

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solver.FrequencyRange "10", "50"

'@ activate global coordinates

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
WCS.ActivateWCS "global"

'@ define monitor: e-field (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "43.2" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: h-field (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "43.2" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=43.2)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "43.2" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ define fieldsource monitor: field-source (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "field-source (f=43.2)" 
     .Domain "Frequency" 
     .FieldType "Fieldsource" 
     .Samples "1" 
     .MonitorValueRange "43.2", "43.2" 
     .InvertOrientation "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .Create 
End With

'@ define monitor: surface-current (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "surface-current (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Surfacecurrent" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define monitor: power (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "power (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Powerflow" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define monitor: current-density (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "current-density (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Current" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define monitor: loss (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "loss (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Powerloss" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define monitor: e-energy (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-energy (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Eenergy" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define monitor: h-energy (f=43.2)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-energy (f=43.2)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Henergy" 
     .MonitorValue "43.2" 
     .Create 
End With

'@ define frequency range

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Solver.FrequencyRange "40", "45"

'@ define monitor: e-field (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-field (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Efield" 
     .MonitorValue "43.5" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define monitor: h-field (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-field (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Hfield" 
     .MonitorValue "43.5" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "0.0", "0.0", "0.0", "0.0", "0.0", "0.0" 
     .SetSubvolumeInflateWithOffset "False" 
     .Create 
End With

'@ define farfield monitor: farfield (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "farfield (f=43.5)" 
     .Domain "Frequency" 
     .FieldType "Farfield" 
     .MonitorValue "43.5" 
     .ExportFarfieldSource "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .EnableNearfieldCalculation "True" 
     .Create 
End With

'@ define fieldsource monitor: field-source (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "field-source (f=43.5)" 
     .Domain "Frequency" 
     .FieldType "Fieldsource" 
     .Samples "1" 
     .MonitorValueRange "43.5", "43.5" 
     .InvertOrientation "False" 
     .UseSubvolume "False" 
     .Coordinates "Structure" 
     .SetSubvolume "-6", "6", "-6", "6", "-0.5", "0.56" 
     .SetSubvolumeOffset "10", "10", "10", "10", "10", "10" 
     .SetSubvolumeInflateWithOffset "False" 
     .SetSubvolumeOffsetType "FractionOfWavelength" 
     .Create 
End With

'@ define monitor: surface-current (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "surface-current (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Surfacecurrent" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ define monitor: power (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "power (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Powerflow" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ define monitor: current-density (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "current-density (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Current" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ define monitor: loss (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "loss (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Powerloss" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ define monitor: e-energy (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "e-energy (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Eenergy" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ define monitor: h-energy (f=43.5)

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With Monitor 
     .Reset 
     .Name "h-energy (f=43.5)" 
     .Dimension "Volume" 
     .Domain "Frequency" 
     .FieldType "Henergy" 
     .MonitorValue "43.5" 
     .Create 
End With

'@ farfield plot options

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With FarfieldPlot 
     .Plottype "Polar" 
     .Vary "angle1" 
     .Theta "90" 
     .Phi "90" 
     .Step "1" 
     .Step2 "1" 
     .SetLockSteps "True" 
     .SetPlotRangeOnly "False" 
     .SetThetaStart "0" 
     .SetThetaEnd "180" 
     .SetPhiStart "0" 
     .SetPhiEnd "360" 
     .SetTheta360 "False" 
     .SymmetricRange "False" 
     .SetTimeDomainFF "False" 
     .SetFrequency "-1" 
     .SetTime "0" 
     .SetColorByValue "True" 
     .DrawStepLines "False" 
     .DrawIsoLongitudeLatitudeLines "False" 
     .ShowStructure "True" 
     .ShowStructureProfile "True" 
     .SetStructureTransparent "False" 
     .SetFarfieldTransparent "True" 
     .AspectRatio "Free" 
     .ShowGridlines "True" 
     .SetSpecials "enablepolarextralines" 
     .SetPlotMode "Directivity" 
     .Distance "1" 
     .UseFarfieldApproximation "True" 
     .IncludeUnitCellSidewalls "True" 
     .SetScaleLinear "False" 
     .SetLogRange "40" 
     .SetLogNorm "0" 
     .DBUnit "0" 
     .SetMaxReferenceMode "abs" 
     .EnableFixPlotMaximum "False" 
     .SetFixPlotMaximumValue "1" 
     .SetInverseAxialRatio "False" 
     .SetAxesType "user" 
     .SetAntennaType "unknown" 
     .Phistart "1.000000e+00", "0.000000e+00", "0.000000e+00" 
     .Thetastart "0.000000e+00", "0.000000e+00", "1.000000e+00" 
     .PolarizationVector "0.000000e+00", "1.000000e+00", "0.000000e+00" 
     .SetCoordinateSystemType "spherical" 
     .SetAutomaticCoordinateSystem "True" 
     .SetPolarizationType "Linear" 
     .SlantAngle 0.000000e+00 
     .Origin "bbox" 
     .Userorigin "0.000000e+00", "0.000000e+00", "0.000000e+00" 
     .SetUserDecouplingPlane "False" 
     .UseDecouplingPlane "False" 
     .DecouplingPlaneAxis "X" 
     .DecouplingPlanePosition "0.000000e+00" 
     .LossyGround "False" 
     .GroundEpsilon "1" 
     .GroundKappa "0" 
     .EnablePhaseCenterCalculation "False" 
     .SetPhaseCenterAngularLimit "3.000000e+01" 
     .SetPhaseCenterComponent "boresight" 
     .SetPhaseCenterPlane "both" 
     .ShowPhaseCenter "True" 
     .ClearCuts 
     .AddCut "lateral", "0", "1"  
     .AddCut "lateral", "90", "1"  
     .AddCut "polar", "90", "1"  

     .StoreSettings
End With

'@ delete monitors

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
Monitor.Delete "current-density (f=43.2)" 
Monitor.Delete "e-energy (f=43.2)" 
Monitor.Delete "e-field (f=26)" 
Monitor.Delete "e-field (f=26.2)" 
Monitor.Delete "e-field (f=28)" 
Monitor.Delete "e-field (f=43.2)" 
Monitor.Delete "farfield (f=26)" 
Monitor.Delete "farfield (f=26.2)" 
Monitor.Delete "farfield (f=28)" 
Monitor.Delete "farfield (f=43.2)" 
Monitor.Delete "field-source (f=43.2)" 
Monitor.Delete "h-energy (f=28)" 
Monitor.Delete "h-energy (f=43.2)" 
Monitor.Delete "h-field (f=26)" 
Monitor.Delete "h-field (f=26.2)" 
Monitor.Delete "h-field (f=28)" 
Monitor.Delete "h-field (f=43.2)" 
Monitor.Delete "loss (f=43.2)" 
Monitor.Delete "power (f=28)" 
Monitor.Delete "power (f=43.2)" 
Monitor.Delete "surface-current (f=26.2)" 
Monitor.Delete "surface-current (f=28)" 
Monitor.Delete "surface-current (f=43.2)"

'@ farfield plot options

'[VERSION]2021.1|30.0.1|20201110[/VERSION]
With FarfieldPlot 
     .Plottype "Polar" 
     .Vary "angle1" 
     .Theta "90" 
     .Phi "90" 
     .Step "1" 
     .Step2 "1" 
     .SetLockSteps "True" 
     .SetPlotRangeOnly "False" 
     .SetThetaStart "0" 
     .SetThetaEnd "180" 
     .SetPhiStart "0" 
     .SetPhiEnd "360" 
     .SetTheta360 "False" 
     .SymmetricRange "False" 
     .SetTimeDomainFF "False" 
     .SetFrequency "-1" 
     .SetTime "0" 
     .SetColorByValue "True" 
     .DrawStepLines "False" 
     .DrawIsoLongitudeLatitudeLines "False" 
     .ShowStructure "True" 
     .ShowStructureProfile "True" 
     .SetStructureTransparent "False" 
     .SetFarfieldTransparent "True" 
     .AspectRatio "Free" 
     .ShowGridlines "True" 
     .SetSpecials "enablepolarextralines" 
     .SetPlotMode "Directivity" 
     .Distance "1" 
     .UseFarfieldApproximation "True" 
     .IncludeUnitCellSidewalls "True" 
     .SetScaleLinear "False" 
     .SetLogRange "40" 
     .SetLogNorm "0" 
     .DBUnit "0" 
     .SetMaxReferenceMode "abs" 
     .EnableFixPlotMaximum "False" 
     .SetFixPlotMaximumValue "1" 
     .SetInverseAxialRatio "False" 
     .SetAxesType "user" 
     .SetAntennaType "unknown" 
     .Phistart "1.000000e+00", "0.000000e+00", "0.000000e+00" 
     .Thetastart "0.000000e+00", "0.000000e+00", "1.000000e+00" 
     .PolarizationVector "0.000000e+00", "1.000000e+00", "0.000000e+00" 
     .SetCoordinateSystemType "spherical" 
     .SetAutomaticCoordinateSystem "True" 
     .SetPolarizationType "Linear" 
     .SlantAngle 0.000000e+00 
     .Origin "bbox" 
     .Userorigin "0.000000e+00", "0.000000e+00", "0.000000e+00" 
     .SetUserDecouplingPlane "False" 
     .UseDecouplingPlane "False" 
     .DecouplingPlaneAxis "X" 
     .DecouplingPlanePosition "0.000000e+00" 
     .LossyGround "False" 
     .GroundEpsilon "1" 
     .GroundKappa "0" 
     .EnablePhaseCenterCalculation "False" 
     .SetPhaseCenterAngularLimit "3.000000e+01" 
     .SetPhaseCenterComponent "boresight" 
     .SetPhaseCenterPlane "both" 
     .ShowPhaseCenter "True" 
     .ClearCuts 
     .AddCut "lateral", "0", "1"  
     .AddCut "lateral", "90", "1"  
     .AddCut "polar", "90", "1"  

     .StoreSettings
End With

