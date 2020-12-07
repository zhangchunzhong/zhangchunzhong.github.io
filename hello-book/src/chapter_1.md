# Chapter 1 Backup architectures

## Backup software requirement
- summary (best-to-have)
    - multiple storage support
        - file system
        - s3 storage
        - ftp 
        - http
        - ssh
- multiple agents support
    - oracle
    - mysql
- recovery from data corruption (data integration/safe)
- snapshot support
- concurrent client access
- encryption support (derived key)
- space efficiency (zip/dedupe)
- speed efficiency (diff data transfer only)
- ease to use / mgmt UI/CLI
- punch / delete / expiration support
- multiple devices/systems/agents support


## Technical points
- repo / access
    - local
    - s3 cloud
    - ftp
    - http
    - ssh
- file container
    - encryption
    - compression
    - extra meta info
        - file level
        - backup level
- file chunking
- index support
- flexible data layout
    - erasure code support
- encryption
    - symmetrical
    - key derived
- data recovery from corruption
    - erasure code support
- punch support
    - data compaction
    - lock free / concurrent client access

## The big questions
- big issue #1: what backup is for ?
    - prevent data lose
    - view history data
    - any others ?
- big issue #2: closed system
    - software NOT interop
    - data format is vendor locked
    - file backup is common, BUT
        - Each database has their own backup method
        - so it is too software/agent related, case by case?
        - not easy to extend
        - not too much value, nichole market
- big issue #3: what is the requirement ?
    - mobile support (from produce view)
        - but phone vendor has solution
            - Narrow down the requirement of backup software