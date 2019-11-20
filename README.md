#code for the multiple column summerisation of Attribute table in ArcGis.

import geopandas as pd #import the geopanda library 
import xlwt as wt # import library for working with Excel
files=['A','B','C','D'] # creates the list shapefile names, used for multiple layer summerisation
for i in files:
    dataa=pd.read_file('{}.shp'.format(i)) #reads the layer life
    #"Level","Remark","Area_Ha" columns area used for summerisation from attribute table of layer.
    dfsize = dataa[['Level','Remark','Area_Ha']].groupby(['Level','Remark'])['Level','Remark','Area_Ha'].size()
    #above line helps to re-arange the attribute table and gives the count of that table with selected column 
    dfsum = dataa[['Level','Remark','Area_Ha']].groupby(['Level','Remark'])['Level','Remark','Area_Ha'].sum()
    #above line helps to gives the area of that table with selected column and it arrange like"(on x-axis "level" column) and (on Y-axis "Remark" column) and last all the count and sum of "Area_Ha" will be arranged
    li=[]# creates the empty list
    for j in dfsize:    
        li.append(j)
    dfsum['Count']=li #creates the dataframe of above table from sum and count of selected column
    dfsum.to_excel('shanta\{}.xlsx'.format(i)) #Exports into the XLS file.
    print("Saved")


