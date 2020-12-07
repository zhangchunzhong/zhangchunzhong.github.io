## backup software in github
### https://github.com/restic/restic
- in golang
- https://restic.readthedocs.io/en/latest/100_references.html#design
    - git like repo
    - CDC, dedupe, encryption

### https://github.com/borgbackup/borg
- in c and python
- https://borgbackup.readthedocs.io/en/stable/internals.html
    - architecture
        - ![architecture](https://borgbackup.readthedocs.io/en/stable/_images/structure.png)
    - repo 
        - https://borgbackup.readthedocs.io/en/stable/internals/data-structures.html#repository
        - ![object-graph](https://borgbackup.readthedocs.io/en/stable/_images/object-graph.png)
    - compaction
        - todo
    - Encryption
        - ![Encryption](https://borgbackup.readthedocs.io/en/stable/_images/encryption.png)


### https://github.com/bup/bup
- python and c
- It uses a rolling checksum algorithm (similar to rsync) to split large files into chunks.
- Bup can use "par2" redundancy to recover corrupted backups even if your disk has undetected bad sectors.
    - https://blog.georgovassilis.com/2018/12/12/parchive-protecting-backups-against-data-corruption/
    - I think par2 is out (?), so have a look on erasure code.
        - https://github.com/darrenldl/reed-solomon-erasure
- bup stores its data in a git-formatted repository. 
    - https://shafiul.github.io/gitbook/7_the_packfile.html
    - git packs come in two parts: the pack itself (.pack) and the index (.idx).
    - when generating a remote backup, we don't have to have a copy of the packfiles from the remote server
        - the local end just downloads a copy of the server's index files,
        - and compares objects against those when generating the new pack, which it sends directly to the server.

### https://github.com/duplicati/duplicati
- c##
- security and dedupe

### https://github.com/gilbertchen/duplicacy
- in golang
- A lock-free deduplication cloud backup tool
    - cloud backup tool
    - chunk index file instead of chunk database
    - super fast
    - lock-free approach

| software  |   cdc  | chunk index  | cloud support| concurrent clients access|
|-----------|:-------------:|------:|------:|------:|
| duplicity |  rsync | none  | none |
| bup       |  librsync | none  | none|
| Duplicati | fix-sized chunk| none | yes| yes, but to different store|
| Attic     | CDC |indexing database| none |  exclusive locking, hard to extend|
| restic    | CDC |git pack|yes|exclusive locking, hard to extend|

### https://github.com/dpc/rdedup
- in rust
- https://github.com/dpc/rdedup/wiki/My-original-use-case-%28old-README.md%29
    - provide encryption, but only symmetrical
    - public key cryptography, secure passpharse is required only when restoring data, 
        - while adding and deduplicating new data does not.
    - libsodium's sealed boxes are used for encryption/decryption
    - private key is encrypted using libsodium crypto secretbox using random nonce, and key derived from passphrase using password hashing and random salt
### https://github.com/jborg/attic
- in python
- https://github.com/sourcefrog/conserve/wiki/Compared-to-others


### https://github.com/sourcefrog/conserve

### https://github.com/fpgaminer/preserve
    - https://github.com/fpgaminer/preserve
```
preserve keygen --keyfile keyfile
preserve create --keyfile keyfile --backend file --backend-path /path/to/my/backups/ my-backup-`date +%Y-%m-%d_%H-%M-%S` /home/me/
preserve list --keyfile keyfile --backend file --backend-path /path/to/my/backups/
preserve restore --keyfile keyfile --backend file --backend-path /path/to/my/backups/ name-of-backup-to-restore /path/to/restore/it/to/
```    

### https://github.com/jendakol/rbackup

