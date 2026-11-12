# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Read https://ethskills.com/SKILL.md and follow it before writing Solidity or shipping anything onchain.

## Overview

Hardhat 2.x template (forked from `zama-ai/fhevm-hardhat-template`) for Solidity contracts that compute on encrypted data using Zama's FHEVM. The only contract is the example `contracts/FHECounter.sol` (an encrypted `euint32` counter). For FHE-specific questions use the `zama-fhevm` skill.

## Commands

```bash
npm run compile          # hardhat compile; postcompile regenerates typechain into ./types
npm test                 # hardhat test (in-process mock FHEVM)
npx hardhat test test/FHECounter.ts            # single file
npx hardhat test --grep "increment"            # single test by name
npm run test:sepolia     # FHECounterSepolia.ts; needs a prior `deploy:sepolia`
npm run coverage         # solidity-coverage + typechain
npm run lint             # solhint (0 warnings) + eslint + prettier --check
npm run prettier:write   # auto-format .sol/.ts/.md/.json/.yml
npm run build:ts         # tsc type-check (CI runs it)
npm run clean            # removes artifacts/cache/types/fhevmTemp, then regenerates typechain
npm run chain            # local node; then `npm run deploy:localhost`
```

CI (`.github/workflows/main.yml`) runs: `compile` → `build:ts` → `test` → `coverage` (plus `prettier:check` and `lint` on the full job). Match that order before finishing.

Config/secrets use Hardhat vars, never files: `npx hardhat vars set MNEMONIC | INFURA_API_KEY | ETHERSCAN_API_KEY`. Defaults are a public test mnemonic and a dummy key.

## Architecture

- **Two test modes, one `fhevm.isMock` switch.** `test/FHECounter.ts` runs only on the mock (`this.skip()` otherwise); `test/FHECounterSepolia.ts` runs only on a live network and reads the address via `deployments.get("FHECounter")`. Don't mix them.
- **Generated code.** `types/` (typechain, ethers-v6), `artifacts/`, `cache/`, `fhevmTemp/` are build output; tests import contract types from `../types`, so compile first after changing a contract.
- **Deploy and tasks.** `deploy/deploy.ts` is a hardhat-deploy script (`deployer` = named account 0, tag `FHECounter`). Custom tasks in `tasks/` (`task:address`, `task:increment`, `task:decrement`, `task:decrypt-count`, `accounts`) are registered by side-effect imports at the top of `hardhat.config.ts`; a new task file must be imported there.
- **Networks.** `hardhat` (default, chainId 31337, mock FHEVM), `anvil` (localhost:8545), `sepolia` (Infura, 11155111).
- **FHE contract pattern.** Contracts inherit `ZamaEthereumConfig`. Encrypted inputs arrive as `externalEuintXX` + `inputProof` and go through `FHE.fromExternal`. After every mutation of stored ciphertext, call `FHE.allowThis(handle)` and `FHE.allow(handle, msg.sender)`, otherwise the contract or user cannot reuse or decrypt it.
- **Compiler.** Solidity 0.8.27, `evmVersion: cancun`, optimizer 800 runs, `bytecodeHash: none`. Prettier formats `.sol` with the slang parser, tab width 4; everything else width 120.

## Project rules

Detailed rules live in `.claude/rules/` (code style, git workflow, testing, security, development, learning loop) and are loaded automatically. Points that are easy to miss:

- Existing tests are Mocha/Chai, not Vitest; the `vi.fn()` mention in `testing.md` doesn't apply here.
- Never push to `main`; use `feat/<ticket>-<desc>` branches and Conventional Commits; stage by explicit file path (parallel sessions share the worktree).
- Browser automation: prefer Chrome DevTools MCP.
