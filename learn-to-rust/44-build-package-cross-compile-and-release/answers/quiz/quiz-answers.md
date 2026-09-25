# Quiz Answers: Module 44

## 1

The host performs the build. The target is the environment the artifact is intended to run on.

## 2

It prevents Cargo from changing the reviewed dependency resolution recorded in Cargo.lock during the release build.

## 3

No. Cross-compilation may also require a target linker, runtime, SDK, native libraries, C toolchain, headers, or other platform support.

## 4

It verifies the actual output you intend to package or publish rather than silently rebuilding a different configuration.

## 5

That the bytes you have match the bytes used to generate the published hash, assuming you obtained the expected hash through a trusted channel.

## 6

A trusted signing system can provide authenticity about who produced or approved the artifact, in addition to integrity.

## 7

Packaged binary metadata is generally recoverable by users or attackers and should be treated as public.

## 8

The newer version may have changed databases, files, schemas, or configuration in a way the old binary cannot read or safely operate on.

## 9

Publishing distributes the artifact to users. Verification should happen before that irreversible or high-impact step.

## 10

No. A release also involves verification, packaging, provenance, integrity/authenticity, communication, and rollback planning.
