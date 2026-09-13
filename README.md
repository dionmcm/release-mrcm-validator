Release MRCM Validator
======================

## Overview

MRCM refsets are part of International Releases since 20170731. The Release MRCM Validator offers services to make sure SNOMED releases are compliant with the MRCM rules published.

## Quick Start
Use Maven to build the executable stand-alone jar and run:
```bash
mvn clean package \
        -DskipTests \
        -Ddependency-check.skip=true && \
    java -Xmx4g \
        --add-opens java.base/java.lang=ALL-UNNAMED \
        -jar target/mrcm-validator-*-jar-with-dependencies.jar \
            {release_package_unzipped_root_dir} \
            {content_type} \
            {release_date} \
            {result_dir}
```

### Configuration options

* {release_package_unzipped_root_dir} is for the release package unzipped file root directory. eg: /Releases/SnomedCT_InternationalRF2_PRODUCTION_20170731T120000Z
* {content_type} is to state whether to use stated or inferred relationships for validation. eg: stated or inferred. To run both, use "stated,inferred"
* {release_date} is the effective date for the release file that is being validated.The format is yyyyMMdd eg:20170731
* {result_dir} is the directory where validation reports will be saved.

System properties:

* `mrcm.validator.index.directory` builds the Lucene index under the named
  directory instead of in RAM. A temporary subdirectory is created per run and
  deleted when the run ends. Unset, the index is held in memory as before. Use
  it when the heap cannot hold the index: the build peaks near 7.8 GB on an
  853 MB edition, and both content forms are indexed at once.

### Validation results
The following reports will be listed in {result_dir} folder.

* MrcmSummaryReport.txt
* MrcmValidationReportWithError.txt                 
* MrcmValidationReportWithWarning.txt 
* MRCMValidationPassed.txt                          
* MRCMValidationSkipped.txt
