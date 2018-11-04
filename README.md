# What the heck ArrayBuffer and Blob are?

## Intro

**ArrayBuffer** object is used to represent generic, fixed-length raw binary data buffer. You cannot directly manipulate the contents of an ArrayBuffer; instead, you create one of the typed array objects or a DataView object which represents the buffer in a specific format, and use that to read and write the contents of the buffer. 

**Blob** object represents a file-like object of immutable, raw data. Blobs represent data that is not necessarily in a JS format. The File interface is based on Blob, inheriting blob functionality and expanding it to support files on user's system. 

## Comparison

* Unless you need the ability to write/edit using an **ArrayBuffer**, then **Blob** format is probably the best.

* An **ArrayBuffer** can be manipulated by using *TypedArrays* and *DataView*, whereas **Blob** is immutable. 

* An **ArrayBuffer** is in memory, available for manipulation. A **Blob** can be on disk, in cache memory, and other places that are not readily available. 

* **Blob** can be passed directly into other functions like ```window.URL.createObjectURL()```.However, you may still need File APIs like *FileReader* to work with **Blob**.

* You can convert Blob to ArrayBuffer, and the other way also holds true. 
   * **Blob** can become an **ArrayBuffer** using *FileReader*'s ```readAsArrayBuffer()```method. 
   * **ArrayBuffer** can also become **Blob** by using ```new Blob([new Uint8Array(data]); ```.
   
While working with HTTP, **Blob** and **ArrayBuffer** are implemented as follows:

```javascript
function GET(url, callback) {
  var xhr = new XMLHttpRequest();
  xhr.open('GET', url, true);
  xhr.responseType = 'arraybuffer'; // or xhr.responseType = "blob";
  xhr.send();

  xhr.onload = function(e) {
    if (xhr.status != 200) {
      alert("Unexpected status code " + xhr.status + " for " + url);
      return false;
    }
    callback(new Uint8Array(xhr.response)); // or new Blob([xhr.response]);
  };
}
```

