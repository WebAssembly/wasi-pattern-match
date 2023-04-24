# WASI Pattern Match APIs

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-pattern-match` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/42fe2a3ca159011b23099c3d10b5b1d9aff2140e/docs/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Andrew Brown](https://github.com/abrown)
- [Jianjun Zhu](https://github.com/jianjunz)
- [Johnnie Birch](https://github.com/jlb6740)
- [Mingqiu Sun](https://github.com/mingqiusun)

### Phase 4 Advancement Criteria

TODO before entering Phase 2.

## Table of Contents [if the explainer is longer than one printed page]

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Scan a block of data](#scan-a-block-of-data)
  - [Scan a stream](#scan-a-stream)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

`wasi-pattern-match` is a WASI API for scanning data and finding out matches with high performance and low latency.

### Goals

- Support PCRE syntax (or subset)
- API: iterate over matches, find the first match, check existence
- Improve upon current WebAssembly performance


### Non-goals

- Not all of the PCRE APIs are supported, e.g.: string replacement


### API walk-through

Initial draft. APIs are subject to change.


#### Scan a block of data

This example creates a scanner with a given pattern, then uses the scanner to scan a block of data to get the number of email addresses.

```
Scanner scanner = create_scanner(["email pattern"]);
Scan result = scan_block(scanner, buffer);
println!("Number of email addresses in the block: {}", all_matches(result).len());
close_scanner(scanner)
```

#### Scan a stream

This example creates a scanner with given patterns, then uses the scanner to scan a stream to detect dangerous traffic.

```
Scanner scanner = create_scanner(["dangerous url", "credit card", "phone number"]);
Stream stream = create_stream(scanner);
while (!eos) {
  // Keep reading chunks from a network level stream, or an application level stream.
  Scan result = scan_stream(stream, chunk);
  if (has_match(result)) {
    // Detected dangerous traffic, drop the connection or return an error code.
  } else {
    // Continue.
  }
}
close_stream(stream)
close_scanner(scanner)
```


### Detailed design discussion

[This section should mostly refer to the .wit.md file that specifies the API. This section is for any discussion of the choices made in the API which don't make sense to document in the spec file itself.]

#### [Tricky design choice #1]

[Talk through the tradeoffs in coming to the specific design point you want to make.]

```
// Illustrated with example code.
```

[This may be an open question, in which case you should link to any active discussion threads.]

#### [Tricky design choice 2]

[etc.]

### Considered alternatives

If a WASM runtime does not support this API, please consider to compile a regex framework to WebAssembly.


### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
