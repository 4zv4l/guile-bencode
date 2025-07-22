# guile-bencode

Bencode library for GNU Guile

# Usage

```guile
(use-modules (sibl bencode))

(let* ((deb-torrent (open-input-file
		     "debian-12.11.0-amd64-netinst.iso.torrent"
		     #:binary #t))
       (info (bdecode deb-torrent))
       (announce (hash-ref info "announce"))
       (comment (hash-ref info "comment"))
       (name (hash-ref (hash-ref info "info") "name")))
  (format #t "a: ~A~%c: ~A~%n: ~A~%" announce comment name))

```
which gives:
```
a: http://bttracker.debian.org:6969/announce
c: Debian CD from cdimage.debian.org
n: debian-12.11.0-amd64-netinst.iso
```
