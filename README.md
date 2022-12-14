# Analysis of a simple SIR model to predict the rate of infection of covid in Italy

In this analysis, I am going to use the SIR model proposed by Dr. Giuseppe Gaeta to verify the accuracy and see if the fit the model gives can be further optimized using a bifurcation analysis around the β parameter.

I started this project by using the SIR model based on the following ODEs:

dS/dt = −α*S*I

dI/dt = α*S*I − β*I

dR/dt = β*I

Where S represents the indivituals susceptible to infection at a given time, I is the number of individuals infected at a given time, and R represents the individuals removed from the epidemic dynamics (i.e. they are either recovered, dead, or isolated). For the α and β parameters and the initial conditions (S0,I0,R0) I used the same values that were estimated in the paper. 

To design the model, I used the forward euler method to estimate solutions to the above ODEs. I took S0 to be the total population in Italy of 6x10^7. The solutions are plotted below for S(t), I(t), and R(t) respectively:

![image](https://user-images.githubusercontent.com/112734081/206884953-af6b9bfd-7c72-4e84-9a82-57ce7f993c3c.png)

![image](https://user-images.githubusercontent.com/112734081/206884959-997cfbae-bac2-48ea-b673-a0cc230bef3f.png)

![image](https://user-images.githubusercontent.com/112734081/206884970-33b44710-4411-4fe8-96d8-2bcc3a0e5b0e.png)

The main focus of the section of the paper that I am analyzing was on the number of cumulative infected individuals based on the total population of Italy (S0). I want to make sure my model conforms to the model used in the paper as they calculated solutions to the ODEs by hand. The solid black line in the top right image below represents the prediction of number of infected indivituals over time they achieved from their model:

![image](https://user-images.githubusercontent.com/112734081/206885122-88c51a01-fef5-4079-ba23-309c86c25532.png)

The model of infected individuals over time is the red plot above. It can be seen that my model is an accurate depiction of their model, so I can look further into fitting this model to the data gathered and seeing if I get a similar fit. The fit they obtained from their model is also shown above in the bottom row. To try and match the fit I downloaded their data in the form of a csv and plotted it against the fit to the plot of R(t). The initial fit is shown below:

![image](https://user-images.githubusercontent.com/112734081/206946209-ca9908f6-1b1d-4957-a932-743256e48a9e.png)

Athough, in this fit the data does not started at optimized value of R(0) calculated within the paper. I do not believe the paper leaves enough information on how exactly they got the plot to fit starting from the point (0,0). In order to get a more accurate fit, I created a seperate CSV file that starts at the March 5th data point which about matches the optimized R(0) value. This plot is shown below:

![image](https://user-images.githubusercontent.com/112734081/206946553-f768204a-e23e-4c96-9fff-519edd6ddb4d.png)

I was able to get a better fit in the early stages of the model, although the farther you extend the range of the model, the more the fit falls off. After day 15 the fit seems to no longer be accurate as can be seen below.

![image](https://user-images.githubusercontent.com/112734081/206947187-38ae9ffa-9404-4f20-a5ad-d4e4584d59d7.png)

This is mentioned in the paper that the fit is only accurate until roughly March 15th as the first set of restrictive measures against covid (masks, isolation) take place on March 8th and take about a week to effect the data. The SIR model itself is limited to only showing us what should be expected in terms of transmission of Covid if no restrictive measures occur.

The β parameter seems to be the main parameter of interest in the paper as it corresponds to the removal rate of individuals who are self isolating. When looking at the overall cumulative number of infected (R), we see that it only depends on I and β. We can conduct a bifurcation analysis on this parameter to see how a change in β effects the steady state of R. 

![image](https://user-images.githubusercontent.com/112734081/207209794-2f60559e-030c-4f27-8f9c-3722a14b316c.png)

Here, I have tested three values of β (-1,0,1) and plotted the corresponding output of dR/dt. As we can see, there lies a steady state at (0,0) which is stable for a negaitve value of β and unstable for a positive value. We can also observe that the value of β cannot be 0. Although in reality, the R value is going to depend on the change in I when solving for this system of differential equations. Based on the plot of R at the beginning of the page, we are also going to approach steady state at R = 4x10^7.

The output of the model corresponds to the two parameters α and β which describe the contact rate and the removal rate. A prompt isolation of infected individuals is reflected in raising β, a reduction of social contacts is reflected in lowering α. To look more specifically at the sensitvity of each parameter, I have raised each parameter by 1% from the intial value. The result is plotted below.

![image](https://user-images.githubusercontent.com/112734081/207211902-26c01560-c486-4a6a-94a0-6a4c3437c430.png)

I then took the percent change in the output to the ode solution and divided it by the percent change in the parameter to calculate the sensitity of R(t).

![image](https://user-images.githubusercontent.com/112734081/207212288-aab1247d-a0ab-4185-854a-6d284cd1b366.png)

We can see that increasing both parameters is going to effect the output in opposite ways. Ideally, to end the epidemic as fast as possible, you are going to want to raise β and reduce α as much as possible. This will raise the epidemic threshold γ. If this threshold is raised above the level of the total population N, the epidemic will stop.


[Works Cited]

Gaeta, Giuseppe. “A Simple SIR Model with a Large Set of 	Asymptomatic Infectives.” Mathematics in Engineering, vol. 3, 	no. 2, 2021, pp. 1–39., https://doi.org/10.3934/mine.2021013. 


