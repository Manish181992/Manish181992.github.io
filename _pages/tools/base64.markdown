---
layout: splash
title: Base64 Encoder-Decoder
permalink: /toolchest/base64/
---

<div class="toolarea">
  <textarea id="plaintext" rows="12" placeholder="Plaintext string..."></textarea>

  <div class="controls">
    <button onclick="encode()" class="btn-encode">
      <span>Encode</span>
      <i class="css-arrow"></i>
    </button>
    <button onclick="decode()" class="btn-decode">
      <i class="css-arrow"></i>
      <span>Decode</span>
    </button>
  </div>

  <textarea id="encodedText" rows="12" placeholder="Base64 encoded string..."></textarea>
</div>

<style>
    /* Using !important to bypass jekyll and minimal mistakes css overrides.*/
    .toolarea {
        display: flex !important;
        justify-content: center !important;
        align-items: stretch !important;
        gap: 20px !important;
        padding: 20px !important;
        box-sizing: border-box !important;
        height: 60vh !important;
        width: 100% !important;
    }

    #plaintext, #encodedText {
        flex: 1 !important;
        width: 100% !important;
        height: 100% !important;
        min-height: 100% !important;
        display: block !important;
        resize: none !important;
        background-color: white !important;
        color: black !important;
        border: 1px solid #ccc !important;
        border-radius: 4px !important;
        padding: 12px !important;
        box-sizing: border-box !important;
    }

    .controls {
        display: flex !important;
        flex-direction: column !important;
        justify-content: center !important;
        align-items: center !important;
        gap: 15px !important;
        flex-shrink: 0 !important;
    }

    button {
        display: inline-flex !important;
        align-items: center !important;
        justify-content: center !important;
        gap: 10px !important;
        height: 46px !important;
        padding: 0 24px !important;
        border-radius: 8px !important;
        white-space: nowrap !important;
        cursor: pointer !important;
    }

    .css-arrow {
        display: inline-block !important;
        width: 8px !important;
        height: 8px !important;
        border-top: 2px solid currentColor !important;
        border-right: 2px solid currentColor !important;
        box-sizing: border-box !important;
        flex-shrink: 0 !important;
    }

    .btn-encode .css-arrow {
        transform: rotate(45deg) !important;
        margin-top: 1px !important;
    }

    .btn-decode .css-arrow {
        transform: rotate(-135deg) !important;
        margin-top: 1px !important;
    }

    @media (max-width: 768px) {
      .toolarea {
        flex-direction: column !important;
        height: auto !important;
        gap: 15px !important;
      }

      #plaintext, #encodedText {
        flex: none !important;
        height: 20vh !important;
        min-height: 20vh !important;
      }

      .controls {
        flex-direction: row !important;
        justify-content: center !important;
        width: 100% !important;
        gap: 15px !important;
        padding: 10px 0 !important;
      }

      .btn-encode .css-arrow {
          transform: rotate(135deg) !important;
          margin-top: -2px !important;
      }

      .btn-decode .css-arrow {
          transform: rotate(-45deg) !important;
          margin-top: 2px !important;
      }
    }
</style>

<script>
    function encode() {
        const plaintextElement = document.getElementById('plaintext');
        let encodedTextElement = document.getElementById('encodedText');
        const plaintext = plaintextElement.value.trim();
        if (!plaintext) {
            encodedTextElement.value = "";
            return;
        }
        const bytes = new TextEncoder().encode(plaintext);
        const binString = Array.from(bytes, (byte) => String.fromCharCode(byte)).join("");
        encodedTextElement.value = btoa(binString);
    }

    function decode() {
        let encodedTextElement = document.getElementById('encodedText');
        let plaintextElement = document.getElementById('plaintext');
        let encodedText = encodedTextElement.value.trim();
        if (!encodedText) {
            plaintextElement.value = "";
            return;
        }
        const binString = atob(encodedText);
        const bytes = Uint8Array.from(binString, (m) => m.charCodeAt(0));
        plaintextElement.value = new TextDecoder().decode(bytes);
    }
</script>