# Wavelet-Boundary-Effect
A method for eliminating boundary effects from wavelet denoising to be used as a possible filter for trading.

Often times in financial literature wavelet transforms are used misleadingly for forecasting. The same is true for other decomposition methods like EMD and FFT. Wavelets and FFT, for instance, assume the signal is periodic for the given sample and that the signal starts and ends at 0. This is clearly false for financial time-series and methods like reflecting the boundary, zero padding, mean padding, etc do not reduce the severe deformities in boundary coefficients caused by these assumptions. Certain wavelet filters such as symlets and daubechies look ahead in the signal to produce coefficients at a given time t making the decomposition even more misleading. 

This works presents one method to eliminate boundary effects through a multistage process. First an end-point flattening function is contructed to "flatten" the signal on a given sample. This transforms the original signal such that the first and last values of the sample are zero, respecting the assumption of periodicity. A sliding window function is created to end point flatten the signal one-step at a time and perform wavelet denoising at each window (an 800 period window is used here). For each window, only the last two coefficients are saved then the window is slid one step ahead until the end is reached. The difference between these last two coefficients at each step is taken and then summed sequentially to produce a smoothed signal free of edge effects, however the new filter's values are not of the same magnitude of the original signal. From this, a possible filter based trading system may be constructed.
