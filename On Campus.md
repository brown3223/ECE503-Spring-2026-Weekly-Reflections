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
  - Frequency response of the DT system $H(e^{j\omega})$ is not identical to the frequency response of the CT system $H(j\Omega)$, even with $\Omega = \omega/T$, however.
    - Periodicity on $\omega$ axis (not on $\Omega$ axis prior to multiplication by pulse train)
    - Aliasing can also cause $H(e^{j\omega})$ to not be a close match to $H(j\Omega)$ between $-\pi$ and $\pi$
- Multirate (4.3 - 4.6)
  - Sample rate conversion (4.3): upsampling by an integer factor, downsampling by an integer factor, and rational sample rate conversion
  - Polyphase implementations of filters with downsampling/upsampling. Motivation: reducing computation (reducing multiplies)
  - Multirate filter banks (4.6)
- Matlab: `impinvar`, `tf`, `impulse`, `step`, `downsample`, `upsample`, `upfirdn`, `resample`

# Week 5 - class canceled

# Week 6: Mar 4, 2026
- Phase delay and group delay (both are units of samples)
- Linear phase systems have constant phase delay and constant group delay (all frequencies delayed by the same amount of time)
- Inverse systems: $H(z)H_i(z) = 1$
- Generalized inverse systems: $H(z)H_i(z) = z^{-n_0}$
- Inverse systems with oversampling (advanced topic, no practice problems, but could be useful)
- Minimum phase systems (all zeros inside the unit circle)
- Inferring magnitude and phase response from pole/zero plots
- How to determine poles and zeros of $H(z)$ from $|H(e^{j\omega})|^2$.
  - If we require $H(z)$ to be causal and stable, then the poles are uniquely determined
  - Cannot uniquely determine the zeros without the phase response or additional restrictions
  - If we require minimum phase, then the zeros are unique
- Matlab: `phasedelay`, `grpdelay`, `zplane`, `freqz`, `roots`, `poly`

# Week 7: Mar 18, 2026
- All-pass filter (only changes the phase, can also apply a constant scaling to the magnitude response, but the magnitude response is flat)
  - Useful for equalizing the group delay over a range of frequencies
  - First order all-pass filter $H(z) = \frac{1-a^* z}{1 - az^{-1}}$ with $|a|<1$ for stability.
- Minimum-phase systems
  - All the poles and zeros are inside the unit circle, LTI, causal, stable
  - Alternatively: LTI, causal, stable, and has a causal, stable inverse
  - To resolve ambiguities, we should also require $H(e^{j0}) > 0$ to achieve the minimum phase delay.
  - Minimum phase $\Rightarrow$ minimum group delay and minimum energy delay
- Minimum-phase all-pass decomposition $H(z) = H_{min}(z) H_{ap}(z)$.
  - Main utility of this is that we can invert $H_{min}(z)$, i.e., $G(z) = (H_{min}(z))^{-1}$. Then $H(z)G(z) = H_{ap}(z)$ and we can correct the residual phase distortion with an all-pass filter.
- Generalized linear phase systems
  - Type I, II, III, IV FIR filters with GLP (distinguished by symmetry vs. anti-symmetry and even vs. odd orders)
  - There are other ways to generate GLP filters beyond these four types (see page 325 of textbook for an IIR filter with group delay of 4.3 samples)
- Note: negative group delay does not necessarily imply a filter is non-causal (see example on page 316 of your textbook, and also see the paper uploaded to Canvas)
- Matlab: `isallpass`, `iirgrpdelay`

# Week 8: March 25, 2026
- Realizing discrete time systems and actually implementing them ("realization structures")
- Direct Form I
- Direct Form II (less memory than Direct Form I, same amount of computation though)
- Cascaded forms (Matlab filter designer calls these "second order sections")
- Parallel forms (not commonly used, not an option in Matlab filter designer)
- FIR lattice
- IIR all pole lattice
- Transposed forms (reverse all flows, pickoff points become sums, sums become pickoff points, swap input and output, redraw the whole thing with the input on the left and the output on the right)
- The main differences are: memory, computation
- Next week we will get into realization structure robustness to finite precision effects
- Matlab: `filterDesigner`, `tf2latc`, `latc2tf`

# Week 9: April 1, 2026
- Finite-precision effects in filtering
- Coefficient quantization
  - Floating-point representation of real numbers (easy)
  - Fixed-point representation of real numbers (harder, the focus this week)
    - Fractional bits
  - FIR filters (equalivalent parallel system, can bound errors)
  - IIR filters (more difficult to analyze, best done numerically in `filterDesigner`)
    - Poles can move outside the unit circle and make an IIR filter unstable
    - A good choice for a realization structure for IIR filters is usually cascaded DFII second order sections (this is what `filterDesigner` defaults to)
  - Why is the cascaded DFII-SOS realization structure so robust to coefficient quantization?
    - Localizes the quantization effects to pairs of poles and pairs of zeros rather than all poles/zeros
    - Reduces the dynamic range between the largest and smallest coefficients in each section
  - Coupled form (uniform distribution of achievable poles/zeros on the z-plane, more computation however)
- Product roundoff error
  - More amenable to analysis
  - Model the error as uniformly distributed, white noise with known variance (like we did for ADCs)
  - Use superposition
  - Determine the transfer function from the noise source to the output
  - Compute the PSD or autocorrelation function at the output, then total power
- In textbook (not covered in the screencasts)
  - Avoiding overflow
  - Fixed-point limit cycles
  - Appendix A gives some useful results for how to compute the integrals involved in noise power calculations

# Week 10: April 8, 2026
- Designing discrete time filters
- IIR vs. FIR
  - IIR: fewer coefficients (less computation) to achieve a desired response, useful for emulating filters we used to build with analog components, can be designed analytically with pencil and paper
  - FIR: always stable, generalized linear phase, good pipelining in most DSP hardware
- Focus this week was on IIR filters since we can design them analytically
- Steps to design a LPF:
  - Filter specification with passband and stopband frequencies on the DT frequuency axis $\omega$
  - Translate DT filter specification to a CT filter specifiation on the CT frequency axis $\Omega$
    - Impulse invariance $\Omega = \omega/T_d$ where $T_d$ is the sampling period
    - Bilinear transform $\Omega = \frac{2}{T_d}\tan (\omega/2)$
  - Design your CT filter (Butterworth, Cheby I/II, elliptical) $\rightarrow H_c(s)$
  - If using impulse invariance:
    - Inverse Laplace transform $H_c(s) \rightarrow h_c(t)$ to get impulse reponse
    - Sample the impulse response (with the same $T_d$ as before) to get $h[n] = h_c(nT_d)$
    - Finally, compute the $z$-transform $h[n] \rightarrow H(z)$
  - If using bilinear transform:
    - Take $H_c(s)$, substitute in $s=\frac{2}{T_d} \left( \frac{1-z^{-1}}{1+z^{-1}} \right)$ to get $H(z)$
- Why choose impulse invariance? Need to match an impulse response of something. Not used that often.
- Why choose bilinear transform?
  - Less steps
  - Preserves cascaded filters
  - Preserves minimum phase
  - Preserves DC gain
  - Does not suffer from aliasing, hence can be used for more than just LPF. Can be used for HPF, BPF (can usually also work with impulse invariance), and BSF
- Designing HPF, BPF, and BSF involves mapping band edge frequencies to a "prototype" LPF and the doing the design as above, and then mapping the LPF back to the HPF, BPF, or BSF
