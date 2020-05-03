# Analyzing-US-Economic-Data-and-Building-a-Dashboard

# -*- coding: utf-8 -*-
"""
Created on Sun May  3 01:38:28 2020

@author: 31685
"""



import pandas as pd

from bokeh.io import push_notebook, output_file,show, output_notebook

from bokeh.layouts import row

from bokeh.plotting import figure


#In this section, we define the function make_dashboard. You don't have to know how the function works, you should only care about the inputs. 
#The function will produce a dashboard as well as an html file. You can then use this html file to share your dashboard. 
#If you do not know what an html file is don't worry everything you need to know will be provided in the lab.
def make_dashboard(x, gdp_change, unemployment, title, file_name):
    output_file(file_name)
    output_notebook()
    p = figure(title=title, x_axis_label='year', y_axis_label='%')
    p.line(x.squeeze(), gdp_change.squeeze(), color="firebrick", line_width=4, legend="% GDP change")
    p.line(x.squeeze(), unemployment.squeeze(), line_width=4, legend="% unemployed")
    show(p)
    
    
#The dictionary links contain the CSV files with all the data. 
#The value for the key GDP is the file that contains the GDP data.
#The value for the key unemployment contains the unemployment data.   
links={'GDP':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_gdp.csv',\
       'unemployment':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_unemployment.csv'}

    
csv_path=links['GDP'] #GDP CSV dosyasini aldik.
df_gdp=pd.read_csv(csv_path) #dosyayi okuduk 
x = pd.DataFrame(df_gdp, columns=['date']) # yeni bir dataframe yarattik date sutununun oldugu 
#print(df_gdp.head())
#print(x.head())



csv_path=links['unemployment'] #unemployment CSV dosyasini aldik.
df_ue=pd.read_csv(csv_path)       #dosyayi okuduk 
#print(df_ue.head())


df1=df_ue[df_ue['unemployment']>8.5] #unemployment dosyasinda 
#print(df1)


gdp_change = pd.DataFrame(df_gdp, columns=['change-current'])
print(gdp_change.head())


unemployment = pd.DataFrame(df_ue, columns=['unemployment'])
print(unemployment.head())


#Give your dashboard a string title, and assign it to the variable title
#title = "Unemployement stats according to GDP"


title = "Unemployement stats according to GDP"


#Finally, the function make_dashboard will output an .html in your direictory, 
#just like a csv file. The name of the file is "index.html" and it will be stored in the varable file_name.

file_name = "index.html"


#Call the function make_dashboard , to produce a dashboard. 
#Assign the parameter values accordingly take a the , 
#take a screen shot of the dashboard and submit it.

make_dashboard(x=x, gdp_change=gdp_change, unemployment=unemployment, title=title, file_name=file_name) 
