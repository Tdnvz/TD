# TD
برای برانامه ریزی روزانه
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>برنامه روزانه</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            transition: background 0.5s, color 0.5s;
        }
        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .theme-button {
            margin: 10px;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .theme-light {
            background: #f9f9f9;
            color: #333;
        }
        .theme-dark {
            background: #333;
            color: #f9f9f9;
        }
        .theme-blue {
            background: #007BFF;
            color: #fff;
        }
        .theme-green {
            background: #28a745;
            color: #fff;
        }
        .chatbox {
            margin-top: 20px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            background: white;
        }
        .chat-input {
            width: 80%;
            padding: 10px;
            margin-top: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body class="theme-light">
    <div class="container">
        <h1>برنامه روزانه</h1>
        <p>برنامه‌ای برای مدیریت بهتر روز</p>
        <button class="theme-button" onclick="changeTheme('theme-light')">روشن</button>
        <button class="theme-button" onclick="changeTheme('theme-dark')">تاریک</button>
        <button class="theme-button" onclick="changeTheme('theme-blue')">آبی</button>
        <button class="theme-button" onclick="changeTheme('theme-green')">سبز</button>
        
        <div class="chatbox" id="chatbox">
            <p><strong>ChatGPT:</strong> سلام! چه کمکی از دستم برمیاد؟</p>
        </div>
        <input type="text" id="userInput" class="chat-input" placeholder="پیامت رو بنویس..." />
        <button class="theme-button" onclick="sendMessage()">ارسال</button>
    </div>
    
    <script>
        function changeTheme(theme) {
            document.body.className = theme;
        }
        
        async function sendMessage() {
            let userInput = document.getElementById("userInput").value;
            let chatbox = document.getElementById("chatbox");
            
            if (userInput.trim() === "") return;
            
            chatbox.innerHTML += `<p><strong>شما:</strong> ${userInput}</p>`;
            document.getElementById("userInput").value = "";
            
            let response = await fetch("https://api.openai.com/v1/completions", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "Authorization": "Bearer YOUR_OPENAI_API_KEY"
                },
                body: JSON.stringify({
                    model: "text-davinci-003",
                    prompt: userInput,
                    max_tokens: 100
                })
            });
            
            let data = await response.json();
            let botMessage = data.choices[0].text.trim();
            chatbox.innerHTML += `<p><strong>ChatGPT:</strong> ${botMessage}</p>`;
        }
    </script>
</body>
</html>
