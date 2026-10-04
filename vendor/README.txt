Third-party files used by the photo check on the captain page (runs on the captain's phone; nothing is uploaded).
Two face detectors: SSD MobileNet makes the count, YuNet gives a second opinion (the rules are in ../facecount.js).

  face-api.js                           browser bundle of @vladmandic/face-api 1.7.15 (includes TensorFlow.js), MIT — LICENSE-face-api.txt
  models/ssd_mobilenetv1_model.*        its SSD MobileNet v1 face detector, from the same package (model/). 5.4 MB, ~3.7 MB over the wire
  ort/ort.wasm.min.js                   onnxruntime-web 1.22.0 (WebAssembly build), MIT — LICENSE-onnxruntime.txt
  ort/ort-wasm-simd-threaded.wasm|.mjs  its WebAssembly engine and loader (11 MB, ~2.9 MB over the wire)
  models/yunet.onnx                     YuNet face detector (OpenCV Zoo, face_detection_yunet_2023mar), MIT — LICENSE-yunet.txt. 0.2 MB.
                                        Only its declared input size was opened up (any size divisible by 32 instead of 640 × 640);
                                        the weights are untouched — see ../../tools/yunet-anysize.py.

All of it (~7 MB over the wire) is fetched in the background once the claim form shows, and the phone keeps it.

History: until 3 Oct 2026 the page used face-api's TinyFaceDetector (190 KB) and an age/gender model. Tiny found 0 faces in
15-28 person team photos; the age/gender guess called most of a women's team "men". Both were removed. On 4 Oct YuNet was added:
SSD alone counted the owner's 15-person stand selfie as 17-18 (two boxes between heads — now merged) and missed faces under hat
brims and half-hidden; with YuNet's second opinion the page counts 27 of 27 test photos exactly, in Chrome and in WebKit.

Sources and checks:
  @vladmandic/face-api@1.7.15   npm tarball sha512 = registry dist.integrity
                                (sha512-WDMmK3CfNLo8jylWqMoQgf4nIst3M0fzx1dnac96wv/dvMTN4DxC/Pq1DGtduDk1lktCamQ3MIDXFnvrdHTXDw==)
  onnxruntime-web@1.22.0        npm tarball sha512 = registry dist.integrity
                                (sha512-Ud/+EBo6mhuaQWt/OjaOk0iNWjXqJoeeMFr6xQEERZdIZH2OWpGzuujz7lfuOBjUa6TEE/sc4nb7Da5dNL34fg==)
  YuNet 2023mar                 sha256 8f2383e4dd3cfbb4553ea8718107fc0423210dc964f9f4280604804ed2552fa4 = opencv_zoo's Git LFS object
The files are byte-for-byte copies (yunet.onnx: the edited one); tests/web.test.js pins every one's sha256.
