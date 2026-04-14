# Week 0: Jan 20, 2026
- Discrete-time signals, e.g.,
  - unit impulse $\delta[n]$
  - unit step $u[n]$
  - exponential signals $a^n$, $e^{j\omega n}$
- Discrete-time systems
  - Focus of ECE503 is on linear time-invariant (LTI) systems 
- Representations of systems:
  - Linear constant coefficient difference equations
  - Impulse response $h[n]$
- Other system properties: 
  - BIBO stability
  - Causal 
  - Memoryless
- Convolution
  - only useful for LTI systems (this is a consequence of the linearity and time invariance of the system)

# Week 1: Jan 27, 2026
- Eigenfunctions of DT-LTI systems: a key one is complex exponential functions
- Frequency response: $H(e^{j\omega})$
  - Frequency domain representation of signals and systems
- DTFT (Discrete Time Fourier Transform) and the inverse DTFT
  - Definition (requires potentially an infinite sum), or an integral for the inverse DTFT
  - Tables in your textbook
  - The DTFT must be periodic in \omega (this is a continuous real-valued variable) with period $2\pi$ 
  - Impulse response $\leftrightarrow$ frequency response
  - Linear constant coefficient difference equation (LCCDE) $\leftrightarrow$ frequency response
  - Simple filtering example
  - Convergence conditions for the DTFT: (i) FIR is sufficient, (ii) absolutely summable impulse response is sufficient, (iii) generalized to allow the frequency response to include Dirac \delta functions
- Matlab: `freqz` function to plot magnitude and phase of a system described by an impulse response or LCCDE
- An application of the DTFT for random signals: autocorrelation $\leftrightarrow$ PSD
- Review of some statistics/properties for random signals: variance, mean, covariance (?), autocorrelation, wide sense stationary

# Week 2: Feb 3, 2026
*Note: Only one student attended this meeting, so we skipped the reflections and just worked on problems. The reflections below are copied from the on-campus section.*
- $Z$-transforms (focus this week is on bilateral, not unilateral)
- Generalization of the DTFT and (converges for a wider class of signals/systems)
- Region of Convergence (ROC) is important to specify when working with bilateral $z$-transforms. The mapping between $x[n] <-> X(z)$ is not unique without the ROC
- Poles are values of $z$ that cause $|X(z)|$ to go to infinity
- Zeros are values of $z$ that cause $X(z)$ to go to zero
- Properties of the ROC
  - Concentric around the origin (disk, ring, or everything but a disk (“outer disk”), all centered)
  - ROC can be an empty set (uncommon)
  - ROC can’t contain any poles
  - Right sided sequence has an ROC that is an “outer disk” (extends from the largest pole to infinity)
  - Left sided sequence has an ROC that is a disk (extends inward from the smallest pole)
  - Two sided sequence has an ROC that is a ring
  - If (and only if) the ROC contains the unit circle, you can substitute $e^{j\omega} = z$ to get the DTFT
  - If (and only if) a system has a $z$-transform with an ROC that contains the unit circle, it is BIBO stable
- Inverse z transform (5 ways to do it)
- Matlab: `tf2zpk`, `roots`, `poly`, `zplane`

# Week 3: Feb 10, 2026
## More $z$-transforms
- Properties of the $z$-transform (highlights: up/down sampling, linearity, time shifting, convolution theorem)
- Convolution theorem (bilateral $z$-transform)
  - assumes the system is relaxed
  - the ROC of the output includes the intersection of the ROCs of the input and system
- Determining stability from the ROC
- Unilateral $z$-transform
  - no need to keep track of the ROC
  - can handle non-zero initial conditions
  - time shifting property is different than bilateral $z$-transform)
