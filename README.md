# [GenerateScanBarcode](https://ashfaqalizardariofficial.github.io/GenerateScanBarcode.github.io) 
by ***Ashfaq Ali Zardari*** 
The JavaScript programming code to generate and scan barcodes.

## Generate Barcode Method and Usage.
```
<!-- Generate Barcode library. -->
<script src="./jquery.min.js"></script>

<!-- Barcode Generate. -->
<script src="./JsBarcode.all.js"></script>

<!-- Barcode Scannner. -->
<script src="./quagga.min.js"></script>

<div style="text-align: center;overflow-x: auto;">
  <svg id="barcodeSvg" style="position: absolute;"></svg>
  <img id="barcodeImg" />
</div>

<script type="text/javascript">
// Init Barcode Code128.
function initBarcodeCode128(ElementID, DataString) {
  JsBarcode(ElementID, DataString, {
    format: "CODE128",
    displayValue: false,
    fontSize: 24,
    lineColor: "black"
  });

  // Png Image.
  var base64 = 'data:image/svg+xml;base64,' + btoa((new XMLSerializer).serializeToString($("#barcodeSvg")[0]));
  var img = document.getElementById("barcodeImg");
  img.src = base64;
}

initBarcodeCode128("#barcodeSvg", "GenerateScanBarcode by ASHFAQ ALI ZARDARI");
</script>
```

## Download Barcode as PNG Image Method and Usage.
```
<!-- Generate Barcode library. -->
<script src="./jquery.min.js"></script>

<!-- Barcode Generate. -->
<script src="./JsBarcode.all.js"></script>

<!-- Barcode Scannner. -->
<script src="./quagga.min.js"></script>

<div style="text-align: center;overflow-x: auto;">
  <svg id="barcodeSvg" style="position: absolute;"></svg>
  <img id="barcodeImg" />
</div>

<script type="text/javascript">
// Download Barcode.
function Download(src) {
  var el = document.createElement("a");
  el.setAttribute("href", src);
  el.setAttribute("download", "img_barcode");
  document.body.appendChild(el);
  el.click();
  el.remove();
}

// Get png image dataURL as src.
function GetPngDataURL(ImgElementID) {
  var img = document.getElementById(ImgElementID);
  var canvas = document.createElement("canvas");
  var w = img.width;
  var h = img.height;
  canvas.width = w;
  canvas.height = h;
  canvas.getContext("2d").drawImage(img, 0, 0, w, h);
  var imgURL = canvas.toDataURL("image/png");
  return imgURL;
}

// Download.
Download(GetPngDataURL("barcodeImg"));
</script>
```


## Scan barcode from WebCam Method and Usage.
```
<!-- Generate Barcode library. -->
<script src="./jquery.min.js"></script>

<!-- Barcode Generate. -->
<script src="./JsBarcode.all.js"></script>

<!-- Barcode Scannner. -->
<script src="./quagga.min.js"></script>

<div id="interactive" style="display: inline-grid;"></div>

<script type="text/javascript">
// Scanning Barcode.
function Scan() {
  Quagga.init({
    inputStream: {
      name: "Live",
      type: "LiveStream",
      target: document.querySelector('#interactive')
    },
    decoder: {
      readers: ["code_128_reader"]
    }
  }, function (err) {
    if (err) {
      console.log(err);
      return
    }
    console.log("Initialization finished. Ready to start");
    Quagga.start();
  });
}
function StopScan() {
  Quagga.stop();
  document.querySelector('#interactive').innerHTML = "";
}

Quagga.onDetected(function (result) {
  StopScan();
  var h2 = document.createElement("h2");
  var div = document.createElement("div");
  h2.innerHTML = `Scanned Result is: ${result.codeResult.code}`;
  div.style.textAlign = 'center';
  div.append(h2);
  document.body.append(div);
  console.log("Barcode detected and processed : [" + result.codeResult.code + "]");
});

// Start Scanning.
Scan();

</script>
```
