<!-- <template>
  <div>
    <button @click="downloadPdf('SALE_AGREEMENT', 'TestDocument.pdf')">
      Download PDF xdddddddddddddddddddddddddd
    </button>
  </div>
</template>

<script>
export default {
  name: "DownloadPdf",
  methods: {
    async downloadPdf(doctype, name) {
      try {
        // Map doctype to type for potential future use
        const typeMap = {
          SALE_AGREEMENT: "saleagreement",
          COC: "projectcompletion",
        };
        const type = typeMap[doctype] || "loandocs";

        // Hardcoded base64 PDF string (minimal valid PDF saying "Hello, World!")
        const base64Data = "JVBERi0xLjQKJeLjz9MKMSAwIG9iago8PC9UeXBlL1BhZ2UvUGFyZW50IDIgMCBSL1Jlc291cmNlcyA8PC9Gb250IDw8L0YxIDMgMCBSPj4+Pi9NZWRpYUJveFswIDAgNjEyIDc5Ml0vQ29udGVudHMgNCAwIFI+PgplbmRvYmoKMiAwIG9iago8PC9UeXBlL1BhZ2VzL0tpZHMgWzEgMCBSXS9Db3VudCAxPj4KZW5kb2JqCjMgMCBvYmoKPDwvVHlwZS9Gb250L1N1YnR5cGUvVHlwZTEvTmFtZS9GMS9CYXNlRm9udC9IZWx2ZXRpY2EvRW5jb2RpbmcvV2luQW5zaUVuY29kaW5nPj4KZW5kb2JqCjQgMCBvYmoKPDwvTGVuZ3RoIDYxPj4Kc3RyZWFtCkJUIAovRjEgMTIgVGYKMzAwIDcwMCBUZAooSGVsbG8sIFdvcmxkISkgVGoKRVQKZW5kc3RyZWFtCmVuZG9iagp4cmVmCjAgNQowMDAwMDAwMDAwIDY1NTM1IGYgCjAwMDAwMDAwMTAgMDAwMDAgbiAKMDAwMDAwMDA3NSAwMDAwMCBuIAowMDAwMDAwMTc5IDAwMDAwIG4gCjAwMDAwMDAyNTkgMDAwMDAgbiAKdHJhaWxlcgo8PC9TaXplIDUvUm9vdCAyIDAgUi9JbmZvIDYgMCBSCj4+CnN0YXJ0eHJlZgozMjYKYl9c";

        // Validate base64 data
        if (typeof base64Data !== "string" || !base64Data.match(/^[A-Za-z0-9+/=]+$/)) {
          throw new Error("Invalid base64 data");
        }

        // Convert base64 to binary
        const binaryData = atob(base64Data);
        const arrayBuffer = new ArrayBuffer(binaryData.length);
        const byteArray = new Uint8Array(arrayBuffer);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        // Create Blob
        const blob = new Blob([byteArray], { type: "application/pdf" });
        const url = window.URL.createObjectURL(blob);

        // Detect Safari
        const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

        // Handle download
        const link = document.createElement("a");
        link.href = url;
        link.download = name;

        if (isSafari) {
          // For Safari, set the href and trigger download without opening a new tab
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
        } else {
          // Standard download for other browsers
          document.body.appendChild(link);
          link.click();
          document.body.removeChild(link);
        }

        // Cleanup object URL after a delay
        setTimeout(() => URL.revokeObjectURL(url), 5000);
      } catch (err) {
        console.error("Download failed:", err);
        alert("Failed to download document. Please try again.");
      }
    },
  },
};
</script>

<style scoped>
button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
</style> -->


<template>
  <div>
    <button @click="downloadPdf">Download PDF</button>
  </div>
</template>