## Periodic sampling of continuous time signals
- Ideal sampling and reconstruction
- Understanding how ideal sampling and reconstruction works in the time domain and frequency domain
  - Sketching spectra at various points in the ideal sampling and reconstruction block diagram
  - Understanding the relationship between the CTFT $X(j\Omega)$ and DTFT $X(e^{j\omega}$.
- Aliasing (not always a bad thing)
- Ideal reconstruction via sinc interpolation
- Nyquist theorem (sample at at least twice the highest frequency of the input signal to avoid aliasing)

# Week 4: Feb 17, 2026
- Processing CT signals with DT systems (screencast 4.1)
  - How to design your DT system to emulate an LTI CT system
  - Sufficient conditions:
    - (i) the DT system must be LTI and
    - (ii) avoid aliasing (or at least make sure the DT system blocks the aliasing before it makes it to the output)
  - $\Omega = \omega/T$ where T is the sampling period (we learned this last week)
- Impulse invariance ($h[n] = h(nT)$) is a specific technique for emulating a CT system with a DT system (screencast 4.2)
  - Does not imply $H(e^{j\omega})$ = $H(j\Omega)$ (because of $2\pi$ periodicity in $\omega$ and potential aliasing effects when sampling the impulse response)
- Multirate signal processing: upsampling, downsampling, rational sample rate conversion (screencasts 4.3-4.6)
- Just started looking at computational complexity of DSP algorithms by counting multiplies
- Efficient (lower computation) structures for sample rate conversion and filtering (screencast 4.4)
- Polyphase filtering (screencast 4.5) and filter banks (screencast 4.6)
- Matlab: `impinvar`, `tf`, `impulse`, `step`, `downsample`, `upsample`, `upfirdn`, `resample`

# Week 5: Feb 24, 2026
- Practical issues in processing CT signals with DT systems
- Dealing with potential aliasing
  - anti-aliasing filters (requires a CT filter at the front end of the system)
  - key idea: do basic CT-AAF, oversample, do a much sharper DT-AAF, then downsample (cheaper, reconfigurable, ...)
  - another key idea: you can shape the spectrum of your DT-AAF to compensate/equalize any rolloff in your CT-AAF
- Quantizing
  - Propagation of the quantization noise to the output of your system (filters, down/up sampling, ...)
  - SNR calculations (assumes certain statistical properties about the noise)
  - Basic quantization $\Rightarrow$ SNR
  - Oversampled quantization (with filtering and downsampling) $\Rightarrow$ usually better SNR
  - Oversampled quantization with noise shaping (with filtering and downsampling) $\Rightarrow$ usually even better SNR
  - Same concepts that we learned for ADCs apply to DACs
  - Refer back to Screencast 1.6 for some background material that may be relevant
- Lots of oversampling

# Week 6: Mar 3, 2026
- Phase delay and group delay
- Linear phase systems (phase delay = group delay, both are constant over $\omega$)
- Inverse systems: $H(z) H_i(z) = \delta[n]$
  - Can I build a causal/stable inverse system $H_i(z)$? Depends on the locations of the poles and zeros of the system you are trying to invert.
  - Generalized inverse: $H(z) H_i(z) = \delta[n-n_0]$
  - Minimum phase systems: all zeros are inside the unit circle
  - Inverse systems inside multirate blocks
- Intuition: connecting $z$-plane pole/zero plots to magnitude response and phase response (and being able to quickly identify the type of filter from the pole/zero plots, e.g., LPF, HPF, bandstop, ...)
- Inferring $H(z)$ from $|H(e^{j\omega})|^2$
  - non-uniqueness of $H(z)$
  - requiring stable+causal: must pick poles from inside the unit circle (poles become unique)
  - zeros are not unique: need additional criteria, e.g., we could require $H(z)$ to be a minimum phase system to make the zero unique
- Matlab: `phasedelay`, `grpdelay`, `zplane`, `freqz`, `roots`, `poly` (seen before)

# Week 7: Mar 17, 2026
- All-pass systems
  - Only affect the phase of the signal at the input (magnitude is constant)
  - First order all-pass filter $H(z) = \frac{1 - a^* z}{1-az^{-1}}$ (IIR filter)
  - Cascaded APFs -> higher order APF
- Minimum phase systems
  - Definition: LTI, causal, stable, and has a causal stable inverse
    - poles inside the unit circle (consequence of causality and stability)
    - zeros inside the unit circle (since inverse must be stable)
    - minimum group delay, minimum energy delay, minimum phase delay (properties that follow from the definition)
  - Any causal stable $H(z)$ can be decomposed into a causal stable $H_{min}(z)$ and a causal stable $H_{ap}(z)$.
  - Application: for any causal stable $H(z)$, we can invert the minimum phase part, i.e., $G(z) = (H_{min}(z))^{-1}$, and then $H(z)G(z) = H_{ap}(z)$. In general, we can equalize the magnitude response by inverting the minimum phase system, but some phase distortion will remain (which we can correct with more all pass filters as shown in Screencast 7-2).
- Linear phase and generalized linear phase FIR filters
  - Type I, II, III, IV FIR filters (not an exhaustive catalog of GLP filters)
- Matlab: `isallpass` and `iirgrpdelay`

# Week 8: Mar 24, 2026
- Skipped (most of the discussion was about the project)

# Week 9: Mar 31, 2026
- Finite-precision effects on filtering
- Coefficient quantization
  - Fixed-point representations of real numbers
  - Analysis of the effect on FIR filters (9.2) and IIR filters (9.3)
  - Causes the poles and zeros of your filter to move (might even make your filter unstable if one or more poles move outside the unit circle)
  - For IIR filters, the most common realization structure is Direct Form II in cascaded second order sections (DFII-SOS) due to its robustness to the effects of coefficient quantization
  - Play around with `filterDesigner` in Matlab
- Product roundoff error
  - This is a consequence of not being able to store the full precision of multiplications in a DSP algorithm
  - Product roundoff noise is modeled in the same way that we modeled quantization error when we were studying ADC (see material from Week 5)
  - We can use superposition to analyze the effect of each product roundoff noise as it appears at the output of the system
  - Typically, we prefer a realization structure with less product roundoff noise at the output

# Week 10: Apr 7, 2026
- Discrete time IIR filter design
  - Classical DSP problem - emulating analog filters with DSP
  - Can design DT filters by designing CT filters and doing all steps with pencil and paper (not iterative procedure, like FIR filters)
- Impulse invariance
  - The limitation of impulse invariance is that the frequency response can be distorted due to aliasing (usually not a problem for lowpass filters, could be a problem for bandpass filters, definitely a problem for highpass filters and bandstop filters)
- Bilinear transform (a better choice in most cases than impulse invariance)
  - Preserves minimum phase, allpass, cascaded forms, and DC gain
  - Especially useful for highpass filters and bandstop filters (filters that would result in aliasing if impulse invariance were used)
  - No aliasing due to the one to one mapping between $\Omega$ and $\omega$
  - In some ways, bilinear is easier to implement analytically since you can go directly from $H_c(s)$ to $H(z)$
- Frequency transformations $\rightarrow$ designing BPF, HPF, BSF using a "prototype" LPF
- Matlab: `impinvar`, `bilinear`

# Week 11: Apr 14, 2026
- Up until this week, the only frequency domain tool you have is the DTFT
  - DTFT: mapping from a discrete-time signal (finite length, infinite length, periodic, ...) to the $\omega$ axis (the normalized continuous frequency axis)
- Discrete Fourier Transform (DFT)
  - Mapping from a *finite-length* (length $N$) discrete-time signal to a *discrete* frequency axis $k=0,1,\dots,N-1$.
  - The DFT is a sampled version (*sampled on the $\omega$ axis*) of the DTFT. $\omega = 2\pi k/N$ for $k=0,1,\dots,N-1$.
  - Review: sampling in the time domain and doing a DTFT creates $H(e^{j\omega})$ which is periodic in the freuqency domain (period $2\pi$).
  - New concept: sampling in the frequency domain (DTFT $\rightarrow$ DFT) and then doing an IDFT creates a discrete-time signal that is periodic in the time domain (this can lead to ``time-domain aliasing'' as discussed in several practice problems)
  - Recall: convolution in the time domain $\Leftrightarrow$ multiplication in the frequency domain (DTFT)
  - The DFT doesn’t work this way. Multiplication of two DFT vectors is equivalent to *circular* convolution (not linear convolution, which is what we normally think of when we discuss convolution)
  - To use the DFT to compute a linear convolution, the common approach is to zero pad your finite length signals, take the DFT of each, multiply (element-wise), and then do the IDFT
  - In Matlab and other programming languages, we always use the FFT to compute the DFT (much faster, same result)
- Discrete Fourier Series (DFS)
  - only applies to infinite length periodic signals (period $N$)
  - Mapping from infinite length periodic discrete-time signals to a *discrete* frequency axis for all integer $k$
  - Close relationship between the DFT coefficients $X[k]$ and the DFS coefficients $\tilde{X}[k]$.
  - Can't use the DFS to do linear convolution (unless you do enough zero padding). Multiplying DFS coefficients is equivalent in the time domain to *periodic* convolution.
