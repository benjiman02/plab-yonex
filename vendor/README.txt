Third-party files used by the photo check on the captain page (runs on the captain's phone; nothing is uploaded).

  face-api.js                           browser bundle of @vladmandic/face-api 1.7.15 (includes TensorFlow.js), MIT licence — see LICENSE-face-api.txt
  models/ssd_mobilenetv1_model.*        the SSD MobileNet v1 face detector's weights, from the same package (model/). 5.4 MB, about
                                        3.7 MB over the wire (GitHub Pages gzips it); the page fetches it in the background once the
                                        claim form shows, and the phone keeps it.

Until 3 Oct 2026 the page used the package's TinyFaceDetector (190 KB) and age/gender model instead. Tiny found 0 faces in
several 15–28 person team photos and 1 of 3 in a close-up selfie; the age/gender guess called most of a women's team "men".
Both were removed; the counting rules that sit on top of the detector are in ../facecount.js.

Source: npm registry, @vladmandic/face-api@1.7.15. The tarball's sha512 matched the registry's dist.integrity
(sha512-WDMmK3CfNLo8jylWqMoQgf4nIst3M0fzx1dnac96wv/dvMTN4DxC/Pq1DGtduDk1lktCamQ3MIDXFnvrdHTXDw==) before these files were taken from it
(checked again on 3 Oct 2026 when the SSD model was added). The files are byte-for-byte copies; tests/web.test.js pins their sha256
so an accidental change is caught.
