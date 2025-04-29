<template>
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
</style>