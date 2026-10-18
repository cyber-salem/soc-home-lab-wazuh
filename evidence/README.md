# Evidence policy and pre-publication review

[← Project](../README.md) · [Screenshot gallery](GALLERY.md) · [Selection queue](REVIEW-QUEUE.md)

## Current state

- **39** curated screenshots in the original organized archive, plus **1** final saved-dashboard screenshot added afterward.
- **15** selected presentation screenshots have been cropped for readability and uploaded to `assets/screenshots/` in this **private** repository.
- The screenshots are real records of a controlled Wazuh/Windows home lab. No event values, rule IDs, SHA-256 strings or dashboard counts were fabricated or changed by the cropping process.
- The underlying unaltered source images remain in the separate original evidence archive; they are **not** uploaded.
- The five visualization editor images from the early archive remain **draft-stage evidence** and have not been substituted for the final dashboard image.

Open the [curated gallery](GALLERY.md) to review screenshots in their investigation context.

## Why only 15 screenshots?

Recruiters need to see the result and an example of analyst reasoning without scrolling through every configuration click. The main README links directly to the strongest examples. The source archive and review queue preserve additional context for deeper technical discussion.

## Public release checklist

- [x] Collect evidence from the controlled lab.
- [x] Select high-signal images for incident/event investigations, FIM, custom detection, and final dashboard.
- [x] Crop extraneous interface areas while preserving technical fields.
- [x] Upload the 15 presentation files to a **private** repository.
- [x] Link them from the README and the relevant technical case reports.
- [ ] **Final human inspection of each displayed image** at full resolution for names, account identifiers, paths, terminal histories, browser tabs and environment-specific details.
- [ ] Decide which VM hostnames and local IP/MAC details are acceptable to publish publicly.
- [ ] Confirm the public captions exactly match evidence and all selected images are legible on a mobile screen.
- [ ] Explicitly approve switching the repository to **Public**.

**No password or API token has been intentionally included in the presentation set, but cropping is not equivalent to complete sensitive-data redaction.** Do not use the private status as a substitute for the release checklist.

## Interpretation safeguards

- Windows Event `4625` demonstrates an authentication failure, not automatically brute force.
- PowerShell Event `4104` demonstrates logging of script-block text, not proof the script succeeded.
- File Integrity Monitoring rule `550` demonstrates a file integrity change, not which actor performed it.
- Rule `100100` applies to one protected file in the lab. The result does not establish a low false-positive rate for a production deployment.
- The saved dashboard reflects the filters and time range of one session; its numbers are not permanently fixed.
- Only the four documented cases and one custom detection are claimed as completed.

## Files and provenance

The companion export **SOC-Portfolio-Reviewed-Screenshots.zip** contains the presentation images and an asset manifest with each original filename, original SHA-256, processed SHA-256, crop coordinates and dimensions.

The source archive **SOC-Home-Lab-Evidence-Review-Pack-v2.zip** is retained as the full 40-image provenance collection.

[Review queue and outstanding work](REVIEW-QUEUE.md)
