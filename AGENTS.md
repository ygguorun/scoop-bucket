# Repository Notes

## Scope
- This is a personal Scoop bucket. Active manifests live in `bucket/*.json`; `deprecated/` and `experience/` are outside the wrapper scripts' default checks.
- `README.md` is an index of manifests and deprecated entries, not a build or test source of truth.

## Commands
- Run commands from the repository root in PowerShell.
- Format active manifests: `& .\bin\formatjson.ps1` or one app with `& .\bin\formatjson.ps1 -App <name>`.
- Check versions: `& .\bin\checkver.ps1` or focused `& .\bin\checkver.ps1 -App <name>`; add `-Update` only when intentionally editing versions/hashes.
- Check URLs: `& .\bin\checkurls.ps1` or focused `& .\bin\checkurls.ps1 -App <name>`.
- Check hashes: `& .\bin\checkhashes.ps1` or focused `& .\bin\checkhashes.ps1 -App <name>`; add `-Update` only when intentionally rewriting hashes.
- Full Pester run: `& .\bin\test.ps1`; it requires PowerShell 5.1 plus `BuildHelpers` 2.0.1 and `Pester` 5.2.0.

## Tooling Details
- The `bin/*.ps1` wrappers resolve Scoop via `$env:SCOOP_HOME` or `scoop prefix scoop`, then call Scoop's own scripts with `-Dir .\bucket`.
- CI is `.github/workflows/schedule.yml`: a scheduled Windows Excavator job every 6 hours with `SKIP_UPDATED=1`; it also creates a Scoop `private_hosts` config for `https://cdn2.wodeabc.com/*` with a `Referer=https://www.wodeabc.com/` header.
- VS Code maps `bucket/**/*.json` to the upstream Scoop manifest schema.

## File Conventions
- Keep CRLF line endings: `.gitattributes` enforces `* text eol=crlf`, and `.editorconfig` sets `end_of_line = crlf`.
- Use 4-space indentation for JSON and PowerShell; YAML uses 2 spaces.
- Do not assume the wrapper scripts validate manifests outside `bucket/`; pass Scoop's underlying scripts a different `-Dir` only if you intentionally need to check `deprecated/` or `experience/`.
