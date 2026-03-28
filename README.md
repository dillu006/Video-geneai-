
<script>
const genBtn = document.querySelector(".gen-btn");
const output = document.getElementById("output");
const responseBox = document.querySelector(".r-box");
const textarea = document.querySelector("textarea");
const apiInput = document.querySelector(".api-wrap input");

genBtn.addEventListener("click", async () => {
  const text = textarea.value.trim();
  const apiKey = apiInput.value.trim();

  if (!text) {
    alert("Please enter something");
    return;
  }

  if (!apiKey) {
    alert("Enter API Key");
    return;
  }

  output.classList.add("show");
  responseBox.classList.add("loading");
  responseBox.innerText = "";

  try {
    const res = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer " + apiKey
      },
      body: JSON.stringify({
        model: "gpt-4o-mini",
        messages: [
          { role: "system", content: "You are a helpful Indian AI assistant." },
          { role: "user", content: text }
        ]
      })
    });

    const data = await res.json();

    responseBox.classList.remove("loading");

    if (data.choices && data.choices.length > 0) {
      responseBox.innerText = data.choices[0].message.content;
    } else {
      responseBox.innerText = "Error: No response";
    }

  } catch (err) {
    responseBox.classList.remove("loading");
    responseBox.innerText = "Error: " + err.message;
  }
});
</script>
