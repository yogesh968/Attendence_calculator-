# 📱 Attendance Calculator — React Native

A lightweight and efficient **React Native mobile application** designed to **mark attendance** and **display attendance batch-wise**.  
The project runs using:

```
npm start
```

---

## 📑 Table of Contents
- [📘 Introduction](#-introduction)  
- [✨ Features](#-features)  
- [🛠️ Tech Stack & Dependencies](#️-tech-stack--dependencies)  
- [📥 Installation](#-installation)  
- [🚀 Running the App](#-running-the-app)  
- [📊 How Attendance Calculation Works](#-how-attendance-calculation-works)  
- [🧪 Usage Examples](#-usage-examples)  
- [⚙️ Configuration](#️-configuration)  
- [🐞 Troubleshooting](#-troubleshooting)  
- [🤝 Contributing](#-contributing)  
- [👥 Contributors](#-contributors)  
- [📄 License](#-license)

---

## 📘 Introduction
The **Attendance Calculator** app makes attendance tracking simple.  
You can **mark daily attendance**, **track student presence**, and **view attendance batch-wise** with automatic percentage calculations.

This project is ideal for:
- Coaching centers  
- Colleges / Schools  
- Training institutes  
- Any batch/group-based attendance system  

---

## ✨ Features
✔️ Mark attendance for students  
✔️ View batch-wise attendance summaries  
✔️ Automatic attendance percentage calculation  
✔️ Works with simple local storage  
✔️ Clean and modular React Native components  
✔️ Easy to extend with backend or cloud storage  

---

## 🛠️ Tech Stack & Dependencies

### **Core Technologies**
- **React Native**
- **Node.js**
- **JavaScript / TypeScript (optional)**
- **AsyncStorage** (or any persistent store)

### **Example Dependencies**
```json
{
  "dependencies": {
    "react": "18.x",
    "react-native": "0.71.x",
    "@react-navigation/native": "^6.1.0",
    "@react-native-async-storage/async-storage": "^1.17.0"
  },
  "scripts": {
    "start": "react-native start",
    "android": "react-native run-android",
    "ios": "react-native run-ios"
  }
}
```

> Replace versions with your actual project versions.

---

## 📥 Installation

### 1️⃣ Clone the project
```bash
git clone <your-repository-url>
cd <your-project-folder>
```

### 2️⃣ Install dependencies
```bash
npm install
```

### 3️⃣ (iOS only) Install Pods
```bash
cd ios
pod install
cd ..
```

---

## 🚀 Running the App

Start the Metro Bundler:
```bash
npm start
```

Run on Android:
```bash
npm run android
```

Run on iOS:
```bash
npm run ios
```

If using **Expo**:
```bash
expo start
```

---

## 📊 How Attendance Calculation Works

### Example Data Structure
```js
const attendanceData = {
  "2025-12-01": {
    "Batch A": {
      "student01": true,
      "student02": false
    }
  }
};
```

### Attendance Calculation Function
```js
function calculateBatchAttendance(attendanceByDate) {
  const dates = Object.keys(attendanceByDate);
  if (dates.length === 0) return { studentPercentages: {}, batchPercentage: 0 };

  const studentIds = new Set();
  dates.forEach(date => {
    Object.keys(attendanceByDate[date] || {}).forEach(id => studentIds.add(id));
  });

  const totals = {};
  studentIds.forEach(id => totals[id] = 0);

  dates.forEach(date => {
    const day = attendanceByDate[date];
    studentIds.forEach(id => {
      if (day && day[id]) totals[id] += 1;
    });
  });

  const studentPercentages = {};
  studentIds.forEach(id => {
    studentPercentages[id] = (totals[id] / dates.length) * 100;
  });

  const batchPercentage =
    Object.values(studentPercentages).reduce((s, p) => s + p, 0) / studentIds.size;

  return { studentPercentages, batchPercentage };
}
```

---

## 🧪 Usage Examples

### 📍 Mark attendance for today
```js
const today = new Date().toISOString().slice(0,10);

attendanceData[today] = attendanceData[today] || {};
attendanceData[today]["Batch A"] = {
  ...attendanceData[today]["Batch A"],
  "student01": true
};
```

### 📍 Show batch attendance percentages
```js
const result = calculateBatchAttendance(attendanceByDate);
console.log(result.studentPercentages);
console.log("Batch Average:", result.batchPercentage);
```

---

## ⚙️ Configuration

You may configure:
- Batch lists  
- Student lists  
- Attendance storage method (AsyncStorage, SQL, backend)  
- Navigation structure  
- Date format (`YYYY-MM-DD`)  

Suggested config folder:
```
/config/batches.json  
/config/students.json  
```

---

## 🐞 Troubleshooting

| Issue | Solution |
|-------|----------|
| Metro bundler stuck | `npm start -- --reset-cache` |
| Android build fails | `cd android && ./gradlew clean` |
| iOS Pod error | Run `pod install` again |
| Attendance % incorrect | Ensure date & batch structure is consistent |
| App runs only in Metro | Use `npm run android` or `npm run ios` |

---

## 🤝 Contributing

1. Fork the repository  
2. Create a feature branch  
3. Commit your changes  
4. Push and submit a PR  

---

## 👥 Contributors
Add your team members here:

- **Your Name** — Developer  
- **Contributor Name** — UI/UX  

---

## 📄 License
```
MIT © <2025> <Yogesh Kumar>
```
