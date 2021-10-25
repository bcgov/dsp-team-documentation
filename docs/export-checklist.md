[![img](https://img.shields.io/badge/Lifecycle-Maturing-007EC6)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)

## DIP Secure Environment Export Checklist

- [ ] Prep tables for export that meet Data Innovation Program statistical disclosure requirements
- [ ] Use [`dipr::dipr_use_export_doc`](https://bcgov.github.io/dipr/reference/dipr_use_export_doc.html) to generate a skeleton of an export document
- [ ] Populate the export document with relevant information about data sources, derived variables and analytic processes


- [ ] Export data through the OCWA (Output Checking Workflow App) portal _inside_ the secure environment
- [ ] Respond to output checker questions
- [ ] Access approved export files through the OCWA (Output Checking Workflow App) portal _outside_ the secure environment (still requires PopData VPN connection)
- [ ] Place exported data and documents on LAN under appropriate project folder
- [ ] After the export is finalized, tag the code repository git history to flag an export:

```bash
git tag -a [export-tag] -m "[export-tag]"
git push --tags
```
   * The export tag name (`-a`) should match the name of the export in OCWA as closely as possible
   * The message (`-m`) can simply be the same as the export tag, or can include more information if required (similar to a commit message)  


