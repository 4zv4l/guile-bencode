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

(let ((h (make-hash-table)))
  (hash-set! h "name" "4zv4l")
  (hash-set! h "age" 99)
  (hash-set! h "cn" (list "BE" "CN" "VT" "TH"))
  (format #t "~A~%" (bencode h)))
```
which gives:
```
a: http://bttracker.debian.org:6969/announce
c: Debian CD from cdimage.debian.org
n: debian-12.11.0-amd64-netinst.iso
d3:agei99e2:cnl2:BE2:CN2:VT2:THe4:name5:4zv4le
```

# Doc

`bencode val`: encode `val` to bencode, `val` must be a string, number, list or hash-table.
`bdecode port`: decode bencode stream from `port`.
