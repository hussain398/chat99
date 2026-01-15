
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>تطبيق شات</title>

<style>
body {
  font-family: Arial;
  background: linear-gradient(to bottom, #87CEEB, #E0F6FF);
  height: 100vh;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.box {
  background: white;
  width: 360px;
  padding: 20px;
  border-radius: 10px;
}

input, button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
}

button {
  background: #1E90FF;
  color: white;
  border: none;
}

#messages {
  border: 1px solid #ccc;
  height: 150px;
  overflow-y: auto;
  padding: 5px;
}

.chatItem {
  padding: 5px;
  border-bottom: 1px solid #eee;
  cursor: pointer;
}
</style>
</head>

<body>

<!-- تسجيل الدخول -->
<div id="loginBox" class="box">
  <h2>تسجيل الدخول</h2>
  <input id="username" placeholder="اسم الحساب">
  <input id="password" type="password" placeholder="رقم المرور">
  <button type="button" onclick="login()">دخول</button>
  <p id="loginMsg"></p>
</div>

<!-- الشات -->
<div id="chatBox" class="box" style="display:none">
  <p>مرحبًا <b id="myName"></b></p>
  <p>ID الخاص بك: <b id="myId"></b></p>

  <h4>المحادثات</h4>
  <div id="chatsList"></div>

  <input id="friendId" placeholder="اكتب ID صديقك">
  <button type="button" onclick="searchFriend()">بحث</button>
  <p id="searchResult"></p>

  <div id="messages"></div>

  <input id="msgInput" placeholder="اكتب رسالة">
  <button type="button" onclick="sendMessage()">إرسال</button>
</div>

<script>
function getUsers() {
  return JSON.parse(localStorage.getItem("users") || "[]");
}

function saveUsers(users) {
  localStorage.setItem("users", JSON.stringify(users));
}

function generateId() {
  return Math.floor(10000000 + Math.random() * 90000000);
}

let currentUser = null;
let currentFriend = null;

function login() {
  const u = username.value.trim();
  const p = password.value.trim();

  // تحقق من الاسم
  if (!u) {
    loginMsg.innerText = "❌ اكتب اسم الحساب";
    return;
  }

  // تحقق من كلمة المرور (أرقام فقط + 6 أرقام على الأقل)
  if (!/^\d{6,}$/.test(p)) {
    loginMsg.innerText = "❌ كلمة المرور يجب أن تكون 6 أرقام على الأقل";
    return;
  }

  let users = getUsers();
  let user = users.find(x => x.username === u);

  if (!user) {
    // إنشاء حساب جديد
    user = {
      username: u,
      password: p,
      id: generateId()
    };
    users.push(user);
    saveUsers(users);
  } else if (user.password !== p) {
    loginMsg.innerText = "❌ رقم المرور غير صحيح";
    return;
  }

  currentUser = user;
  myName.innerText = user.username;
  myId.innerText = user.id;

  loginBox.style.display = "none";
  chatBox.style.display = "block";

  loadChatsList();
}

function chatKey(a, b) {
  return "chat_" + [a, b].sort().join("_");
}

function searchFriend() {
  const users = getUsers();
  currentFriend = users.find(u => u.id == friendId.value && u.id != currentUser.id);

  if (currentFriend) {
    searchResult.innerText = "✅ تم العثور على " + currentFriend.username;
    saveChat(currentFriend);
    loadMessages();
    loadChatsList();
  } else {
    searchResult.innerText = "❌ لم يتم العثور";
  }
}

function saveChat(friend) {
  const key = "myChats_" + currentUser.id;
  let chats = JSON.parse(localStorage.getItem(key) || "[]");

  if (!chats.find(c => c.id === friend.id)) {
    chats.push(friend);
    localStorage.setItem(key, JSON.stringify(chats));
  }
}

function loadChatsList() {
  const key = "myChats_" + currentUser.id;
  const chats = JSON.parse(localStorage.getItem(key) || "[]");
  chatsList.innerHTML = "";

  chats.forEach(c => {
    const div = document.createElement("div");
    div.className = "chatItem";
    div.innerText = c.username + " (" + c.id + ")";
    div.onclick = () => {
      currentFriend = c;
      loadMessages();
    };
    chatsList.appendChild(div);
  });
}

function loadMessages() {
  if (!currentFriend) return;
  const key = chatKey(currentUser.id, currentFriend.id);
  const msgs = JSON.parse(localStorage.getItem(key) || "[]");
  messages.innerHTML = "";
  msgs.forEach(m => {
    messages.innerHTML += `<div><b>${m.from}:</b> ${m.text}</div>`;
  });
}

function sendMessage() {
  if (!currentFriend || !msgInput.value) return;
  const key = chatKey(currentUser.id, currentFriend.id);
  const msgs = JSON.parse(localStorage.getItem(key) || "[]");
function sendMessage() {
  if (!currentFriend || !msgInput.value) return;

  const key = chatKey(currentUser.id, currentFriend.id);
  const msgs = JSON.parse(localStorage.getItem(key) || "[]");

  msgs.push({
    from: currentUser.username,
    text: msgInput.value
  });

  localStorage.setItem(key, JSON.stringify(msgs));

  // ⭐ حفظ الصديق في قائمة المحادثات
  saveChat(currentFriend);
  loadChatsList();

  msgInput.value = "";
  loadMessages();
}

  msgs.push({ from: currentUser.username, text: msgInput.value });
  localStorage.setItem(key, JSON.stringify(msgs));
  msgInput.value = "";
  loadMessages();
}

setInterval(loadMessages, 1000);
</script>

</body>
</html>
