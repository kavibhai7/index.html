# index.html
<!DOCTYPE html>
<html>
<head>
    <title>College AI Chatbot</title>
    <script>
        async function sendMessage() {
            let userMessage = document.getElementById("userInput").value;
            let response = await fetch("https://api-inference.huggingface.co/models/microsoft/DialoGPT-medium", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ inputs: userMessage })
            });
            let data = await response.json();
            document.getElementById("chatbox").innerHTML += "<p><b>You:</b> " + userMessage + "</p>";
            document.getElementById("chatbox").innerHTML += "<p><b>Bot:</b> " + data[0]["generated_text"] + "</p>";
        }
    </script>
</head>
<body>
    <h1>College AI Chatbot</h1>
    <div id="chatbox"></div>
    <input type="text" id="userInput" placeholder="Ask something..." />
    <button onclick="sendMessage()">Send</button>
</body>
</html>
