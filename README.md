# QuSpinTesting
Code, manuals and results from testing the quspin sensor for use in the TUCAN nEDM experiment.

The goal is to have simultaneous readout of the Quspin sensor and the data from an oscilloscope measuring the output voltage of a function generator that is powering a small coil inside a magnetic shielding apparatus.

#Web Links
Information online relavent to the project
[QuSpin Sensor Supplier page](https://quspin.com/qtfm/)

## Qu Spin Relavent Information
- Internal DAC Sample rate: 1600Hz
- Decimation Rates: 2^n for n=2 to 11
- Max Sample Rate: 400 samples/s
  - dt = ~0.0025 seconds between sameples
- Minimum Sample Rate: 0.78125
  - dt = ~1.28 seconds between pulses
- Note: there is a difference between the QuSpin reported dt and the calculated dt above using the manual values.
- Dynamic Range: 1000 nT to 100000 nT
-The qu-spin has a buffer of unknown size that will store data until a read is requested


### Qu Spin Tests and Results
Short summaries of test results, folders can be made to add results
#### Buffer Testing
Performed By: T. Hepworth, M. McCrea, J. Martin, and A. Zahra

Date: 2022/07/26

##### Method:
- Data taking was controled through the python code at https://github.com/mmccrea/QuSpinTesting/blob/main/QTFM_DAQ_Code on 2022/07/26.
- Data taking was started by connecting to the serial port that communicates with the Qu-Spin sensor.
- Decimation rate was set to give roughly 0.62 to 1.25 seconds between data points so a human could evaluate the timing of the module.
- Various sleep() statements were used to pause data taking either after the communications was established, or after one or more  data points were taken.
- The readout rate from the system was observed as the returned values in the Spyder python terminal given the 1.25 second delay differences in the timing could be observed without using computer timing.

##### Results
- After a sleep time longer than the delay between taking new data points by the quspin it would be observed that the quspin when queried with a data read operation would rapidly return a number of data points equal to what would have been taken during the sleep() time.  
- This indicates the presence of a buffer in the ECU (electronic control unit) of the Qu-Spin that stored up to 20-40 data points from the delay without losing any measurment points.  We beleive no measurement points were lost as the counter that indicates the number of DAC cycles since the device was initialized showed a consistent increment whether the data points were read out immediately or after a delay.
- It appears to be a FIFO buffer returining the oldest data points first.

##### Future Tests
Run the QuSpin at a decimation rate that reads out the counter from the internal DAC and use that to determine what is the maximum number of samples that can be stored inside the Qu-spin (priority: low, no impact on anticipated data taking methods in the near future)
---
#### Orientation Testing

---
#### Buffer Testing

---
#### Long Term Stability

---
#### Square Wave Read-in

---
***Other Tests to be added***
