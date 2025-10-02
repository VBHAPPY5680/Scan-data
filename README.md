<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Order / Product / Remarks Sections</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <style>
    body {
      margin: 0;
      font-family: "Segoe UI", sans-serif;
      background: #1e1e1e;
      padding: 20px;
      color: #fff;
    }

    .chat-box {
      max-width: 700px;
      margin: 20px auto;
      padding: 16px;
      border-radius: 14px;
      background: #2a2a2a;
      box-shadow: 0 2px 8px rgba(0,0,0,0.4);
    }

    .chat-label {
      font-size: 15px;
      margin-bottom: 8px;
      font-weight: bold;
      color: #ccc;
    }

    .chat-messages {
      min-height: 100px;
      padding: 10px;
      margin-bottom: 12px;
      border-radius: 10px;
      background: #242424;
      overflow-y: auto;
      max-height: 200px;
    }

    .msg {
      padding: 8px 12px;
      margin: 6px 0;
      border-radius: 10px;
      max-width: 80%;
      word-wrap: break-word;
    }

    .user-msg {
      margin-left: auto;
      background: #3d7eff;
      color: #fff;
    }

    .bot-msg {
      background: #444;
      color: #fff;
    }

    .chat-input {
      display: flex;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;
    }

    .chat-input input[type="text"] {
      flex: 1;
      padding: 12px;
      border-radius: 10px;
      font-size: 15px;
      border: 1px solid #555;
      background: #333;
      color: #fff;
    }

    .chat-input button {
      padding: 10px 16px;
      border: none;
      border-radius: 10px;
      font-size: 15px;
      font-weight: bold;
      background: #3d7eff;
      color: #fff;
      cursor: pointer;
    }

    .icon-btn {
      font-size: 18px;
      border-radius: 50%;
      width: 42px;
      height: 42px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #444;
      cursor: pointer;
    }

    .file-input {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Section 1: Order No -->
  <div class="chat-box">
    <div class="chat-label">Order No</div>
    <div class="chat-messages" id="chat1"></div>
    <div class="chat-input">
      <input id="input1" type="text" placeholder="Enter order number..." />
      <label class="icon-btn" for="file1">📎</label>
      <input type="file" id="file1" class="file-input" />
      <div class="icon-btn">📷</div>
      <div class="icon-btn">📷</div>
      <button id="send1">Send</button>
    </div>
  </div>

  <!-- Section 2: Product -->
  <div class="chat-box">
    <div class="chat-label">Product</div>
    <div class="chat-messages" id="chat2"></div>
    <div class="chat-input">
      <input id="input2" type="text" placeholder="Enter product name..." />
      <label class="icon-btn" for="file2">📎</label>
      <input type="file" id="file2" class="file-input" />
      <div class="icon-btn">📷</div>
      <div class="icon-btn">📷</div>
      <button id="send2">Send</button>
    </div>
  </div>

  <!-- Section 3: Remarks -->
  <div class="chat-box">
    <div class="chat-label">Remarks</div>
    <div class="chat-messages" id="chat3"></div>
    <div class="chat-input">
      <input id="input3" type="text" placeholder="Enter remarks..." />
      <label class="icon-btn" for="file3">📎</label>
      <input type="file" id="file3" class="file-input" />
      <div class="icon-btn">📷</div>
      <div class="icon-btn">📷</div>
      <button id="send3">Send</button>
    </div>
  </div>

  <script>
    function setupChat(inputId, btnId, chatId, fileId) {
      const input = document.getElementById(inputId);
      const btn = document.getElementById(btnId);
      const chat = document.getElementById(chatId);
      const fileInput = document.getElementById(fileId);

      btn.addEventListener("click", () => {
        const val = input.value.trim();
        if (!val) return;
        const userMsg = document.createElement("div");
        userMsg.className = "user-msg msg";
        userMsg.textContent = val;
        chat.appendChild(userMsg);
        input.value = "";
        setTimeout(() => {
          const botMsg = document.createElement("div");
          botMsg.className = "bot-msg msg";
          botMsg.textContent = "✅ Saved";
          chat.appendChild(botMsg);
          chat.scrollTop = chat.scrollHeight;
        }, 400);
      });

      fileInput.addEventListener("change", () => {
        if (fileInput.files.length > 0) {
          const fileMsg = document.createElement("div");
          fileMsg.className = "user-msg msg";
          fileMsg.textContent = "📎 " + fileInput.files[0].name;
          chat.appendChild(fileMsg);
          chat.scrollTop = chat.scrollHeight;
        }
      });
    }

    setupChat("input1", "send1", "chat1", "file1");
    setupChat("input2", "send2", "chat2", "file2");
    setupChat("input3", "send3", "chat3", "file3");
  </script>

</body>
</html>
