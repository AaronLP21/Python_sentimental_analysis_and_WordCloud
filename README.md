# Python_sentimental_analysis_and_WordCloud
Sentimental analysis metrics are computed for a big text, also a WordCloud.

# -*- coding: utf-8 -*-
"""
Created on Fri Mar  5 22:47:02 2021

@author: Aaron
"""

import pandas as pd
from textblob import TextBlob
import seaborn as sns
import os
from wordcloud import WordCloud, STOPWORDS 
import matplotlib.pyplot as plt 

#VAMOS A REALIZAR UN ANALISIS DE SENTIMIENTOS DE UN TEXTO QUE CONTIENE REGISROS DE TEXTO
os.getcwd()
os.chdir('C:\\Users\\Aaron\\Desktop\\Boehringer\\Codes\\Python')
os.getcwd()
df=pd.read_excel('F1_2.xlsx')#si funciona
df.to_csv ("Test.csv",index = None,header=True)
df = pd.DataFrame(pd.read_csv("Test.csv"))
print(df.dtypes)
print(df.head(4))
df['Polaridad']=df['Comentarios'].apply(lambda x: TextBlob(x).sentiment.polarity)
print(df['Polaridad'].head(4))
df['Sub-Obj']=df['Comentarios'].apply(lambda x: TextBlob(x).sentiment.subjectivity)
print(df['Sub-Obj'].head(4))
df.head(5)
df.describe()
df.to_csv ("Test.csv",index = None,header=True)#LISTO; dataframe exportado
sns.distplot(df['Polaridad'])
sns.distplot(df['Sub-Obj'])


#AHORA VAMOS A CREAR LA NUBE DE PALBARAS:  
df = pd.read_csv("1F_3.csv", encoding ="latin-1") 
df=pd.DataFrame(df)
len(df)
comment_words = '' 
stopwords = set(STOPWORDS) 
  
print(stopwords.__class__)
print(stopwords)
# iterate through the csv file 
for val in range(19638): 
      
    # typecaste each val to string 
    val = str(df.values) 
  
    # split the value 
    tokens = val.split() 
      
    comment_words += " ".join(tokens)+" "
  
wordcloud = WordCloud(width = 800, height = 800, 
                background_color ='white', 
                stopwords = stopwords, 
                min_font_size = 10).generate(comment_words) 
  
# plot the WordCloud image                        
plt.figure(figsize = (8, 8), facecolor = None) 
plt.imshow(wordcloud) 
plt.axis("off") 
plt.tight_layout(pad = 0) 
  
plt.show()
