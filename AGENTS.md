# Shimmer-MATLAB-ID

The Shimmer MATLAB Instrumentation Driver. **This repo spans two product families**, which is the
first thing to get straight:

| Location | Family | What it is |
|---|---|---|
| repo root | **Shimmer3 / 3R** | `ShimmerDeviceHandler.m`, `ComPortEventData.m`, the `*example.m` scripts, `Legacy/`, `quaternion/` |
| `VerisenseTools/` | **Verisense** | Verisense MATLAB examples, a file parser and a configure/sync console app |

## It is a wrapper, not an implementation

The root drives the Shimmer wire format through Java, not through MATLAB code:
`ShimmerBiophysicalProcessingLibrary_Rev_0_10.jar` is **closed source** and ships prebuilt. It
provides `PPGtoHRAlgorithm`, `ECGtoHRAdaptive`, and the deprecated `ECGtoHRAlgorithm` — prefer
`ECGtoHRAdaptive`, which is both more accurate and more efficient.

A parsing, protocol or calibration fix belongs in the Java API upstream; it reaches here for free.
Do not reimplement wire-format logic in MATLAB.

## `VerisenseTools/FileParser` is a vendored build, and it has drifted

`VerisenseFileParserPC.jar` plus `VerisenseFileParserPC_lib/` and a bundled JRE 1.8 is a **build of
`ASM_PC/VerisenseFileParser`**, not a second implementation. Nothing links the two.

It is stale: the changelog here stops at **2023-02-10** (parser 1.02.039) while
`ASM_PC/VerisenseFileParser` was last changed **2026-08-14**. Treat parsed output from this jar as
potentially behind the current parser, and re-vendor rather than patch the jar in place.

The Verisense MATLAB examples are **Pre-Alpha**. `VerisenseTools/datarecordingexample.m` is the
intended starting point.

## Older MATLAB versions need a Java class path override

The driver requires specific Apache Commons Math versions — `libs/commons-math-2.2.jar` and
`libs/commons-math3-3.6.jar`. MATLAB 2012 and 2014 bundle older ones and will load theirs instead,
so a `javaclasspath.txt` in the script's directory must point at the bundled jars. `Readmejavaclasspath.txt`
has the detail. A failure here looks like a maths or algorithm bug rather than a class path problem,
which is what makes it worth knowing.

## Note

No MATLAB is installed on the machine this was last worked from, so the code here is a read-only
reference in that context — changes cannot be run or tested locally.
