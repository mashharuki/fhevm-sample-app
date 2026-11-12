# fhevm-sample-app core

Zama FHEVM Hardhat template (forked from zama-ai/fhevm-hardhat-template v0.4.1). Single package, no sub-modules. Example: encrypted `FHECounter`.

## Source map
- `contracts/` Solidity (FHECounter.sol; inherits `ZamaEthereumConfig`)
- `test/` Mocha/Chai TS: `FHECounter.ts` (mock FHEVM), `FHECounterSepolia.ts` (live Sepolia only)
- `deploy/deploy.ts` hardhat-deploy script; `tasks/` custom Hardhat tasks (registered via imports in `hardhat.config.ts`)
- `types/`, `artifacts/`, `cache/`, `fhevmTemp/` = generated, do not edit
- `.claude/rules/` project rules (code style, git, testing, security, Japanese learning-loop); `.agents/skills`, `skills-lock.json` = skills

## Invariants
- Solidity code: FHE ops via `@fhevm/solidity` `FHE` lib; always `FHE.allowThis` + `FHE.allow(handle, user)` after mutating an encrypted state value
- Secrets via `npx hardhat vars set MNEMONIC|INFURA_API_KEY|ETHERSCAN_API_KEY` (never in files)
- Local chainId 31337; Sepolia 11155111 via Infura
- Stack/versions: `mem:tech_stack`; commands: `mem:suggested_commands`; style: `mem:conventions`; done-checklist: `mem:task_completion`
- The Zama FHEVM skill (`zama-fhevm`) exists for FHE-specific guidance