<script>
export default {
  name: "DownloadPdf",
  methods: {
    downloadPdf() {
      try {
        // Minimal valid base64-encoded PDF (displays "Hello, World!")
        const base64Data = "JVBERi0xLjQKJeLjz9MKMSAwIG9iago8PC9UeXBlL1BhZ2UvUGFyZW50IDIgMCBSL1Jlc291cmNlcyA8PC9Gb250IDw8L0YxIDMgMCBSPj4+Pi9NZWRpYUJveFswIDAgNjEyIDc5Ml0vQ29udGVudHMgNCAwIFI+PgplbmRvYmoKMiAwIG9iago8PC9UeXBlL1BhZ2VzL0tpZHMgWzEgMCBSXS9Db3VudCAxPj4KZW5kb2JqCjMgMCBvYmoKPDwvVHlwZS9Gb250L1N1YnR5cGUvVHlwZTEvTmFtZS9GMS9CYXNlRm9udC9IZWx2ZXRpY2EvRW5jb2RpbmcvV2luQW5zaUVuY29kaW5nPj4KZW5kb2JqCjQgMCBvYmoKPDwvTGVuZ3RoIDYxPj4Kc3RyZWFtCkJUIAovRjEgMTIgVGYKMzAwIDcwMCBUZAooSGVsbG8sIFdvcmxkISkgVGoKRVQKZW5kc3RyZWFtCmVuZG9iagp4cmVmCjAgNQowMDAwMDAwMDAwIDY1NTM1IGYgCjAwMDAwMDAwMTAgMDAwMDAgbiAKMDAwMDAwMDA3NSAwMDAwMCBuIAowMDAwMDAwMTc5IDAwMDAwIG4gCjAwMDAwMDAyNTkgMDAwMDAgbiAKdHJhaWxlcgo8PC9SaXplIDUvUm9vdCAxIDAgUj4+CnN0YXJ0eHJlZgozMDUKJSURRg==";

        // Validate base64 format
        if (!base64Data.match(/^[A-Za-z0-9+/=]+$/)) {
          throw new Error("Invalid base64 format");
        }
        console.log("Base64 length:", base64Data.length);

        // Decode base64 to binary
        const binaryData = atob(base64Data);
        console.log("Binary length:", binaryData.length);

        // Convert to ArrayBuffer
        const byteArray = new Uint8Array(binaryData.length);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        // Create Blob
        const blob = new Blob([byteArray], { type: "application/pdf" });
        console.log("Blob created:", blob.size, "bytes");

        // Create download link
        const url = window.URL.createObjectURL(blob);
        const link = document.createElement("a");
        link.href = url;
        link.download = "TestDocument.pdf";

        // Trigger download
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);

        // Cleanup
        setTimeout(() => {
          window.URL.revokeObjectURL(url);
          console.log("URL revoked");
        }, 100);
      } catch (error) {
        console.error("PDF download failed:", error);
        alert(`Failed to download PDF: ${error.message}`);
      }
    },
  },
};
</script>

<style scoped>
button {
  padding: 12px 24px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #218838;
}

button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.3);
}
</style>



<template>
  <div>
    <button @click="downloadPdf">Download PDF</button>
  </div>
</template>

