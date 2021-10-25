## Export Checklist

- Prep tables for export that meeting statistical disclosure requirements
- Use [`dipr::dipr_use_export_doc`](https://bcgov.github.io/dipr/reference/dipr_use_export_doc.html) to generate a skeleton of an export document
- Populate the export document with relevant information about data source and processes


- Export data through OCWA portal
- Respond to output checker questions
- After the export is finalized, tag the code repository to flag an export. 
```bash
git tag -a [export-tag] -m "[export-tag]"
git push --tags
```
  The export tag name (`-a`) should match the name of the export in OCWA as closely as possible. The message (`-m`) can simply be the same as the export tag, or can include more information if required (similar to a commit message).

- Place exported data on LAN under appropriate folder
