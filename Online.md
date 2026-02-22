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



