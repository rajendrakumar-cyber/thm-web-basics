
# 🔐 TryHackMe - Web Application Basics (Day 1)

## 📅 Date
25 March 2026

---

## 🚀 What I Learned

Today I completed the **Web Application Basics** lab on TryHackMe.

I learned the fundamentals of how web applications communicate using HTTP methods and APIs.

---

## 🧠 Key Concepts

### 🌐 HTTP Methods
- **GET** → Retrieve data
- **POST** → Send/update data
- **DELETE** → Remove data

---

### 🔗 API Interaction
- Understood how APIs work with endpoints like:


/api/user1
/api/user2

- Learned how different HTTP methods affect the server response

---

### 🛠️ Practical Tasks Completed

#### ✅ Task 1: DELETE Request
- Endpoint: `/api/user/1`
- Successfully deleted a user
- Received flag:

---

#### ✅ Task 2: POST Request (Update User)
- Endpoint: `/api/user/2`
- Updated user (Bob) country from **UK → US**
- Learned how to send data using POST body:



---

## ⚠️ Mistake I Made
- Initially sent a POST request **without data**
- Server performed unexpected action (deleted user)
- Lesson: Always check **request body + headers**

---

## 🧪 Tools Used
- TryHackMe built-in browser
- HTTP request editor

---

## 📸 Screenshot

![Lab Screenshot](./screenshot.png)

---

## 🎯 Key Takeaways
- APIs depend heavily on HTTP methods
- Small mistakes (like missing body data) can change behavior
- Understanding requests = foundation of web hacking

---

## 🔥 Next Step
- Learn **Burp Suite**
- Practice **API manipulation**
- Move to **authentication bypass labs**

---

## 💀 Goal
Become a **real-world ethical hacker** by mastering web exploitation.


