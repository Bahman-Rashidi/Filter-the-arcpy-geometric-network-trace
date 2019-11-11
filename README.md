# Filter-the-arcpy-geometric-network-trace

1- copy your connection to  this folder  or  any location "arcpy.env.workspace = "C:\\data\\WEBGISCNN.sde"

2-add  script  to arcmap

3-add  4 parameter  
Trace_Task_Type = arcpy.GetParameterAsText(0)   string

Flags = arcpy.GetParameterAsText(1)  string

Barriers = arcpy.GetParameterAsText(2) string

Trace_Layer  as  Trace_Layer  (Out)

4- save  it

5- run script    

6-  set  Flags   ={"x": 5899051.380576774,"y": 4226652.968110627,"spatialReference": {"wkid": 102100}}

7- run 

8- share result  az a service..now  you can use this  servic
