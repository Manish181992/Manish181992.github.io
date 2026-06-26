---
layout: splash
title: Beautify JSON
permalink: /toolchest/beautify_json/
---

<div class="toolarea">
    <h6>WARNING: Duplicate keys will be removed from the beautified JSON output.</h6>
    <textarea id="jsonText" rows="12" placeholder="JSON string..."></textarea>
    
    <div class="controls">
        <button onclick="beautifyJson()">
          <span>Beautify</span>
        </button>
    </div>
    <textarea id="errorOutput"></textarea>
</div>

<style>
    
    .toolarea {
        display: flex !important;
        flex-direction: column;
        align-items: center;
        gap: 20px;
        
        padding: 20px !important;
    }

    #jsonText {
        background-color: white !important;
        color: black;
    }
    
    #errorOutput {
        color: red;
    }
</style>

<script>
    function beautifyJson() {
        const jsonTextElement = document.getElementById('jsonText');
        const errorOutputElement = document.getElementById('errorOutput');
        errorOutputElement.value = "";
        const jsonString = jsonTextElement.value;
        if (!jsonString) {
            return;
        }
        
        try {
            const jsonObject = JSON.parse(jsonString);
            jsonTextElement.value = JSON.stringify(jsonObject, null, 4);
        } catch (error) {
            if (error instanceof SyntaxError) {
                console.error('Invalid JSON syntax:', error.message);
            } else {
                console.error('Unexpected error:', error);
            }
            errorOutputElement.value = error.message;
        } 
    }
</script>
