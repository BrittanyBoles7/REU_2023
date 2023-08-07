01b_DataAcquisition
    01_Input:
        Docker images but not really in a different directory
        TD: 
            Add docker images to correct directory
    02_protocol:
        Code for running all versions and all images of G and T
    03_incremental:
        Empty
    04_product:
        Output of G and T separated by each tool, each version, and each image in JSON format
        Note:
            There is some images that G or T couldn't do they are null put still in the outputs. 

02_PreProcessing
    02a_jsonTocvs
        01_input:
            Output of G and T separated by each tool, each version, and each image in JSON format
        02_protocol:
            Converting json to csv, removing extra columns, adding to known correlated vulnerabilities table. We use the vulnerabilities from the CVE file if one is present in the correlated vulnerabilities table
            TD:
            -are connected vulnerabilities universal?
            -add connected vulnerabilities for T
            -add separate function for connected vulnerabilities
        03_incremental:
            Table of correlated vulnerabilities. Columns are vulnerability, related vulnerability(CVE) and severity. If more than one related vulnerability corresponds to a vulnerably we list them all in separate rows.          
            TD:
            -add title descriptions and how severity was chosen and what the variable means. 
            -add T table
        04_product:
            Output from protocol, for each tool, each version, and each image with csv format. Images without vulnerabilities are filled in with NA values
    02b_squish
        01_input:
            Output from protocol, for each tool, each version, and each image with csv format. Images without vulnerabilities are filled in with NA values
        02_protocol:
            For each version, for each image, sum number of times each found vulnerability was identified. If severity of same vulnerability was different count it as different vulnerabilities. 
        03_incremental:
            nothing
        04_product:
            For each tool, for each version, one csv of all images, with columns as sum number of times each found vulnerability was identified, severity, type of error and image found in.
            Note:
                -Unknowns are typically newer vulnerabilities that we just don't know the danger level.
                -G and T don't always agree on severity for same vulnerabilities.
    02c_onlyCVEs:
        01_input:
             For each tool, for each version, one csv of all images, with columns as sum number of times each found vulnerability was identified, severity, type of error and image found in.
            Note:
                -Unknowns are typically newer vunerablities that we just don't know the danger level.
                -G and T don't always agree on severity for same vulnerabilities.
        02_protocol:
            For each tool, each version, if a main vulnerability has multiple related CVEs report all CVEs and use CVE severity ratings. Remove all none CVE vulnerabilities, note this doesn't include images that have no vulnerabilities (NA). 
            Also creates a list of CVE's we have run across. 
            Note: 
                G and T do this on the same project
        03_incremental:
            List of all CVE's we have run across
        04_product:
            For each tool, each version, a table with image name, vulnerablityID which now just has CVE's listed, severity, and sum of number of times each CVE shows up in each image. 
        02d_tables
            01_input:
                For each tool, each version, a table with image name, vulnerablityID which now just has CVE's listed, severity, and sum of number of times each CVE shows up in each image.
            02_product:
                Old Programs:
                    countComparison:
                        looking at count total of CVE's for G and T and putting them together by vulnerablityID. 
                        note: not updated for multiple versions of G and T
                        td.......
                onlydifference:
                    pick the version of G and T you want to compare. (one version comparison at a time)
            03_incremental
                nothing
            04_product:
                seems more one version at a time
                td....
    03_Analysis
        01_input:
            For each tool, each version, a table with image name, vulnerablityID which now just has CVE's listed, severity, and sum of number of times each CVE shows up in each image.
        02_protocol:
            intertool-line:
                plotting overall vuln count from version to version over time for G and T 
            trivyBarChart:
                plots T total vuln count in bar graph form
            twoTools_countDifferenceComparison:
                Looks at vuln with over 45 difference between any two tools(any version) you can compare version vs version or tool verse tool. 
            ImagecountVariation:
                Using both G and T (separate graphs) looking at images with standard deviations(from across versions) that are greater than X.
            ImageCount_ToolVersions_Onlychange:
                Every images, every images total vunerablity count over every version over time for G and T and difference of G and T using two month intervals and current version of each tool. ????????
                ????
            ImageCount_ToolVersions:
                Every images, every images total vulnerability count over every version over time for G and T and difference of G and T using two month intervals and current version of each tool. 
            GrypeBarChart_Stacked:
                bar chart of total count of vulns in each versions, blocked with severity. 
                Note:
                    currently doesn't run
            GrypeBarchart_Basic:
                Bar chart of total count of vulns in each version. 
            CVECounts_ToolsVersions(obselete):
                trying to be vuln counts tool versions but doesn't work
            CVECounts_ToolsVersions:
                Looking at certain vuln, their count in all images, across all versions over time. Each tool and their difference have their own graph. Note in the difference graph negative is when trivy have has more vulns.stacked bar chart with goal of looking at the CVE counts of all images that don't change across versions and do change.
Graph of vulnerabilities that have the greatest total count difference between any version. For G and T and difference of G and T 
                Note:
                    G tool page doesn't have all versions
            CVECounts_Comprehensive:
                Across all versions, summing up all vuln counts, choosing the top vulns and normalizing based on number of versions to compare G and T. Also looking at the normalized differences and choosing their top vulns. 
            bubbleViz:
                Looks at top problematic images and CVEs in G, T and their difference. If a vuln is found in a certain image, their a dot, the dots size is if present how often does it occur, and color is the frequency of versions that this error shows up in this image. 
        03_Incremental:
            Empty
        04_Product:
            Graphs from bubbleViz, CVECounts_toolVersions and imagecounts_toolversions



            
                









            










        

        
        
        






