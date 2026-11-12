# Task completion checklist

Mirrors CI (`.github/workflows/main.yml`). Run in order:
1. `npm run prettier:write` (if formatting changed) then `npm run lint`
2. `npm run compile`
3. `npm run build:ts`
4. `npm test`
5. `npm run coverage` for contract changes

Then commit per `mem:conventions` (Conventional Commits, feature branch, explicit paths).
