# Tech stack

- Node >=20, npm; Hardhat 2.x (not Hardhat 3) + hardhat-deploy, typechain (ethers-v6, out `types/`)
- Solidity compiler 0.8.27, evmVersion `cancun`, optimizer runs 800, bytecodeHash none (contract pragma `^0.8.24`)
- FHEVM: `@fhevm/solidity`, `@fhevm/hardhat-plugin`, `@fhevm/mock-utils`, `@zama-fhe/relayer-sdk`, `encrypted-types`
- Tests: Mocha + Chai (+ hardhat-chai-matchers), ethers v6; coverage via solidity-coverage (`.solcover.js`); gas via `REPORT_GAS=1`
- Lint/format: solhint (`--max-warnings 0`), eslint 9 flat config (`eslint.config.mjs`) + typescript-eslint, prettier 3 + prettier-plugin-solidity (slang parser)
- Prettier: width 120, trailing commas all, LF, `.sol` tabWidth 4, md proseWrap always
- Networks: `hardhat` (default, in-process mock FHEVM), `anvil` (localhost:8545), `sepolia`
