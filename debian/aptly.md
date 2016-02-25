# Aptly - Repository Management

Aptly is a great free tool to manage Debian package repositories. It offers
mirroring, snapshots, publishing and signing of Debian packages.

## Managing Personal Packages

Note: aptly will create a default config file in the users home directory if it
does not already exist.
    
    aptly repo create -distribution=squeeze -component=main aptly-release
    aptly repo add aptly-release ./debs
    aptly repo show -with-packages aptly-release
    aptly snapshot create aptly-0.1 from repo aptly-release
    aptly snapshot list
    aptly publish -skip-signing snapshot aptly-0.1

## References

https://github.com/smira/aptly
http://www.aptly.info/download
