# Hardware Diagnostic Support

This repository contains the integration for vendor hardware diagnostics.

The vendor diagnostics will be represented by a YAML file that will be
read by vyatta-diag-op from /opt/vyatta/hardware-diagnotics.  The probe
routine should exit with a value of 0 or 1 depending on whether the
diagnositcs are relevant to the current platform.

diagnostics is a dictionary of the available tests to run. Each test
should contain a run and optionally completions, prerun and postrun.
completions should be another dictionary of possible completions for a
given test with a set of arguments.  prerun and postrun can be used to
setup and teardown anything necessary for the run stage.

During the run stage, %args% will be replaced by the existing arguments
from the command line.


        name: [Vendor] hardware diagnostics module
        probe: probe-routine-for-this-module
        diagnostics:
                test1:
                        completions:
                        run: |
                                echo test1 %args%

                test2:
                        completions:
                                test2: a b
                                test2 a: c
                                test2 b: d
                        run: |
                                echo test2 %args%

A sample is included in hardware-diagnostics/demo-diagnostics.yaml
