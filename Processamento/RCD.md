# Robust Cascade Decimation

## Steps:

> File

  > Tools
  
   > cascade decimation, robust processing 
    
   > Select the folder where the files will be save
   * click in `new`
   
   > **Parameters file widard**
   + Parameter file (*rcd): (Name it!)
   - Time series type: depends on the equipament. Emi, Metronix
   - insert the number of sites process.
   - insert the number of frequency band.
          
   > **Parameters file widard - Time series 1** 
   
   - Weighting Type: depends on! I choose Rho variance in the processing
   - Robust Processing: Enable the sites 
   - Threshold when to exit robust: 0.0
   - Maximun % of data to discard: 35.0
   - Robust Maximization type: Local E - Local H if you don't have remote station
   
   > **Parameters file widard - Time series 2**
   - Select the band -> Add file 
   Band | ts
   -----|---
   1 | TS4
   2| TS3
   3| TS2
   4| TS1
