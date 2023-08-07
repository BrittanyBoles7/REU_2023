---
title: "README"
author: "Gabe Cowley"
date: "2023-06-21"
output: html_document
---

Our input is the two files of all the images, their respective vulnerabilityIDs, the counts, and the vulnerability severity.

Our function countComparison removes the respective image names and simply looks for overall how much each vulnerability shows up. This is the first point at which we are actually comparing Trivy and Grype's counts to each other. Now, the function countComparison_differences takes this output and removes all of the identical entries such that we are left exclusively with the differences to see where the detections differ.

Our function severityComparison looks for all those vulnerabilities that show up in both Trivy and Grype's output (i.e. filtering out those vulnerabilties that show up exclusively from one tool or the other), comparing them to see if they are actually the same. Trivy's classifications span "critical", "high", "medium", "low", and "unknown", while Grype had these in addition to "negligible". We saw that Trivy's "low" severity quite frequently corresponded to Grype's "low" and "negligible" (look at the python image, for example, where Grype had 66 low and 588 negligible while Trivy had 653 low vulnerabilities). So, in our severityComparison_differences, we removed those times that Trivy gave "low" while Grype gave "negligible" for the same image. Furthermore, we filtered out thek "unknown" classifications, which seemed to be given to more recently discovered vulnerabilities.

Please note that for images with no vulnerabilities, we've removed them entirely from the equation, so they don't show up in our output file.