# Writing scientific papers in LaTex (Tips and Tricks)

## General


## Meta

### Highlight updates

```latex
\usepackage[dvipsnames]{xcolor} %required package
\newcommand{\update}[1]{{\color{YellowOrange} #1}} %usage \update{this is changed.}
```


## Math

Typesetting and defining symbols:
```latex
\usepackage{xifthen}
\newcommand{\prob}[1][]{%requires xifthen package%
\ifthenelse{\isempty{#1}}%
      {\ensuremath{P}}%
    {\ensuremath{P\left\(#1\right\)}}%
}
\newcommand{\vect}[1]{\boldsymbol{\mathrm{#1}}}
\newcommand{\mat}[1]{\boldsymbol{\mathrm{#1}}}
\newcommand{\MSE}{\mathrm{MSE}}
\newcommand{\tr}{\mathrm{tr}}
\newcommand{\moddef}{\mathrm{mod}}
\newcommand{\diag}{\mathrm{diag}}
\newcommand{\vecop}{\text{vec}}
\newcommand{\CP}{L}
\newcommand{\hddots}{\hdots}
\newcommand*{\inC}[1]{\in\mathbb{C}^{#1}}
\newcommand{\norm}[1]{\left\lVert#1\right\rVert}
\newcommand{\abs}[1]{\left\lvert#1\right\rvert}
\newcommand{\expt}[1]{\mathbb{E} \left\{#1\right\}}
\newcommand{\cn}[2]{\ensuremath{\sim\mathcal{C}\mathcal{N}\left(#1,#2\right)}}
```


## Glossaries

<details>
<summary>Example</summary>
<!--All you need is a blank line-->

