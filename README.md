# Halo2 Combine Step Acceleration

Prize Sponsor: Mina Foundation

Prize Architect: Mina / O(1) Labs

## Prize Description

### Summary

The Bootleproof inner-product argument used in Halo-type SNARKs is one of the more costly operations for provers. This prize focuses on improving the performance of this operation in browser-based provers.

  

### Optimization Objective (1-sentence)

Competitors should provide, using the [arkworks library](https://github.com/arkworks-rs/) and its [curves implementations](https://github.com/arkworks-rs/curves/), a function

  

	fn combine(g1: &[ark_pallas::Affine], g2: &[ark_pallas::Affine], chal: &[bool]) -> Vec<ark_pallas::Affine>;

  

The semantics of this function should be as in [this gist](https://gist.github.com/imeckler/9cd2ec6bb7a6e77eedc838cf4933b7c7).

  

### Constraints

- Runtime must be WASM

- The MSM must be over the Pallas curve as described.

- Web workers may be used

  

NOTE: All submissions must include documentation (in English) sufficient to understand the approach being taken.

  
  
  

## Timeline

June 17 - Competition begins

July 25 - Mid-competition submission due

September 17 - Final submission due

## Judging

Submissions will be analyzed for both correctness and performance.

### Correctness

Submissions will be tested against the sample implementation described in the above gist.

### Performance

Random arrays g1 and g2 of size 2^16 and a random challenge of 128 bits will be selected to test the speed of the implementation. The score of the submission will be the average performance across 100 trials.

  

In addition, all submissions will be manually reviewed by the prize committee.

  

The fastest existing implementation is [here](https://github.com/o1-labs/proof-systems/blob/194b0748bc8a674f9453d11be8342e233e070752/poly-commitment/src/combine.rs#L288), which makes use of Pallas’s curve-endomorphism (x, y) -> (base_endo_coeff * x, y), where base_endo_coeff = 0x2D33357CB532458ED3552A23A8554E5005270D29D19FC7D27B7FD22F0201B547

  

It also makes use of multithreading and batched-affine operations.

  

The endomorphism-based scalar multiplication is defined in [section 6.2 of the Halo paper](https://eprint.iacr.org/2019/1021.pdf).

### Hardware & Benchmarks

Implementations will be compiled to WASM and benchmarked on a consumer-laptop with at least 8 cores in Google Chrome.

## Prize Allocation

The prize amount will be divided among the top two finishers according to the following proportions: 75% to winning implementation and 25% to second place.

## Notes

All submission code must be open-sourced at the time of submission. Code and documentation must be dual-licensed under both the MIT and Apache-2.0 licenses.

## Questions

If there are any questions about this prize, please contact Brett Carter at brett@o1labs.org