<script>
export default {
  name: "DownloadPdf",
  methods: {
    downloadPdf() {
      try {
        // Minimal valid base64-encoded PDF (displays "Hello, World!")
        const base64Data = "JVBERi0xLjYNJeLjz9MNCjI0IDAgb2JqDTw8L0ZpbHRlci9GbGF0ZURlY29kZS9GaXJzdCA0L0xlbmd0aCAyMTYvTiAxL1R5cGUvT2JqU3RtPj5zdHJlYW0NCmjePI9RS8MwFIX/yn1bi9jepCQ6GYNpFBTEMsW97CVLbjWYNpImmz/fVsXXcw/f/c4SEFarepPTe4iFok8dU09DgtDBQx6TMwT74vaLTE7uSPDUdXM0Xe/73r1FnVwYYEtHR6d9WdY3kX4ipRMV6oojSmxQMoGyac5RLBAXf63p38aGA7XPorLewyvFcYaJile8rB+D/YcwiRdMMGScszO8/IW0MdhsaKKYGA46gXKTr/cUQVY4We/cYMNpnLVeXPJUXHs9fECr7kAFk+eZ5Xr9LcAAfKpQrA0KZW5kc3RyZWFtDWVuZG9iag0yNSAwIG9iag08PC9GaWx0ZXIvRmxhdGVEZWNvZGUvRmlyc3QgNC9MZW5ndGggNDkvTiAxL1R5cGUvT2JqU3RtPj5zdHJlYW0NCmjeslAwULCx0XfOL80rUTDU985MKY42NAIKBsXqh1QWpOoHJKanFtvZAQQYAN/6C60NCmVuZHN0cmVhbQ1lbmRvYmoNMjYgMCBvYmoNPDwvRmlsdGVyL0ZsYXRlRGVjb2RlL0ZpcnN0IDkvTGVuZ3RoIDQyL04gMi9UeXBlL09ialN0bT4+c3RyZWFtDQpo3jJTMFAwVzC0ULCx0fcrzS2OBnENFIJi7eyAIsH6LnZ2AAEGAI2FCDcNCmVuZHN0cmVhbQ1lbmRvYmoNMjcgMCBvYmoNPDwvRmlsdGVyL0ZsYXRlRGVjb2RlL0ZpcnN0IDUvTGVuZ3RoIDEyMC9OIDEvVHlwZS9PYmpTdG0+PnN0cmVhbQ0KaN4yNFIwULCx0XfOzytJzSspVjAyBgoE6TsX5Rc45VdEGwB5ZoZGCuaWRrH6vqkpmYkYogGJRUCdChZgfUGpxfmlRcmpxUAzA4ryk4NTS6L1A1zc9ENSK0pi7ez0g/JLEktSFQz0QyoLUoF601Pt7AACDADYoCeWDQplbmRzdHJlYW0NZW5kb2JqDTIgMCBvYmoNPDwvTGVuZ3RoIDM1MjUvU3VidHlwZS9YTUwvVHlwZS9NZXRhZGF0YT4+c3RyZWFtDQo8P3hwYWNrZXQgYmVnaW49Iu+7vyIgaWQ9Ilc1TTBNcENlaGlIenJlU3pOVGN6a2M5ZCI/Pgo8eDp4bXBtZXRhIHhtbG5zOng9ImFkb2JlOm5zOm1ldGEvIiB4OnhtcHRrPSJBZG9iZSBYTVAgQ29yZSA1LjQtYzAwNSA3OC4xNDczMjYsIDIwMTIvMDgvMjMtMTM6MDM6MDMgICAgICAgICI+CiAgIDxyZGY6UkRGIHhtbG5zOnJkZj0iaHR0cDovL3d3dy53My5vcmcvMTk5OS8wMi8yMi1yZGYtc3ludGF4LW5zIyI+CiAgICAgIDxyZGY6RGVzY3JpcHRpb24gcmRmOmFib3V0PSIiCiAgICAgICAgICAgIHhtbG5zOnBkZj0iaHR0cDovL25zLmFkb2JlLmNvbS9wZGYvMS4zLyIKICAgICAgICAgICAgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIgogICAgICAgICAgICB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIKICAgICAgICAgICAgeG1sbnM6ZGM9Imh0dHA6Ly9wdXJsLm9yZy9kYy9lbGVtZW50cy8xLjEvIj4KICAgICAgICAgPHBkZjpQcm9kdWNlcj5BY3JvYmF0IERpc3RpbGxlciA2LjAgKFdpbmRvd3MpPC9wZGY6UHJvZHVjZXI+CiAgICAgICAgIDx4bXA6Q3JlYXRlRGF0ZT4yMDA2LTAzLTA2VDE1OjA2OjMzLTA1OjAwPC94bXA6Q3JlYXRlRGF0ZT4KICAgICAgICAgPHhtcDpDcmVhdG9yVG9vbD5BZG9iZVBTNS5kbGwgVmVyc2lvbiA1LjIuMjwveG1wOkNyZWF0b3JUb29sPgogICAgICAgICA8eG1wOk1vZGlmeURhdGU+MjAxNi0wNy0xNVQxMDoxMjoyMSswODowMDwveG1wOk1vZGlmeURhdGU+CiAgICAgICAgIDx4bXA6TWV0YWRhdGFEYXRlPjIwMTYtMDctMTVUMTA6MTI6MjErMDg6MDA8L3htcDpNZXRhZGF0YURhdGU+CiAgICAgICAgIDx4bXBNTTpEb2N1bWVudElEPnV1aWQ6ZmYzZGNmZDEtMjNmYS00NzZmLTgzOWEtM2U1Y2FlMmRhMmViPC94bXBNTTpEb2N1bWVudElEPgogICAgICAgICA8eG1wTU06SW5zdGFuY2VJRD51dWlkOjM1OTM1MGIzLWFmNDAtNGQ4YS05ZDZjLTAzMTg2YjRmZmIzNjwveG1wTU06SW5zdGFuY2VJRD4KICAgICAgICAgPGRjOmZvcm1hdD5hcHBsaWNhdGlvbi9wZGY8L2RjOmZvcm1hdD4KICAgICAgICAgPGRjOnRpdGxlPgogICAgICAgICAgICA8cmRmOkFsdD4KICAgICAgICAgICAgICAgPHJkZjpsaSB4bWw6bGFuZz0ieC1kZWZhdWx0Ij5CbGFuayBQREYgRG9jdW1lbnQ8L3JkZjpsaT4KICAgICAgICAgICAgPC9yZGY6QWx0PgogICAgICAgICA8L2RjOnRpdGxlPgogICAgICAgICA8ZGM6Y3JlYXRvcj4KICAgICAgICAgICAgPHJkZjpTZXE+CiAgICAgICAgICAgICAgIDxyZGY6bGk+RGVwYXJ0bWVudCBvZiBKdXN0aWNlIChFeGVjdXRpdmUgT2ZmaWNlIG9mIEltbWlncmF0aW9uIFJldmlldyk8L3JkZjpsaT4KICAgICAgICAgICAgPC9yZGY6U2VxPgogICAgICAgICA8L2RjOmNyZWF0b3I+CiAgICAgIDwvcmRmOkRlc2NyaXB0aW9uPgogICA8L3JkZjpSREY+CjwveDp4bXBtZXRhPgogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAKICAgICAgICAgICAgICAgICAgICAgICAgICAgCjw/eHBhY2tldCBlbmQ9InciPz4NCmVuZHN0cmVhbQ1lbmRvYmoNMTEgMCBvYmoNPDwvTWV0YWRhdGEgMiAwIFIvUGFnZUxhYmVscyA2IDAgUi9QYWdlcyA4IDAgUi9UeXBlL0NhdGFsb2c+Pg1lbmRvYmoNMjMgMCBvYmoNPDwvRmlsdGVyL0ZsYXRlRGVjb2RlL0xlbmd0aCAxMD4+c3RyZWFtDQpIiQIIMAAAAAABDQplbmRzdHJlYW0NZW5kb2JqDTI4IDAgb2JqDTw8L0RlY29kZVBhcm1zPDwvQ29sdW1ucyA0L1ByZWRpY3RvciAxMj4+L0ZpbHRlci9GbGF0ZURlY29kZS9JRFs8REI3Nzc1Q0NFMjI3RjZCMzBDNDQwREY0MjIxREMzOTA+PEJGQ0NDRjNGNTdGNjEzNEFCRDNDMDRBOUU0Q0ExMDZFPl0vSW5mbyA5IDAgUi9MZW5ndGggODAvUm9vdCAxMSAwIFIvU2l6ZSAyOS9UeXBlL1hSZWYvV1sxIDIgMV0+PnN0cmVhbQ0KaN5iYgACJjDByGzIwPT/73koF0wwMUiBWYxA4v9/EMHA9I/hBVCxoDOQeH8DxH2KrIMIglFwIpD1vh5IMJqBxPpArHYgwd/KABBgAP8bEC0NCmVuZHN0cmVhbQ1lbmRvYmoNc3RhcnR4cmVmDQo0NTc2DQolJUVPRg0K";



        // Validate base64 format
        if (!base64Data.match(/^[A-Za-z0-9+/=]+$/)) {
          throw new Error("Invalid base64 format");
        }
        console.log("Base64 length:", base64Data.length);

        // Decode base64 to binary
        const binaryData = atob(base64Data);
        console.log("Binary length:", binaryData.length);

        // Convert to ArrayBuffer
        const byteArray = new Uint8Array(binaryData.length);
        for (let i = 0; i < binaryData.length; i++) {
          byteArray[i] = binaryData.charCodeAt(i);
        }

        // Create Blob
        const blob = new Blob([byteArray], { type: "application/pdf" });
        console.log("Blob created:", blob.size, "bytes");

        // Create download link
        const url = window.URL.createObjectURL(blob);
        const link = document.createElement("a");
        link.href = url;
        link.download = "TestDocument.pdf";

        // Trigger download
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);

        // Cleanup
        setTimeout(() => {
          window.URL.revokeObjectURL(url);
          console.log("URL revoked");
        }, 100);
      } catch (error) {
        console.error("PDF download failed:", error);
        alert(`Failed to download PDF: ${error.message}`);
      }
    },
  },
};
</script>

<style scoped>
button {
  padding: 12px 24px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #218838;
}

button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.3);
}
</style>