# renovate-config

The shared [Renovate](https://docs.renovatebot.com/) preset for every Chorus product repository. Each repository's
`renovate.json` extends it and adds only its own rules:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>chorus-run/renovate-config"]
}
```

`github>chorus-run/renovate-config` resolves to `default.json` on this repository's default branch
([shareable config presets](https://docs.renovatebot.com/config-presets/)). It is public because the repositories
that extend it sit under several GitHub accounts, and the Mend Renovate app can read a private preset only from
within the same account ([private presets](https://docs.renovatebot.com/getting-started/private-packages/)).

What it sets, all from Renovate's built-in presets:

- `config:recommended`: Renovate's recommended base, with the Dependency Dashboard issue.
- `schedule:weekly`: update PRs open early on Mondays, `America/Toronto` time
  ([schedule presets](https://docs.renovatebot.com/presets-schedule/)).
- `group:allNonMajor`: one PR for every minor and patch update; each major update gets its own PR.
- `:maintainLockFilesWeekly`: a weekly lockfile refresh.
- `minimumReleaseAge` 3 days, at most 5 open PRs, never automerged: every PR waits for the owner's review.
- Security updates skip the schedule and the release-age wait.

Check a change with Renovate's validator before pushing:

```sh
npx --package renovate -- renovate-config-validator --strict default.json
```
