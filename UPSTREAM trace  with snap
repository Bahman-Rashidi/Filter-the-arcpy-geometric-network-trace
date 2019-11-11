


import arceditor

import arcpy


import arcpy.mapping as mapping


arcpy.env.workspace = "C:\\data\\WEBGISCNN.sde"


# Script arguments
Trace_Task_Type = arcpy.GetParameterAsText(0)
if Trace_Task_Type == '#' or not Trace_Task_Type:
    Trace_Task_Type = "TRACE_UPSTREAM" # provide a default value if unspecified







spatial_reference = arcpy.SpatialReference('Projected Coordinate Systems/World/WGS 1984 Web Mercator (auxiliary sphere)')

Flags = arcpy.GetParameterAsText(1)
if Flags == '#' or not Flags:
    Flags = "new_point" # provide a default value if unspecified

Barriers = arcpy.GetParameterAsText(2)
if Barriers == '' or not Barriers:
    Barriers = "" # provide a default value if unspecified




Accumulation_Cost = Trace_Task_Type

motevaset="address  of  your line  layer  for snap"
snapEnv1 = [motevaset, "EDGE", "30 Feet"]
zaiif="address  of  your line  layer  for snap"
snapEnv2 = [zaiif, "EDGE", "10 Unknown"]
cable="address  of  your line  layer  for snap"
snapEnv3 = [cable, "EDGE", "10 Unknown"]
#SemnanDB.SDE.SP_MV_cable

pointflag = arcpy.AsShape(Flags,True)
# Process: Snap
arcpy.Snap_edit(pointflag, [snapEnv1,snapEnv2,snapEnv3])





Flag_Locations = pointflag



arcpy.AddMessage(" snap is done ")

try:


       gnVersionFDS_1 = "in_memory\\Storm_Net"
       SemnanDB_SDE_elec_Net = "address of  you  elec_Net"
       arcpy.TraceGeometricNetwork_management(SemnanDB_SDE_elec_Net, gnVersionFDS_1, Flag_Locations, Trace_Task_Type,"", "", "", "", "", "NO_TRACE_ENDS", "", "", "", "AS_IS", "", "", "", "AS_IS")
       
       network = arcpy.mapping.Layer(gnVersionFDS_1)	
       count=0
       for sublayer in network:
           count=count+1
          
       
       arcpy.AddMessage("count  layer  {} ".format(count))
       
       spal=None
       arcpy.AddMessage("  {} ".format("input In Script"))
       
       
       arcpy.AddMessage(" workspace is = " + arcpy.env.workspace)
       #FC = arcpy.CreateFeatureclass_management("in_memory",FeatureClass,"POLYLINE","","DISABLED","DISABLED",spatialRefCode)
       FC = arcpy.CreateFeatureclass_management("in_memory","Q443t","POINT","","DISABLED","DISABLED",spatial_reference)
       for FeatureClass in FC:
         arcpy.AddField_management(FeatureClass, "TableName", "TEXT", "", "", "80", "", "NULLABLE", "NON_REQUIRED", "")
         arcpy.AddField_management(FeatureClass, "Obj_ID", "TEXT", "", "", "80", "", "NULLABLE", "NON_REQUIRED", "")
         arcpy.AddField_management(FeatureClass, "GeoJson", "TEXT", "", "", "880", "", "NULLABLE", "NON_REQUIRED", "")
         arcpy.AddField_management(FeatureClass, "LayerId", "TEXT", "", "", "80", "", "NULLABLE", "NON_REQUIRED", "")
         arcpy.AddField_management(FeatureClass, "LayerName", "TEXT", "", "", "80", "", "NULLABLE", "NON_REQUIRED", "")
       


       arcpy.AddMessage(" Fc  has  been  created  and  filed  ah been  aded ")
       fields = arcpy.ListFields(FC)
       for field in fields:
           arcpy.AddMessage("{0} is a type of {1} with a length of {2}"
                 .format(field.name, field.type, field.length)) 
       
       
       arcpy.AddMessage(" goto  trace network ")
       numbeeLayerId=0   
       for sublayer in network:
          layername=sublayer.name
          ld=arcpy.Describe(sublayer)
          layeraliasname=ld.aliasname
          numbeeLayerId=numbeeLayerId+1;
          if arcpy.Describe(sublayer).shapeType=="Point":
            with arcpy.da.SearchCursor(sublayer,("OBJECTID","SHAPE@","SHAPE@JSON"),"",spatial_reference=spatial_reference)as cursora:
       	         with arcpy.da.InsertCursor(FC,("OID","Shape","TableName","Obj_ID","GeoJson","LayerId","LayerName")) as iCur:
       	             for row in cursora:
       		             iCur.insertRow((row[0],row[1],layername,row[0],row[2],numbeeLayerId,layeraliasname))
       
       
       arcpy.AddMessage("  {} ".format(" end FC"))
       
       Trace_Layer = 'in_memory'
       # Process: Make Feature Layer
       arcpy.MakeFeatureLayer_management(FC, Trace_Layer, "", "", "")
       arcpy.SetParameter(3,Trace_Layer) 
except arcpy.ExecuteError:
         arcpy.AddError(arcpy.GetMessages(2))
         arcpy.ClearWorkspaceCache_management()
finally:
         arcpy.ClearWorkspaceCache_management() 
