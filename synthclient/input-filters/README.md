# `synthclient` input filters

Because different vendors have proprietary conflicting extensions
(such as for indicating modified bases) to the common FASTA format,
`synthclient` cannot a priori know which extension syntax and grammar
to use.  This directory tree is intended to contain various
implementations of filters, all of which are expected to accept
proprietary formats and emit the format specified for `synthclient`.

In general, each subtree should contain a filter, along with test
files showing acceptable inputs and the resulting outputs.  These may
eventually be used in CI.

Vendors with specific needs are encouraged to contribute to this tree
if able, or to contact SecureDNA.  We would be happy to support your
particular input format.

## Structure

- `multivendor/`: Combined Eurofins/IDT input filter
