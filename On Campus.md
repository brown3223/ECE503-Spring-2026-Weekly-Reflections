# Week 0: Jan 21, 2026
- History of DSP
- Advantages and disadvantages of DSP compared to analog SP
- Basics of DSP - graphs and functions
- Discrete time signals, e.g.,
  - unit impulse $\delta[n]$
  - unit step $u[n]$
  - periodicity $x[n] = x[n-N]$
  - exponential (real $a^n$ and complex $e^{j\omega n}$)
- Discrete time systems and their properties:
  - memoryless
  - linearity
  - time-invariance
  - causality
  - stability
- Ways of representing LTI discrete-time systems (in the time domain):
  - Impulse response
  - Linear constant coefficient difference equations
- Convolution review (consequence of linearity and time invariance of a system)
- Tiny bit of Matlab in the final screencast
  - `conv` function
  - `filter` function
  - Use the Matlab symbolic toolbox to check your algebra/calculus!
  - Usually Matlab is useful for numerical simulation to test the theory (midterm project)
 
# Week 1: Jan 28, 2026
- Complex exponentials are eigenfunctions of DT-LTI systems
- DTFT - discrete time Fourier transform
- Transforms between discrete time (time domain) signals/systems and *continuous* frequency (frequency domain) representations 
- Impulse response $h[n] \leftrightarrow H(e^{j\omega})$ (for a given $\omega$, this is just a complex number, usually represented as magnitude and phase)
- Linear constant coefficient difference equation (LCCDE) $\leftrightarrow H(e^{j\omega})$
- $H(e^{j\omega})$ is periodic in $\omega$ with period $2\pi$
- Filtering of *random* signals (last screencast)
  - Application of the DTFT: autocorrelation $\leftrightarrow$ power spectral density
  - Application of the DTFT: filtering of random signals to shape the output power spectral density
- Matlab: `freqz`

# Week 2: Feb 4, 2026
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

# Week 3: Feb 11, 2026
## More $z$-transforms
- Properties of the $z$-transform (linearity, time shifting, upsampling, downsampling, convolution)
- Unilateral $z$-transform
  - allows for non-zero initial conditions
  - no need to specify the ROC (implies a right sided sequence)
  - Time-shifting property is not the same as bilateral
- Determining the BIBO stability of a system from the $z$-transform (ROC of $H(z)$ includes the unit circle)
## Ideal periodic sampling and reconstruction
- Conversion between continuous time and discrete time signals
- Should be able to understand and operate in the time domain and frequency domain when looking at ideal sampling and reconstruction systems
- Continuous time signals, we have the CTFT $X(j\Omega)$
- Relationship between CTFT and DTFT $\Omega = \omega/T$ 
- Aliasing (not always a bad thing) and spectral replication when sampling
- Reconstruction

# Week 4: Feb 18, 2026
- Processing analog signals with DT systems (4.1)
- Designing digital filters via the impulse invariance method (4.2)
  - this is one specific technique (we will learn more techniques later in this course)
  - Frequency response of the DT system ($H(e^{j\omega})$) is not identical to the frequency response of the CT system ($H(j\Omega)$), however.
    - Periodicity on $\omega$ axis (not on $\Omega$ axis prior to multiplication by pulse train)
    - Aliasing can also cause $H(e^{j\omega})$ to not be a close match to $H(j\Omega)$ between $-\pi$ and $\pi$
- Multirate (4.3 - 4.6)
  - Sample rate conversion (4.3): upsampling by an integer factor, downsampling by an integer factor, and rational sample rate conversion
  - Polyphase implementations of filters with downsampling/upsampling. Motivation: reducing computation (reducing multiplies)
  - Multirate filter banks (4.6)
- Matlab: `impinvar`, `tf`, `impulse`, `step`, `downsample`, `upsample`, `upfirdn`, `resample`




