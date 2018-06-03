# CrudeOill

import pandas as pd 
import matplotlib.pyplot as plt
from quantopian.research.experimental import history
from quantopian.research.experimental import continuous_future

#-------------------------------------------------------------------------------------------
# Here i just collected data from corn and oil based on the bloomberg word document i sent  
# I also added gasoline ( RBOB ) just to have another factor in there

Corn = continuous_future( 'CN' , roll = 'volume')  #Corn Futures  

Corn = history(     
    Corn, 
    fields='price', 
    frequency='daily', 
    start='2017-06-01', 
    end='2017-08-31'
)

WTI = continuous_future( 'CL', roll = 'volume' ) #Crude Oil Futures 

WTI = history(
    WTI, 
    fields='price', 
    frequency='daily', 
    start='2017-06-01', 
    end='2017-08-31'
)

rbob = continuous_future( 'XB' , roll = 'volume')  #Gasoline Futures  

rbob = history(     
    rbob, 
    fields='price', 
    frequency='daily', 
    start='2017-06-01', 
    end='2017-08-31'
)

#-------------------------------------------------------------------------------------------------------
# We just got the percent changes to normalize the prices

Corn = Corn.pct_change()*100    

WTI = WTI.pct_change()*100

rbob = rbob.pct_change()*100

#-------------------------------------------------------------------------------------------------------
# Plot the data just to see were we can "zoom in" to get specific dates 

plt.plot(Corn)
plt.plot(WTI)
#plt.plot(rbob)
plt.ylabel('Price')
plt.legend(['Corn', 'WTI','rbob']);

#---------------------------------------------------------------------------------------------------------
#Get corrilations of corn, oil and rbob

WTI.corr(Corn)  #There 20% correlated

rbob.corr(Corn)

WTI.corr(rbob)  

#-----------------------------------------------------------------------------------------------------
#I relized that august 2017 is a good time period to start. So i "zoom in there" 

CornAugust = continuous_future( 'CN' , roll = 'volume')  #Corn Futures  

CornAugust = history(     
    CornAugust, 
    fields='price', 
    frequency='daily', 
    start='2017-08-01', 
    end='2017-08-17'
)

WTI_August = continuous_future( 'CL', roll = 'volume' ) #Crude Oil Futures 

WTI_August = history(
    WTI_August, 
    fields='price', 
    frequency='daily', 
    start='2017-08-01', 
    end='2017-08-17'
)

#---------------------------------------------------------------------------------------------------------

CornAugust = CornAugust.pct_change()  #We just got the percent changes to normalize the prices 

WTI_August = WTI_August.pct_change()

plt.plot(CornAugust)
plt.plot(WTI_August)
plt.ylabel('Price')
plt.legend(['Corn','WTI']);
