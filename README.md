# Marine Heatwave Prediction
*ML workflow to predict marine heatwaves.* 

This project involves tracking extreme and prolonged warming events in sea surface known as marine heatwaves that have been observed throughout the world. Their effects have led to increased economic tensions between nations due to the closures of lucrative fisheries and changes in catch quotas. Knowing when and where marine heatwaves will occur will mitigate the impacts of these events by informing response decisions that protect living marine resources.


**Project Team:** Hillary Scannell<sup>:mortar_board:</sup>, Chris Fraley<sup>:globe_with_meridians:</sup>, Sarah Battersby<sup>:globe_with_meridians:</sup>, Kevin Binz<sup>:globe_with_meridians:</sup>, Nathan Mannheimer<sup>:globe_with_meridians::mortar_board:</sup>, Robert Kincaid<sup>:globe_with_meridians:</sup>

:mortar_board: *University of Washington*

:globe_with_meridians: *Tableau Software*


***

![Location of Initial time series](https://github.com/hscannell/MHWpredict/blob/master/data/datamap.png)

***
### Leader Board 
*Average score across all four time series (30n120w, 30n140w, 40n160w, & 50n140w) unless otherwise noted.

| Model | Description | Error |
|---|---|---|
| TBATS | Exponential smothing state space model with Box-Cox Transformation |  ? |
| AR | AutoRegressive order(6) |  MSE = 0.10 |
| ARMA | AutoRegressive Moving Average, order(6,2) | MSE = 0.13 |
| SARIMAX | Seasonal AutoRegressive Integrated Moving Average with eXogenous regressors, order(6,2,1)(6,2,1,4) | MSE = 0.13 |
| Persistence | "walk-forward" validation | MSE = 0.28 (1-day), 0.29 (3-day), 0.65 (9-day) |
|LSTM_1var | 5 neuron LSTM, 1 neuron Dense output layer, tanh activation, SGD optimizer, fit with 20 epochs, 520 batch size, forecasting 5-day sequence based on the previous 20 days, features are only SST | |
| LSTM_adjacent | LSTM trained on the SST from a neighboring grid cells | |
| LSTM_5var | 30 neuron LSTM, 1 neurton Dense output, tanh activation, SGD optimizer, 20 epochs, 800 batch_size, forecasting 21-day sequences based on the previous 100 days, features include SST, AirT, RH, WS, and SLP | |   
| LSTM_2var_PCA | features include SST and the first 2 PCs of SST, AirT, RH, WS and SLP | |
| XGB_1var_binary | Gradient Boosted Machines for event classification using SST alone to predict marine heatwave class, labels are binary (0=no event, 1=MHW), forecasts 30 days using the past 40, weights are given to circumvent class imbalance | 
| XGB_5var_binary | Gradient Boosted Machines for event classification using SST, AirT, RH, WS, and SLP to predict marine heatwave class, **labels are binary** (0=no event, 1=MHW), forecasts 30 days using the past 40, weights are given to circumvent class imbalance |  |
| XGB_1var_categ | Gradient Boosted Machines for event classification using SST alone to predict marine heatwave class, **labels are categorical** for MHWs only (0=no event, 1=moderate, 2=strong, 3=severe, 4=extreme), forecasts 30 days using the past 40 | |
| XGB_5var_categ | Gradient Boosted Machines for event classification using SST, AirT, RH, WS, and SLP to predict marine heatwave class, **labels are categorical** for MHWs only (0=no event, 1=moderate, 2=strong, 3=severe, 4=extreme), forecasts 30 days using the past 40 |  |
| XGB_1var_categ_mhw_mcw | Gradient Boosted Machines for event classification using SST alone to predict **both marine heatwave and coldwave** class, labels are categorical, positive for MHWs & negative for MCWs  (0=no event, 1=moderate, 2=strong, 3=severe, 4=extreme), forecasts 30 days using the past 40 | |
| XGB_5var_categ_mhw_mcw | Gradient Boosted Machines for event classification using SST, AirT, RH, WS, and SLP to predict **both marine heatwave and coldwave** class, labels are categorical, positive for MHWs & negative for MCWs (0=no event, 1=moderate, 2=strong, 3=severe, 4=extreme), forecasts 30 days using the past 40 |  |

***
Related Tutorials:
- https://machinelearningmastery.com/multivariate-time-series-forecasting-lstms-keras/
- https://machinelearningmastery.com/return-sequences-and-return-states-for-lstms-in-keras/
