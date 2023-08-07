---
title: "README.md"
author: "Gabe Cowley"
date: "2023-06-21"
output: html_document
---

Our functions squishGrype and squishTrivy have a twofold function.
Firstly, it takes each image and tallies up the number of times a particular vulnerability shows up, giving the tally and deleting the other instances to compress or "squish" the file. This is with respect to each individual image.
Secondly, it compiles all of the Grype image tallies on one document and all of the Trivy image tallies on another.

The output file should have the columns in the order of "Image Name", "Vulnerability ID", "Count", and "Severity".

For images without any vulnerabilities, the image name is given, the vulnerabilityID is "NA", the count is "0", and the severity is "NA".