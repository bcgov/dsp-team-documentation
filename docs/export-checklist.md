## Export Checklist

- Prep tables for export that meeting statistical disclosure requirements
- Use [`dipr::dipr_use_export_doc`](https://bcgov.github.io/dipr/reference/dipr_use_export_doc.html) to generate a skeleton of an export document
- Populate the export document with relevant information about data source and processes
- Tag code repository to flag an export 
```bash
git tag -a [export-tag] -m "[export-tag]"
git push --tags
```
- Export data through OCWA portal
- Respond to output checker questions
- Place exported data on LAN under appropriate folder
