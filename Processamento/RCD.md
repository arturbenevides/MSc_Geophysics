# Robust Cascade Decimation

## Steps:

1. File

2. Tools
  
3. cascade decimation, robust processing 
    
4. Select the folder where the files will be save
   * click in `new`
   
 5. **Parameters file widard**
   * Parameter file (*rcd): (Name it!)
   * Time series type: depends on the equipament. Emi, Metronix
   * insert the number of sites process.
   * insert the number of frequency band.
          
6. **Parameters file widard - Time series 1** 
   
   * Weighting Type: depends on! I choose Rho variance in the processing
   * Robust Processing: Enable the sites 
   * Threshold when to exit robust: 0.0
   * Maximun % of data to discard: 35.0
   * Robust Maximization type: Local E - Local H if you don't have remote station
   
7.  **Parameters file widard - Time series 2**
   * Select the band -> Add file 
   * Add file to set 1.
   

Band of frequency | time series 
---------|----------------------
1      | TS4
2      |  TS3
3      |  TS2
4      |  TS1

  - Sensor path: Choose the folder where are the informations about sensor for calibration.
  
8. **Parameters file widard - Time series 3**
  
  * Name the site and select `Finish`.
  
9. **Robust Cascade Decimation** 
  * Select parameter files (MT000.rcd) to include in Batch run field
  * Select `run` and it done!
  
  
