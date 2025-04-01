# sit737-2025-prac5p

# 🔢 Advanced Calculator Microservice

## 📚 Overview
The **Advanced Calculator Microservice** is a lightweight and efficient **Node.js-based application** that provides a user-friendly interface for performing both **basic and advanced arithmetic operations**. It includes a **RESTful API** powered by **Express.js**, a **frontend (`index.html`)**, and a robust **logging system (`logger.js`)** for monitoring activities using **Winston**.

---

## 📂 mycal
This directory contains all the necessary files for running the Advanced Calculator Microservice.

---

## 🎯 Features

✅ **Basic Arithmetic Operations**: Addition, Subtraction, Multiplication, and Division  
✅ **Advanced Operations**: Exponentiation (Power), Square Root, and Modulo  
✅ **Dynamic UI**: Enables/disables input fields for specific operations  
✅ **RESTful API**: Handles calculations via HTTP requests  
✅ **Logging with Winston**: Captures all activities & errors in log files  

---

## 🏠 Technologies Used

| Technology | Purpose |
|------------|---------|
| **Node.js** | JavaScript runtime for backend |
| **Express.js** | Web framework to handle HTTP requests |
| **Winston** | Logging library for structured logging |
| **HTML, CSS, JavaScript** | Frontend for user interaction |

---

## 📝 File Descriptions

### 1️⃣ **`index.html`** - Frontend UI
A simple yet interactive calculator UI that communicates with the backend API to perform calculations.

🔹 **User Inputs**:
- Enter two numbers
- Select an operation
- Click "Calculate" to get the result  

🔹 **Dynamic UI**:
- If **Square Root (\u221a)** is selected, it disables the second input field.

🔹 **Frontend Logic**:
- Sends HTTP GET requests to the server
- Displays results dynamically  
- Handles API errors gracefully

---

### 2️⃣ **`server.js`** - Backend API
The **Express.js server** that:
- Serves the frontend (`index.html`)
- Provides a **REST API (`/calculate`)** to perform arithmetic operations
- Implements **error handling** for invalid inputs
- Logs every calculation request

**Supported API Operations:**
- `add` ➞ Addition (`num1 + num2`)
- `subtract` ➞ Subtraction (`num1 - num2`)
- `multiply` ➞ Multiplication (`num1 * num2`)
- `divide` ➞ Division (`num1 / num2`)
- `power` ➞ Exponentiation (`num1 ^ num2`)
- `sqrt` ➞ Square Root (`√num1`)
- `mod` ➞ Modulo (`num1 % num2`)

**Example API Request:**
```sh
GET http://localhost:3040/calculate?operation=add&num1=5&num2=3
```

---

## 🛠️ Docker Setup

### **Dockerfile**
This file contains the instructions to containerize the application.

```dockerfile
# Use an official Node.js runtime as the base image
FROM node:18

# Set the working directory in the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose port 3040
EXPOSE 3040

# Command to start the application
CMD ["npm", "start"]

# Health check to monitor the service
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
CMD curl --fail http://localhost:3040 || exit 1
```

---

### **Docker Compose File (`docker-compose.yml`)**
This file simplifies multi-container Docker applications and manages services efficiently.

```yaml
version: '3.8'
services:
  web:
    image: mycalapp:latest
    build: .
    ports:
      - "3040:3040"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=production
    restart: always  # Ensures the container restarts automatically if it crashes
    healthcheck:
      test: ["CMD", "curl", "--fail", "http://localhost:3040"]
      interval: 30s  # Perform the health check every 30 seconds
      timeout: 10s   # Wait up to 10 seconds for a response
      retries: 3     # Restart the container after 3 failed checks
```

---

## 🚀 Running the Application

### **Using Docker Compose**
1. **Build and Start the Containers**:
   ```sh
   docker-compose up -d --build
   ```
2. **Check Running Containers**:
   ```sh
   docker ps
   ```
3. **Inspect Container Logs**:
   ```sh
   docker logs container_id
   ```
4. **Stop and Remove Containers**:
   ```sh
   docker-compose down
   ```

---

## 🌟 Conclusion
The **Advanced Calculator Microservice** is now fully containerized, allowing seamless deployment across different environments. It automatically **monitors its health**, ensuring high availability and resilience. Happy coding! ✨

