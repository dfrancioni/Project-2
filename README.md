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

The main focus of the paper was on the number of infected individuals. I want to make sure my model conforms to the model used in the paper as they calculated solutions to the ODEs by hand. The solid black line in the top right image below represents the prediction of number of infected indivituals over time they achieved from their model:

![image](https://user-images.githubusercontent.com/112734081/206885122-88c51a01-fef5-4079-ba23-309c86c25532.png)

It can be seen that my model is an accurate depiction of their model, so I can look further into fitting this model to the data gathered and seeing if I get a similar fit.
