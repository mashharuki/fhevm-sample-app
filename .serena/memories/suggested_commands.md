# Suggested commands

- `npm run compile` (sets TS_NODE_TRANSPILE_ONLY; postcompile runs typechain)
- `npm test` = `hardhat test` (mock FHEVM; Sepolia test file self-skips off-Sepolia)
- `bun run test:sepolia` needs deployed contract + `.env` set
- `npm run coverage`, `npm run clean` (also regenerates typechain)
- `npm run lint` = solhint + eslint + prettier:check; `npm run prettier:write` to fix formatting
- `npm run build:ts` = `tsc --project tsconfig.json` (type check; CI runs it)
- `npm run chain` (local node) then `npm run deploy:localhost`; `deploy:sepolia`, `verify:sepolia <addr>`
- Secrets: put in `.env`; fallback `bunx hardhat vars set <NAME>`