```latex
%
% Add new acronyms in alphabetical order
% use small letters unless capitalization is required e.g., GPS is Global Positioning System (GPS)
% you can use Wikipedia to know if it is required or not.
%
\newacronym{aoa}{AOA}{angle-of-arrival}
\newacronym{aod}{AOD}{angle-of-departure}
\newacronym{ap}{AP}{access point}
\newacronym{ar}{AR}{augmented reality}
\newacronym{asic}{ASIC}{application specific integrated circuit}
\newacronym{awgn}{AWGN}{additive white Gaussian noise}
\newacronym{amp}{AMP}{approximate message passing}
\newacronym{bs}{BS}{base station}
\newacronym{ce}{CE}{channel estimation}
\newacronym{ced}{CED}{cumulative energy density}
\newacronym{cdf}{CDF}{cumulative distribution function}
\newacronym{ecdf}{eCDF}{empirical cumulative distribution function}
\newacronym{cpu}{CPU}{central-processing unit}
\newacronym{csi}{CSI}{channel state information}
\newacronym{csp}{CSP}{contact service point}
\newacronym{crlb}{CRLB}{Cram\'er-Rao lower bound}
\newacronym{cs}{CS}{compressed sensing}
\newacronym{crs}{CRS}{cell reference signal}
\newacronym{cqi}{CQI}{channel quality indicator}
\newacronym{dc}{DC}{direct current}
\newacronym{dl}{DL}{downlink}
\newacronym{dcc}{DCC}{dynamic cooperation clustering}
\newacronym{ul}{UL}{uplink}
\newacronym{dmimo}{D-MIMO}{distributed MIMO}
\newacronym{ecsp}{ECSP}{edge computing service point}
\newacronym{eirp}{EIRP}{equivalent isotropically radiated power}
\newacronym{em}{EM}{electromagnetic}
\newacronym{en}{EN}{energy neutral}
\newacronym{e2e}{E2E}{End-to-End}
\newacronym{epu}{EPU}{edge processing unit}
\newacronym{fa}{FA}{federation anchor}
\newacronym{fh}{FH}{fronthaul}
\newacronym{gnb}{gNB}{Next Generation Node B}
\newacronym{ic}{IC}{integrated circuit}
\newacronym{iot}{IoT}{Internet of Things}
\newacronym{fim}{FIM}{Fisher information matrix}
\newacronym{id}{ID}{information decoding}
\newacronym{kpi}{KPI}{key performance indicator}
\newacronym{lca}{LCA}{life cycle assessment}
\newacronym{lis}{LIS}{large intelligent surface}
\newacronym{liion}{Li-ion}{lithium-ion}
\newacronym{los}{LoS}{line-of-sight}
\newacronym{lp}{LP}{linear programming}
\newacronym{lpwan}{LPWAN}{low-power wide-area network}
\newacronym{lmo}{LMO}{lithium ion manganese oxide}
\newacronym{lrt}{LRT}{likelihood-ratio test}
\newacronym{lsfc}{LSFC}{large-scale fading component}
\newacronym{lmmse}{LMMSE}{least minimum mean square error}
\newacronym{mf}{MF}{matched filter}
\newacronym{mmse}{MMSE}{minimum mean square error}
\newacronym{mmwave}{mmWave}{millimeter wave}
\newacronym{mimo}{MIMO}{multiple-input multiple-output}
\newacronym{miso}{MISO}{multiple-input single-output}
\newacronym{mpc}{MPC}{multipath component}
\newacronym{mrc}{MRC}{maximum ratio combining}
\newacronym{mrt}{MRT}{maximum ratio transmission}
\newacronym{mse}{MSE}{mean square error}
\newacronym{ofdm}{OFDM}{orthogonal frequency-division multiplexing}
\newacronym{ota}{OTA}{over-the-air}
\newacronym{nb}{NB}{narrowband}
\newacronym{nr}{NR}{New Radio}
\newacronym{pa}{PA}{power amplifier}
\newacronym{pdp}{PDP}{power delay profile}
\newacronym{pdcch}{PDCCH}{physical downlink control channel}
\newacronym{pdsch}{PDSCH}{physical downlink shared channel}
\newacronym{per}{PER}{packet error rate}
\newacronym{pg}{PG}{path gain}
\newacronym{pl}{PL}{path loss}
\newacronym{pc}{PC}{pilot count}
\newacronym{re}{RE}{radio element}
\newacronym{rf}{RF}{radio frequency}
\newacronym{rfid}{RFID}{radio frequency identification}
\newacronym{ris}{RIS}{reflective intelligent surface}%reconfigurable?
\newacronym{rms}{RMS}{root-mean-square}
\newacronym{rss}{RSS}{received signal strength}
\newacronym{rssi}{RSSI}{received signal strength indicator}
\newacronym{rw}{RW}{RadioWeaves}
\newacronym{mmtc}{mMTC}{massive machine-typed communication}
\newacronym{rmse}{RMSE}{root-mean-square error}
\newacronym{sa}{SA}{synchronization anchor}
\newacronym{sdg}{SDG}{Sustainable Development Goal}
\newacronym{sdn}{SDN}{software-defined network}
\newacronym{sinr}{SINR}{signal-to-interference-plus-noise ratio}
\newacronym{siso}{SISO}{single-input single-output}
\newacronym{slam}{SLAM}{simultaneous localization and mapping}
\newacronym{snr}{SNR}{signal-to-noise ratio}
\newacronym{smc}{SMC}{specular multipath component}
\newacronym{svd}{SVD}{singular value decomposition}
\newacronym{ssb}{SSB}{synchronisation signal block}
%\newacronym{sppu}{SPPU}{service point processing unit}
%\newacronym{sp}{SP}{service point}
\newacronym{tdd}{TDD}{time division duplexing}
\newacronym{tdoa}{TDOA}{time-difference-of-arrival}
\newacronym{toa}{TOA}{time-of-arrival}
\newacronym{tx}{TX}{transmitter}
\newacronym{rx}{RX}{receiver}
\newacronym{ue}{UE}{user equipment}
\newacronym{uhf}{UHF}{ultra high frequency}
\newacronym{ula}{ULA}{uniform linear array}
\newacronym{upa}{UPA}{uniform planar array}
\newacronym{urllc}{URLLC}{Ultra-Reliable Low Latency Communications}
\newacronym{ura}{URA}{uniform rectangular array}
\newacronym{uv}{UV}{unmanned vehicle}
\newacronym{uwb}{UWB}{ultrawideband}
\newacronym{gsm}{GSM}{Global System for Mobile Communications}
\newacronym{wb}{WB}{wideband}
\newacronym{wpt}{WPT}{wireless power transfer}
\newacronym{zf}{ZF}{zero forcing}
\newacronym{mcs}{MCS}{modulation and coding scheme}
\newacronym{zmcscg}{ZMCSCG}{zero mean circularly symmetric complex Gaussian}
\newacronym{cfo}{CFO}{carrier frequency offset}
\newacronym{llh}{LLH}{log-likelihood}
\newacronym{lorawan}{LoRaWAN}{long-range wide-area network}
\newacronym{ls}{LS}{least squares}
\newacronym{iid}{i.i.d.}{independently and identically distributed}
\newacronym{sfn}{SFN}{single frequency network}
\newacronym{harq}{HARQ}{hybrid automatic repeat request}
\newacronym{ldpc}{LDPC}{low-density parity-check}
\newacronym{qos}{QoS}{quality-of-service}
\newacronym{gpu}{GPU}{graphics processing unit}
\newacronym{embb}{eMBB}{enhanced Mobile Broadband}
\newacronym{rreq}{RREQ}{route request packet}
\newacronym{ofdmim}{OFDM-IM}{OFDM with index modulation}
\newacronym{HyMPRo}{HyMPRo}{Hybrid Multi-Path Routing algorithm}
\newacronym{papr}{PAPR}{peak-to-average power ratio}
\newacronym{cp}{CP}{cyclic prefix}
\newacronym{gf}{GF}{grant-free}
\newacronym{gb}{GB}{grant-based}
\newacronym{noma}{NOMA}{non-orthogonal multiple access}
\newacronym{rbs}{RBS}{radio base station}
```
</details>


## Bibliography

- Clean-up your bib files: https://flamingtempura.github.io/bibtex-tidy/
- I also always enable the "Enclose values in double braces" option to keep the capitalization in titles.






## Figures

### Python to Tikz

tikzplotlib

### Extract data from existing figures

https://automeris.io/WebPlotDigitizer/

![](https://automeris.io/WebPlotDigitizer/images/wpd-scaled.png)

### Indicate lines in a plot

```latex
%draw arc
\draw (x0, y0) arc
    [
        start angle=50,
        end angle=310,
        x radius=0.1cm,
        y radius =0.6cm
    ] ;
    
%draw line 
\draw[] (x1, y1) -- (x2, y2);

%add text
\node[] (x3,  y3) {my text};
```

example: 

![My Image](figs/arc_example.PNG)
